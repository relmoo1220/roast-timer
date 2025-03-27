<script lang="ts">
  import { writable } from "svelte/store";

  export let timerStarted: boolean;
  export let elapsedTime: number;

  let timerInterval: any;

  // Functions to start and stop the timer
  export function startTimer() {
    if (!timerStarted) {
      timerStarted = true;
      timerInterval = setInterval(() => {
        elapsedTime = elapsedTime + 10; // Increase time by 10 milliseconds
      }, 10);
    }
  }

  export function stopTimer() {
    clearInterval(timerInterval);
    timerStarted = false;
  }

  // Reset the timer
  export function resetTimer() {
    clearInterval(timerInterval);
    timerStarted = false;
    elapsedTime = 0; // Reset elapsed time to 0
  }

  // Format the time into minutes, seconds, and milliseconds
  function formatTime() {
    const currentElapsedTime = elapsedTime; // Reactive value from store
    const minutes = Math.floor(currentElapsedTime / 60000);
    const seconds = Math.floor((currentElapsedTime % 60000) / 1000);
    const milliseconds = Math.floor((currentElapsedTime % 1000) / 10);
    return {
      minutes: String(minutes).padStart(2, "0"),
      seconds: String(seconds).padStart(2, "0"),
      milliseconds: String(milliseconds).padStart(2, "0"),
    };
  }
</script>

<div class="flex flex-col text-center">
  <!-- Displaying formatted time -->
  <h1 class="text-6xl font-semibold p-2">
    {formatTime().minutes}:{formatTime().seconds}:{formatTime().milliseconds}
  </h1>

  <!-- Buttons to start, stop, and reset timer -->
  <div class="mt-4">
    <button
      type="button"
      class="btn preset-filled-warning-500"
      on:click={startTimer}
      disabled={timerStarted}
      >Start
    </button>

    <button
      type="button"
      class="btn preset-filled-error-500"
      on:click={stopTimer}
      disabled={!timerStarted}
      >Stop
    </button>
    <button
      type="button"
      class="btn preset-filled-surface-500"
      on:click={resetTimer}>Reset</button
    >
  </div>
</div>
