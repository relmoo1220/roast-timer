<script lang="ts">
  import "../app.css";

  let { children } = $props();
</script>

<div class="w-full h-screen">
  {@render children()}
</div>
