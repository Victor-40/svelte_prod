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
    console.log(allCfg)
  };

// onMount(getTodos());

// function getTodos() {
axios
  .get(path)
  .then(response  => {
    test_cfg(response.data);
    // allCfg = response.data;
    // allCfg = allCfg;
    // console.log("allCfg");
    // console.log(allCfg);
  });
</script>

<style>
  /* table {
    border: 1px solid;
  } */
  td,
  th {
    padding-left: 7em;
    text-align: left;
    vertical-align: top;
  }
  th {
    padding-bottom: 20px;
  }
  .layer {
    width: 80%;
    margin: 0 auto;
  }
  h2 {
    text-align: center;
    margin-bottom: 30px;
  }
  /* ul {
    list-style: none;
    padding-left: 0;
  } */
	/* .busy {
		color: red;
	} */
</style>

<svelte:head>
  <title>About</title>
</svelte:head>

<div>
  <h2>Start clear VM</h2>
  <table class="layer">
    <tr>
      <th>Choose free VM</th>
      <th>Choose snapshot</th>
    </tr>
    <tr>
      <td>
        {#each freeVm as free}
          <label>
            <input type="radio" bind:group={selectedVm} value={free}  on:change={()=>{selectedSnapshot=''; snapList = allCfg[selectedVm].snap;}} />
          {free}
          </label><br>
        {/each}
      </td>
      <td>
        {#if snapList}
          {#each snapList as sn}
            <label>
              <input type="radio" bind:group={selectedSnapshot} value={sn} />
            {sn}
            </label><br>
          {/each}
        {/if}
      </td>
    </tr>
  </table>
  <p>Your choice:</p>
  <p>{selectedVm}  --  {selectedSnapshot}</p>

</div>
