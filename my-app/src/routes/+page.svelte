<script>
  import { onMount } from "svelte";
  let grid = [];
  let matches = null;
  let response = {};
  let array = [];
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

    (grid = apiResponse.grid),
      (matches = apiResponse.matches),
      (reward = apiResponse.reward);
    /* grid = apiResponse.grid; */
  };
  onMount(getData);
</script>

<div class="card">
  <div>
    <table>
      {#each grid as row}
        <tr>
          {#each row as cell}
            <td>{cell}</td>
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

  <h1>payout: {response.reward ?? ""}</h1>
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
    background-color: #fff;
    border-radius: 4px;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    padding: 16px;
    max-width: 500px;
    margin: 0 auto;
  }
</style>
