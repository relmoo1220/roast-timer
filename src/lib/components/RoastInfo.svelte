<script lang="ts">
  export let timerStarted: boolean;
  export let chargeTemp: number;
  export let endTemp: number;
</script>

<div class="flex items-center justify-center">
  <div class="flex border-1 border-yellow-900 rounded-2xl w-4/5 p-4 space-x-4">
    <label class="label w-1/2">
      <span class="label-text">Charge Temperature</span>
      <input
        class="input border border-yellow-900"
        type="text"
        placeholder="Temperature (°C)"
        disabled={!timerStarted}
        bind:value={chargeTemp}
      />
    </label>
    <label class="label w-1/2">
      <span class="label-text">End Temperature</span>
      <input
        class="input border border-yellow-900"
        type="text"
        placeholder="Temperature (°C)"
        disabled={!timerStarted}
        bind:value={endTemp}
      />
    </label>
  </div>
</div>
