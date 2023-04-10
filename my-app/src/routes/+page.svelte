<!-- <script>
  import { onMount } from "svelte";

  let response = {};

  let array = [];
  [...Array(5).keys()].forEach((getData) => console.log(Array(getData)));
  const getData = async () => {
    let bet = 100;
    const res = await fetch(
      "https://us-central1-ccc-slots.cloudfunctions.net/api/v2",
      {
        method: "POST",
        mode: "cors",
        cache: "no-cache",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ bet }),
      }
    );
    /*  console.log(res); */
    let apiResponse = await res.json();
    console.log(apiResponse);
    response = {
      currentPayout: apiResponse.payout,
      slotText: apiResponse.result,
    };
  };
  onMount(getData);
</script>

<div class="box">
  <h1>Combination: {response.slotText}</h1>
  <h1>payout: {response.currentPayout ?? ""}</h1>
  <button on:click={getData}>Run</button>
</div>

<style>
  .box {
    border-radius: 16px;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
    padding: 24px;
    background-color: #fff;
  }
</style>
 -->

<script>
  let grid = [];
  let trips = [];
  let pairs = [];
  let reward = 0;

  const fetchData = async () => {
    // fetch data from API endpoint
    const response = await fetch(
      "https://us-central1-ccc-slots.cloudfunctions.net/api/v2"
    );
    const data = await response.json();
    console.log(data);
    // update variables with new data
    grid = data.grid;
    trips = data.matches.trips;
    pairs = data.matches.pairs;
    reward = data.reward;
  };
</script>

<div class="card" />

<style>
  .card {
    background-color: #fff;
    box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.1);
    border-radius: 5px;
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  button {
    margin-top: 20px;
    padding: 10px 20px;
    border-radius: 5px;
    border: none;
    background-color: #3366cc;
    color: #fff;
    font-weight: bold;
    cursor: pointer;
  }

  button:hover {
    background-color: #265799;
  }
</style>
