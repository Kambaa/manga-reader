<script>
  import { fade, fly } from "svelte/transition";
  export let src;
  export let alt;
</script>

<img
  in:fly={{ x: -200, duration: 200 }}
  out:fade
  src="data:image/png;base64,{src}"
  {alt}
/>
