<script>
  import axios from "axios";
  import { onMount } from "svelte";

  const path_cfg = "http://rum-cherezov-dt:5000/api/cfg";
  const path_run = "http://rum-cherezov-dt:5000/api/startclear";

  let freeVm = [];
  let snapList = [];
  let allCfg = {};
  let selectedVm = "";
  let selectedSnapshot = "";
  

  // $: snapList = allCfg[selectedVm].snap;

  function test_cfg(c) {
    // console.log(c);
    for (let key in c) {
      if (c[key].status == 'free') {
        freeVm.push(key);
      }
    }
    freeVm = freeVm;
    allCfg = c;
    console.log(allCfg);
  }
  function start_vm() {
    let vm_cfg = {'vm': selectedVm, 'snap': selectedSnapshot};
    axios.post(path_run, vm_cfg).then(response=> {
      console.log(response.data)
    })
  }
  // onMount(getTodos());

  // function getTodos() {
  axios.get(path_cfg).then(response => {
    test_cfg(response.data);
    // allCfg = response.data;
    // allCfg = allCfg;
    // console.log("allCfg");
    // console.log(allCfg);
  });
</script>

<style>
  h2 {
    text-align: center;
  }
  h3 {
    /* text-align: center; */
    margin-bottom: 30px;
    font-weight: bold;
  }
  .wrapper {
    margin-top: 30px;
    display: grid;
    grid-template-columns: 350px 300px;
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

<h2>Start clear virtual machine</h2>
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
    <button class="btn-style" on:click={start_vm}>Start VM</button>
  {/if}
</div>
