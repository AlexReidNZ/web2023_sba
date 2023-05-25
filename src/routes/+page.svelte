<script>
  import { onMount } from "svelte";
  import Card from "../lib/+card.svelte";

  const BASE_URL = "https://rickandmortyapi.com/api/";

  let characters = [];
  let totalCharacters;

  onMount(async () => {
    //Randomly get 6 characters and assign them to an array
    for (let i = 0; i < 6; i++) {
      fetch(`${BASE_URL}/character/`)
        .then((res) => res.json())
        .then((data) => {
          totalCharacters = data.info.count; //Get the total number of characters in the api
          return fetch(`${BASE_URL}/character/${Math.floor(Math.random() * totalCharacters )}`); //Get a random character from that number
        })
        .then((res) => res.json())
        .then((data) => {
          characters = [...characters, data]; //Add that character to the array
        });
    }
  });
</script>

<div class="grid">
  {#each characters as character}
    <!--Display a card for each character-->
    <Card
      name={character.name}
      status={character.status}
      species={character.species}
      location={character.location}
      image={character.image}
    />
  {/each}
</div>

<style>
  .grid {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 30px;
  }
</style>
