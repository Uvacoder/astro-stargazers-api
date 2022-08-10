<script lang="ts">
import { fly } from 'svelte/transition';
import Image from './Image.svelte';

export let images: any[] = [];

let currentIdx = 0;
function next() {
  currentIdx = (currentIdx + 1) % images.length;
}
function previous() {
  if (currentIdx === 0) {
    currentIdx = images.length - 1;
  } else {
    currentIdx -= 1;
  }
}

</script>

<div class="buttons">
  <button on:click={previous}>
    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" role="img" class="iconify iconify--material-symbols" width="32" height="32" preserveAspectRatio="xMidYMid meet" viewBox="0 0 24 24"><title>Previous</title><path fill="currentColor" d="m12.3 15.3l-2.6-2.6q-.15-.15-.225-.325Q9.4 12.2 9.4 12t.075-.375q.075-.175.225-.325l2.6-2.6q.475-.475 1.087-.212q.613.262.613.937v5.15q0 .675-.613.937q-.612.263-1.087-.212Z"></path></svg>
  </button>
  <h2>{images[currentIdx].title}</h2>
  <button on:click={next}>
    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" role="img" class="iconify iconify--material-symbols" width="32" height="32" preserveAspectRatio="xMidYMid meet" viewBox="0 0 24 24"><title>Next</title><path fill="currentColor" d="M11.7 15.3q-.475.475-1.087.212Q10 15.25 10 14.575v-5.15q0-.675.613-.937q.612-.263 1.087.212l2.6 2.6q.15.15.225.325q.075.175.075.375t-.075.375q-.075.175-.225.325Z"></path></svg>
  </button>
</div>
<div class="images">
  {#each images as image, idx}
  {#if idx === currentIdx}
    <div class="image-container" transition:fly={{ y: 30 }}>
      <Image {image}>
        <a slot="figcaption" href={`/${image.date}`}>Learn more</a>
      </Image>
    </div>
  {/if}
  {/each}
</div>

<style>
  .images {
    display: flex;
		position: relative;
    width: 100%;
	}

  .buttons {
    display: grid;
    grid-template-columns: 3rem 1fr 3rem;
  }

  .image-container {
    position: absolute;
    height: min-content;
    inset: 0;
  }

  button {
    background: none;
    border: none;
    color: var(--color-text-secondary);
    border-radius: 0.3rem;
    transition: background-color 0.2s;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  button:hover, button:focus-visible {
    background-color: var(--grey-2);
  }

  button svg {
    width: 100%;
    height: auto;
  }

  h2 {
    text-align: center;
    font-size: var(--font-size-base);
  }

  a, a:visited {
    display: flex;
    justify-content: center;
    padding: 0.5rem;
  }
</style>