<script>
  import axios from "axios";
  import { onMount } from "svelte";

  const path = "http://rum-cherezov-dt:5000/api/startclear";

  let freeVm = [];
  let snapList = [];
  let allCfg = {};
  let selectedVm = "";
  let selectedSnapshot = "";
  let snaplist = [];

  // $: snapList = allCfg[selectedVm].snap;

  function test_cfg(c) {
    // console.log(c);
    for (let key in c) {
      freeVm.push(key);
    }
    freeVm = freeVm;
    allCfg = c;
    console.log(allCfg);
  }

  // onMount(getTodos());

  // function getTodos() {
  axios.get(path).then(response => {
    test_cfg(response.data);
    // allCfg = response.data;
    // allCfg = allCfg;
    // console.log("allCfg");
    // console.log(allCfg);
  });
</script>

<style>
  h3 {
    /* text-align: center; */
    margin-bottom: 30px;
    font-weight: bold;
  }
  .wrapper {
    margin-top: 30px;
    display: grid;
    grid-template-columns: 400px 300px;
    grid-column-gap: 50px;
    justify-content: center;
  }
  .card {
    padding: 10px;
    /* background-color: aquamarine; */
  }
  .choice {
    color: green;
    font-weight: bold;
  }
  .btn {
    margin-top: 20px;
    text-align: center;
  }
  .btn-style {
    padding: 5px 15px;
    border-radius: 5px;
    font-weight: bold;
    color: white;
    background-color: green;
  }
</style>

<svelte:head>
  <title>ClearVM</title>
</svelte:head>

<div class="wrapper">
  <div class="card">
    <h3>Choose free VM</h3>
    {#each freeVm as free}
      <label>
        <input
          type="radio"
          bind:group={selectedVm}
          value={free}
          on:change={() => {
            selectedSnapshot = '';
            snapList = allCfg[selectedVm].snap;
          }} />
        {free}
      </label>
      <br />
    {/each}
    <br />
    <hr />
    <h3>Your choice:</h3>
    <p class="choice">{selectedVm} -- {selectedSnapshot}</p>
  </div>
  <div class="card">
    <h3>Choose snapshot</h3>
    {#if snapList}
      {#each snapList as sn}
        <label>
          <input type="radio" bind:group={selectedSnapshot} value={sn} />
          {sn}
        </label>
        <br />
      {/each}
    {/if}
  </div>
</div>
<div class="btn">
  {#if selectedSnapshot}
    <button class="btn-style">Start VM</button>
  {/if}
</div>
