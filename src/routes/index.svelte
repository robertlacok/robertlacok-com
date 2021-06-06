<script context="module">
  const posts = import.meta.glob("./recipes/*.{md,svx}");

  let body = [];

  for (const path in posts) {
    body.push(
      posts[path]().then(({ metadata }) => {
        return {
          metadata,
          path,
        };
      })
    );
  }
  /**
   * @type {import('@sveltejs/kit').Load}
   */
  export async function load() {
    const res = await Promise.all(body);
    const posts = res;
    return {
      props: {
        posts,
      },
    };
  }
</script>

<script>
  import { paginate, PaginationNav } from "svelte-paginate";
  //https://www.npmjs.com/package/svelte-paginate

  export let posts;

  let items = posts;
  let currentPage = 1;
  let pageSize = 200;
  $: paginatedItems = paginate({ items, pageSize, currentPage });
</script>

<main>
  <article>
    <h1 class="font-bold text-6xl mb-12">Čo jesť?</h1>
    <p class="mb-8">Minimalistická zbierka receptov. Aby sa na ne nezabudlo.</p>
    <div class="article-list">
      {#each paginatedItems as { metadata: { title, description, tags, outline, slug }, path }}
        <div class="mb-4">
          <a sveltekit:prefetch href={path.replace(/\.[^/.]+$/, "")}
            ><h2 class="text-3xl leading-relaxed">{title}</h2></a
          >
          {#if description}
            <small>{description}</small>
          {/if}
        </div>
      {/each}
    </div>
    {#if posts.length > pageSize}
      <div class="mx-auto">
        <PaginationNav
          totalItems={items.length}
          {pageSize}
          {currentPage}
          limit={1}
          showStepOptions={true}
          on:setPage={(e) => (currentPage = e.detail.page)}
        />
      </div>
    {/if}
  </article>
</main>
