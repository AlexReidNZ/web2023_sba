<script>
  import { page } from "$app/stores";
  import { onMount } from "svelte";

  const BASE_URL = "https://rickandmortyapi.com/api/";
  const location_id = $page.url.searchParams.get("id");
  console.log(location_id);

  let location = { name: "", type: "", dimension: "", residents: 0 };

  onMount(async () => {
    //Fetch the data for the location with the given ID
    fetch(`${BASE_URL}/location/${location_id}`)
      .then((res) => res.json())
      .then((data) => {
        location.name = data.name;
        location.type = data.type;
        location.dimension = data.dimension;
        location.residents = data.residents;
      });
  });
</script>

<div>
  <h1>{location.name}</h1>
  <h3>{location.type} | {location.dimension}</h3>
  <h5>{location.residents.length} residents</h5>
</div>
