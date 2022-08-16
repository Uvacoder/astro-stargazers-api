<!--src/components/Image.svelte-->
<script>
  export let title = '';
  export let url = '';
  export let alt = '';
  export let media_type = 'image';
</script>

<figure>
  {#if media_type === 'image'}
    <img class="media" src={url} alt={alt} />
  {:else}
    <!--for videos and other media, embed with an iframe-->
    <iframe class="media" title={title} width="500" height="300" src={url}></iframe>
  {/if}
  <figcaption>
    <!--slot extra information like a "learn more" link or image description-->
    <slot name="figcaption" />
  </figcaption>
</figure>

<style>
  figure {
    background: var(--grey-1);
    border: 2px solid var(--grey-2);
    box-shadow: var(--box-shadow-glow);
    border-radius: 0.5rem;
    margin: 0;
    padding-bottom: 1rem;
  }

  figcaption {
    padding-inline: 1rem;
  }

  .media {
    width: 100%;
    height: auto;
    aspect-ratio: 16 / 10;
    object-fit: cover;
    border-radius: inherit;
    border: none;
  }
</style>