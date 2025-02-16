<script lang="ts">
  import Hamburger from "$lib/Hamburger.svelte";
  import "../app.css";

  let { children } = $props();
  let navOpen = $state(false);

  const pages = import.meta.glob("/src/routes/**/+page.svelte", { eager: true });
  let routes = [];

  for (const path in pages) {
    let route = path
      .replace(/^.*\/src\/routes/, "")
      .replace("/+page.svelte", "");
    if (route === "") {
      route = "/";
    }
    routes.push(route);
  };
</script>

<div class="min-h-screen">
  <nav class="fixed top-0 w-screen h-16 transition-colors duration-250 dark:bg-dark-900 backdrop-blur-3xl flex items-center">
    <Hamburger on:click={() => navOpen = !navOpen} open={navOpen} />
    <input type="checkbox" onclick={() => document.documentElement.classList.toggle("dark")} checked={true} />  
  </nav>

  <div class="flex transition-colors duration-250 mt-16 bg-gray-800">
    <nav class={`w-64 h-screen bg-gray-800 text-white transition-all duration-300 ${navOpen ? "ml-0" : "-ml-64"}`}>
      <ul class="p-4">
        {#each routes as route}
          <li class="py-2">
            <a href="{route}" class="hover:underline">
              {route}
            </a>
          </li>
        {/each}
      </ul>
    </nav>

    <article class="flex-grow transition-transform duration-250 p-8 rounded-tl-xl bg-blue-800">
      {@render children()}
    </article>


  </div>
  
  <footer class="p-4 transition-colors duration-250 bg-gray-700 text-white text-center">
    © 2023 Your Company Name. All rights reserved.
  </footer>
</div>