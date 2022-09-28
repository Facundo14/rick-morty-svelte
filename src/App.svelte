<script>
  import Character from './lib/Character.svelte';
  let characters = [];
  let page = 1;
  async function loadCharacters() {
    const res = await fetch(`https://rickandmortyapi.com/api/character?page=${page}`);
    const data = await res.json();

    characters = data.results;

    console.log(characters);
  }

  loadCharacters();

  function nextPage(){
    page++;
    loadCharacters();
  }

  function prevPage(){
    page--;
    loadCharacters();
  }
</script>
<main class="container">
  <h1 class="title">Rick and Morty Svelte</h1>
  <div class="btns">
    <button class="btn" on:click={prevPage} disabled={page===1}>Prev</button>
    <button class="btn" on:click={nextPage}>Next</button>
  </div>
  <div class="grid">
    {#each characters as character}
      <Character character={character} />
    {/each}
  </div>
</main>
