<script lang="ts">
  export let elapsedTime: number;
  export let timerStarted: boolean;
  export let dryEndTemp: number;
  export let firstCrackTemp: number;
  export let developmentEndTemp: number;
  export let dryEndTime: number;
  export let firstCrackTime: number;
  export let developmentEndTime: number;

  let dryEndMarked: boolean = false;
  let firstCrackMarked: boolean = false;
  let developmentEndMarked: boolean = false;

  // Mark the specified stage and store the time
  function markStage(stage: string) {
    switch (stage) {
      case "dryEnd":
        dryEndMarked = true;
        dryEndTime = elapsedTime; // Store the current elapsed time for Dry End
        break;
      case "firstCrack":
        firstCrackMarked = true;
        firstCrackTime = elapsedTime; // Store the current elapsed time for First Crack
        break;
      case "developmentEnd":
        developmentEndMarked = true;
        developmentEndTime = elapsedTime; // Store the current elapsed time for Development End
        break;
      default:
        console.error("Invalid stage");
    }
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

<div class="flex items-center justify-center">
  <div class="table-wrap border-1 border-yellow-900 rounded-2xl w-4/5 p-4">
    <table class="table caption-bottom">
      <thead>
        <tr>
          <th>Dry End</th>
          <th>First Crack</th>
          <th>Development End</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>
            {dryEndMarked
              ? `${formatTime(dryEndTime).minutes}:${formatTime(dryEndTime).seconds}`
              : "Not Marked"}
          </td>
          <td>
            {firstCrackMarked
              ? `${formatTime(firstCrackTime).minutes}:${formatTime(firstCrackTime).seconds}`
              : "Not Marked"}
          </td>
          <td>
            {developmentEndMarked
              ? `${formatTime(developmentEndTime).minutes}:${formatTime(developmentEndTime).seconds}`
              : "Not Marked"}
          </td>
        </tr>
        <tr>
          <td>
            <label class="label">
              <input
                class="input border border-yellow-900"
                type="text"
                placeholder="Temperature (°C)"
                disabled={!dryEndMarked}
                bind:value={dryEndTemp}
              />
            </label>
          </td>
          <td>
            <label class="label">
              <input
                class="input border border-yellow-900"
                type="text"
                placeholder="Temperature (°C)"
                disabled={!firstCrackMarked}
                bind:value={firstCrackTemp}
              />
            </label>
          </td>
          <td>
            <label class="label">
              <input
                class="input border border-yellow-900"
                type="text"
                placeholder="Temperature (°C)"
                disabled={!developmentEndMarked}
                bind:value={developmentEndTemp}
              />
            </label>
          </td>
        </tr>
        <tr>
          <td>
            <button
              type="button"
              class="btn preset-tonal-warning"
              disabled={dryEndMarked || !timerStarted}
              on:click={() => markStage("dryEnd")}
            >
              Mark
            </button>
          </td>
          <td>
            <button
              type="button"
              class="btn preset-tonal-warning"
              disabled={firstCrackMarked || !timerStarted}
              on:click={() => markStage("firstCrack")}
            >
              Mark
            </button>
          </td>
          <td>
            <button
              type="button"
              class="btn preset-tonal-warning"
              disabled={developmentEndMarked || !timerStarted}
              on:click={() => markStage("developmentEnd")}
            >
              Mark
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</div>
