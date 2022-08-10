<script>
  export let image = {};
</script>

<figure>
  {#if image.media_type === 'image'}
    <img class="media" src={image.url} alt={image.explanation} />
  {:else}
    <iframe class="media" title={image.title} width="500" height="300" src={image.url}></iframe>
  {/if}
  <figcaption>
    <slot name="figcaption" /> 
  </figcaption>
</figure>

<style>
  figure {
    background: var(--grey-1);
    border: 2px solid var(--grey-2);
    box-shadow: var(--box-shadow-glow);
    padding: 1.5rem;
    border-radius: 0.5rem;
    margin: 0;
  }

  .media {
    width: 100%;
    height: auto;
    aspect-ratio: 16 / 10;
    object-fit: cover;
  }
</style>