<script>
  import { onMount } from "svelte";
  let grid = [];
  let matches = null;
  let response = {};
  let array = [];
  let rewardsArray = [];
  let sumOfRewards = 0;
  let reward = 0;

  /*   [...Array(5).keys()].forEach((getData) => console.log(Array(getData))); */
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
    console.log(res);
    let apiResponse = await res.json();
    console.log(apiResponse);

    /*     (grid = apiResponse.grid), (matches = apiResponse.matches);
     */ /*   (reward = apiResponse.reward); */
    /* grid = apiResponse.grid; */
    ({ grid, matches, reward } = apiResponse);
    /*   const another = { ...matches };
    for (let key in another) {
      console.log(key, another[key]);
    } */

    /*    matches.pairs.forEach((pair) => {
      rewardsArray.push(pair.reward);
    });
    matches.trips.forEach((trip) => {
      rewardsArray.push(trip.reward);
    });

    sumOfRewards = rewardsArray.reduce(
      (accumulator, currentValue) => accumulator + currentValue,
      0
    );
    console.log(rewardsArray);
    console.log(sumOfRewards);
    rewardsArray.length = 0; */
  };
  onMount(getData);
</script>

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

  <h1>Total payout:</h1>
  <p>{reward}</p>
  <!-- <h1>payout: {response.reward ?? ""}</h1> -->
  <button on:click={getData}>Run</button>
</div>

<style>
  .box {
    background-color: #2aa3c2;
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
  .card {
    background-color: #2e8799;
    border-radius: 4px;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    padding: 16px;
    max-width: 500px;
    margin: 0 auto;
  }
  .highlight {
    border: 1px solid rgba(12, 0, 0, 0.904);
  }
</style>
