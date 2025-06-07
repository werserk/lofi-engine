<script lang="ts">
  import { IconCampfire } from "@tabler/icons-svelte";
  import { onMount } from "svelte";
  import { convertFileSrc } from "@tauri-apps/api/tauri";

  export let volume: number;

  let fire = new Audio(convertFileSrc("assets/engine/effects/fire.mp3"));
  let isFire = false;

  function toggleStorm() {
    if (isFire) {
      fire.pause();
    } else {
      fire.play();
      fire.loop = true;
      fire.volume = volume;
    }

    isFire = !isFire;
  }

  // Shortuct to toggle fire with "F" key
  window.addEventListener("keydown", (e) => {
    if (e.key === "f") {
      toggleStorm();
    }
  });

  // Update volume
  onMount(() => {
    setInterval(() => {
      fire.volume = volume;
    },100);
  });
</script>

<button
  style={`
        background-color: ${isFire ? "white" : "transparent"};
        `}
  on:click={toggleStorm}
>
  <IconCampfire size={25} color={isFire ? "black" : "white"} />
</button>

<style>
  button {
    color: white;
    border-radius: 50%;
    aspect-ratio: 4/4;
  }
</style>
