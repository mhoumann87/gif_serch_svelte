<script>
  import config from "./config.js";
  let search = "";
  let loading = false;
  const API_URL = "https://api.giphy.com/v1/gifs/search?api_key=";
  let gifs = [];

  async function formSubmitted(e) {
    e.preventDefault();
    gifs = [];
    let search_url = `${API_URL}${config.apiKey}&q=${search}`;
    loading = true;

    const response = await fetch(search_url);
    const json = await response.json();
    gifs = json.data.map(gif => gif.images.original.url);
    loading = false;
    search = "";
  }
</script>

<style>
  .loader {
    border: 16px solid var(--border-color);
    border-top-color: var(--accent-color);
    border-radius: 50%;
    width: 200px;
    height: 200px;
    animation: spin 2s linear infinite;
    margin: 3rem auto;
  }

  @keyframes spin {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }

  .gifs {
    width: 90%;
    margin: 3em auto;
  }

  @media screen and (min-width: 749px) {
    .gifs {
      width: 80%;
      column-count: 3;
    }
  }

  img {
    width: 100%;
    height: auto;
    display: block;
    margin-bottom: 0.5em;
  }
</style>

<header>
  <h1>Search for gifs</h1>
</header>

<form on:submit={formSubmitted}>
  <label for="search">Search for:</label>
  <input bind:value={search} id="search" name="search" />
  <button type="submit" name="submit">Search!</button>
</form>
{#if loading}
  <div class="loader" />
{/if}
<div class="gifs">
  {#each gifs as gif}
    <img src={gif} alt="gif" />
  {/each}
</div>
