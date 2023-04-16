<!-- <script>
  import { onMount } from "svelte";
<<<<<<< Updated upstream

=======
  const rewardsArray = [];
  let grid = [];
  let matches = null;
>>>>>>> Stashed changes
  let response = {};

  let array = [];
<<<<<<< Updated upstream
  [...Array(5).keys()].forEach((getData) => console.log(Array(getData)));
=======
  let reward = 0;
  /*   [...Array(5).keys()].forEach((getData) => console.log(Array(getData))); */
>>>>>>> Stashed changes
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
<<<<<<< Updated upstream
    response = {
      currentPayout: apiResponse.payout,
      slotText: apiResponse.result,
    };
=======

    (grid = apiResponse.grid), (matches = apiResponse.matches);
    reward = apiResponse.reward;
    /* grid = apiResponse.grid; */

    /*  const another = { ...matches };
    for (let key in another) {
      console.log(key, another[key]);
    }
    console.log(another.pairs.reward); */

    matches.pairs.forEach((pair) => {
      rewardsArray.push(pair.reward);
    });
    matches.trips.forEach((trip) => {
      rewardsArray.push(trip.reward);
    });

    const sumOfRewards = rewardsArray.reduce(
      (accumulator, currentValue) => accumulator + currentValue,
      0
    );
    console.log(rewardsArray); // output: [15, 30]
    console.log(sumOfRewards); // output: 45
>>>>>>> Stashed changes
  };
  onMount(getData);
</script>

<<<<<<< Updated upstream
<div class="box">
  <h1>Combination: {response.slotText}</h1>
  <h1>payout: {response.currentPayout ?? ""}</h1>
=======
<div class="card">
  <div>
    <table>
      {#each grid as row, i}
        <!--  {#if matches.pairs.some( (pair) => pair.position.some( (pos) => pos.includes(i)) ) }
          <h1>true</h1>
        {/if} -->
        <tr>
          {#each row as cell, j}
            <td
              class={matches.pairs.some((pair) =>
                pair.position.some((pos) => pos[0] === i && pos[1] === j)
              ) ||
              matches.trips.some((trip) =>
                trip.position.some((pos) => pos[0] === i && pos[1] === j)
              )
                ? "highlight"
                : ""}>{cell}</td
            >
          {/each}
        </tr>
      {/each}
    </table>
  </div>

  <div>
    <h2>Matches :</h2>
    {#if matches}
      <ul>
        <li>Trips: {JSON.stringify(matches.trips)}</li>
        <li>Pairs: {JSON.stringify(matches.pairs)}</li>
      </ul>
    {/if}
  </div>

  <h1>
    Total payout:{sumOfRewards}
  </h1>
  <!-- <h1>payout: {response.reward ?? ""}</h1> -->
>>>>>>> Stashed changes
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
