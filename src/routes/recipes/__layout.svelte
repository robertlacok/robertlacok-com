<script>
  import "../../app.postcss";
  import "../../style.css";
</script>

<div class="body-wrapper max-w-screen-md mx-auto">
  <slot />
</div>

<svelte:head>
  <title>Čo jesť?</title>
  <meta
    name="description"
    content="Minimalistická zbierka receptov, ktoré boli niekedy v pravidelnej rotácii, ale už nie sú. Tak aby sa na ne nezabudlo."
  />
</svelte:head>
