<script lang="ts">
  import RoastInfo from "$lib/components/RoastInfo.svelte";
  import RoastTable from "$lib/components/RoastTable.svelte";
  import Timer from "$lib/components/Timer.svelte";

  let elapsedTime: number = 0;
  let timerStarted: boolean = false;

  let chargeTemp: number;
  let endTemp: number;
  let dryEndTemp: number;
  let firstCrackTemp: number;
  let developmentEndTemp: number;

  let dryEndTime: number;
  let firstCrackTime: number;
  let developmentEndTime: number;

  function generateReport() {
    const formattedDryEndTime = `${formatTime(dryEndTime).minutes}:${formatTime(dryEndTime).seconds}`;
    const formattedFirstCrackTime = `${formatTime(firstCrackTime).minutes}:${formatTime(firstCrackTime).seconds}`;
    const formattedDevelopmentTime = `${formatTime(developmentEndTime).minutes}:${formatTime(developmentEndTime).seconds}`;

    const report = {
      chargeTemp: chargeTemp,
      endTemp: endTemp,
      dryEnd: {
        dryEndTemp: dryEndTemp,
        dryEndTime: formattedDryEndTime,
      },
      firstCrack: {
        firstCrackTemp: firstCrackTemp,
        firstCrackTime: formattedFirstCrackTime,
      },
      developmentEnd: {
        developmentEndTemp: developmentEndTemp,
        developmentEndTime: formattedDevelopmentTime,
      },
    };
    console.log(report);
  }

  function formatTime(time: number) {
    const minutes = Math.floor(time / 60000);
    const seconds = Math.floor((time % 60000) / 1000);
    const milliseconds = Math.floor((time % 1000) / 10);
    return {
      minutes: String(minutes).padStart(2, "0"),
      seconds: String(seconds).padStart(2, "0"),
      milliseconds: String(milliseconds).padStart(2, "0"),
    };
  }
</script>

<div
  class="flex flex-col w-full h-full justify-center items-center bg-yellow-900"
>
  <div class="flex w-full h-full justify-between items-center pl-30 pr-30">
    <div class="flex space-x-2 items-center">
      <img class="w-10 h-10" src="coffee-bean.svg" alt="coffee-bean" />
      <div class="font-extrabold text-2xl pb-4 pt-4">Roast Timer</div>
    </div>
    <div class="flex">
      <button type="button" class="btn preset-filled-primary-500">
        <div class="flex space-x-2 items-center">
          <div class="font-bold">Login</div>
          <img class="w-6 h-6" src="notion-logo.svg" alt="notion-logo" />
        </div>
      </button>
    </div>
  </div>

  <div class="flex w-full h-full pl-30 pr-30 pb-10">
    <div
      class="flex flex-col justify-center items-center w-full h-full space-y-4 bg-black"
    >
      <Timer bind:timerStarted bind:elapsedTime />
      <RoastInfo bind:timerStarted bind:chargeTemp bind:endTemp />
      <RoastTable
        bind:dryEndTemp
        bind:firstCrackTemp
        bind:developmentEndTemp
        bind:dryEndTime
        bind:firstCrackTime
        bind:developmentEndTime
        bind:timerStarted
        bind:elapsedTime
      />
      <button
        type="button"
        class="btn preset-filled-warning-500 m-4"
        on:click={generateReport}
        disabled={timerStarted}
        >Generate Report
      </button>
    </div>
  </div>
</div>
