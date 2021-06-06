<script>
  export let title;
  export let description;
  export let slug;
  export let imagePath;

  let image = imagePath ? imagePath : slug;
</script>

<h1 class="font-bold text-6xl mb-12">{title}</h1>

<article class="post">
  <slot />
</article>

<div class="mb-4">
  <a href="/recipes"> &larr; Späť</a>
</div>

<div class="recipe-img mb-4">
  <img class="recipe-img" src="/pictures/{image}.jpg" onerror="this.style.display = 'none'" alt={title} />
</div>

<svelte:head>
  <title>{title}</title>
  <meta name="description" content={description} />
</svelte:head>

<style>
  .post {
    margin-bottom: 4rem;
  }
  .recipe-img {
    border-radius: 5px;
  }
</style>
