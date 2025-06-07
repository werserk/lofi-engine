<script lang="ts">
  import { IconTrees } from "@tabler/icons-svelte";
  import { onMount } from "svelte";
  import { convertFileSrc } from "@tauri-apps/api/tauri";

  export let volume: number;

  let jungle = new Audio(convertFileSrc("assets/engine/effects/jungle.mp3"));
  let isActive = false;

  function toggleSound() {
    if (isActive) {
      jungle.pause();
    } else {
      jungle.play();
      jungle.loop = true;
      jungle.volume = volume;
    }

    isActive = !isActive;
  }

  // Shortuct to toggle jungle with "D" key
  window.addEventListener("keydown", (e) => {
    if (e.key === "d") {
      toggleSound();
    }
  });
  // Update volume
  onMount(() => {
    setInterval(() => {
      jungle.volume = volume;
    },100);
  });
</script>

<button
  style={`
        background-color: ${isActive ? "white" : "transparent"};
        `}
  on:click={toggleSound}
>
  <IconTrees size={25} color={isActive ? "black" : "white"} />
</button>

<style>
  button {
    color: white;
    border-radius: 50%;
    aspect-ratio: 4/4;
  }
</style>
