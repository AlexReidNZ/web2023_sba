<script>
  import { onMount } from "svelte";

  export let name;
  export let status;
  export let species;
  export let location;
  export let image;

  let locationID;

  onMount(async () => {
    //Get the locations ID from the location object
    fetch(`${location.url}`)
      .then((res) => res.json())
      .then((data) => {
        locationID = data.id;
        locationID = locationID;
      });
  });
</script>

<div class="card">
  <img src={image} alt="image of {name}" />
  <div class="info">
    <h1>{name}</h1>
    <h3 class="status">
      <div class="{status.toLowerCase()} statusCircle" />
      {status} - {species}
    </h3>
    <h3 class="locationLabel">Last known location</h3>
    <h3 class="location">
      <a href="/location?id={locationID}">{location.name}</a>
    </h3>
  </div>
</div>

<style>
  .card {
    font-family: sans-serif;
    color: white;
    background: #333;
    overflow: hidden;
    height: 240px;
    display: flex;
    border-radius: 20px;
  }

  img {
    width: 30%;
    background-size: cover;
    background-position: center;
  }

  .info {
    padding: 10px 20px 15px;
  }

  .statusCircle {
    width: 10px;
    height: 10px;
    border-radius: 100%;
    margin-right: 10px;
  }

  .dead {
    background: firebrick;
  }

  .alive {
    background: green;
  }

  .unknown {
    background: gray;
  }

  .status {
    color: white;
    display: flex;
    align-items: center;
  }

  .locationLabel {
    color: #777;
    font-size: 16px;
    margin: 0 0 5px;
  }

  .location {
    font-size: 16px;
    margin: 0 0 5px;
  }

  .location a {
    color: white;
    font-size: 16px;
    margin: 0 0 5px;
  }
</style>
