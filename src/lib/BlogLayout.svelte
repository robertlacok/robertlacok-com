<script>
  export let title;
  export let description;
</script>

<h1 class="font-bold text-6xl mb-12">{title}</h1>

<div class="post">
  <slot />
</div>

<div class="mb-4">
  <a href="/"> &larr; Späť</a>
</div>

<svelte:head>
  <title>{title}</title>
  <meta name="description" content={description} />
</svelte:head>

<style>
  .post {
    margin-bottom: 4rem;
  }
</style>
