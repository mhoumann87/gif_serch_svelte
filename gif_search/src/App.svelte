<script>
  import config from "./config.js";

  console.log(config.apiKey);
  export let search = "";
</script>

<style>

</style>

<form>
  <label for="search">Search</label>
  <input bind:value={search} id="search" name="search" />
</form>
<h2>{search}</h2>
