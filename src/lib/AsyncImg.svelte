<script>
  import { onMount } from "svelte";
  import Img from "./Img.svelte";

  export let promise;

  let showImg = false;
  let src;

  

  if (promise) {
    console.log("Promise found!");

    promise.then(
      function (base64Str) {
        src = base64Str;
        showImg = true;
      },
      function (e) {
        console.log(e);
        throw "promise Error : " + e.message;
      }
    );
  } else {
    console.log("Promise not found!");
  }
</script>

{#if src}
  <Img {src} alt="alt" />
{/if}
