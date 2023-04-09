<script>
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
    console.log(res);
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

<!-- <script>
  import { onMount } from 'svelte';
  import { Line } from 'svelte-chartjs';

  let slotMachineData = [];
  let graphData = {
    labels: [],
    datasets: [
      {
        label: 'Wins',
        data: [],
        borderColor: 'blue',
        fill: false
      },
      {
        label: 'Losses',
        data: [],
        borderColor: 'red',
        fill: false
      }
    ]
  };

  onMount(async () => {
    const response = await fetch('https://us-central1-ccc-slots.cloudfunctions.net/api/v1');
    const data = await response.json();
    slotMachineData = data.slotMachineData;
    graphData.labels = data.graphData.labels;
    graphData.datasets[0].data = data.graphData.wins;
    graphData.datasets[1].data = data.graphData.losses;
  });
</script>

<main>
  <h1>Slot Machine Data</h1>
  <table>
    <thead>
      <tr>
        <th>Spin ID</th>
        <th>Result</th>
        <th>Win/Loss</th>
      </tr>
    </thead>
    <tbody>
      {#each slotMachineData as spin}
        <tr>
          <td>{spin.spinId}</td>
          <td>{spin.result}</td>
          <td>{spin.winLoss}</td>
        </tr>
      {/each}
    </tbody>
  </table>
  <h1>Graph Data</h1>
  <Line {data=graphData} />
</main> -->

<style>
  .box {
    position: relative;
    right: 4 rem;
    top: 4 rem;
    padding: 20px;
    width: 400px;
    height: 400px;
    border-radius: 50px;
    background: #18c0c3;
    box-shadow: inset -28px -28px 56px #14a3a6, inset 28px 28px 56px #1cdde0;
  }
</style>
