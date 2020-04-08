<script>
  import axios from "axios";

  let tag = "";
  let build = "";
  let subdir = "";
  let showParam = false;

  $: tag = tag.replace("git--", "");
  $: build = tag.match(/\.(\d\d\d\d)_/) ? tag.match(/\.(\d\d\d\d)_/)[1] : "";
  let checkedNames = [
    "CFW",
    "EFD.LAB",
    "EFD.NX",
    "EFD.PRO",
    "EFD.SE",
    "EFD.V5"
  ];
  let prodList = ["CFW", "EFD.LAB", "EFD.NX", "EFD.PRO", "EFD.SE", "EFD.V5"];
  let setupParams = {};
  let setupCount = 0;
  let cfgCount = 0;

  let resp_cfg = {};
  let fullCfg = [];
  // let resp

  function findSetups() {
    const path = "http://rum-cherezov-dt:5000/api/findsetups";
    showParam = true;
    setupParams.build = build;
    setupParams.tag = tag;
    setupParams.subdir = subdir;
    setupParams.products = checkedNames;

    axios.post(path, setupParams).then(response => {
      resp_cfg = response.data;
      // console.log(resp_cfg);
      resp_cfg = resp_cfg;
      setupCount = resp_cfg.length;
    });
  }

  function makeXls() {
    const path = "http://rum-cherezov-dt:5000/api/makexls";
    axios
      .post(path, resp_cfg)
      .then(res => {
        fullCfg = res.data;
        cfgCount = fullCfg.length;
      })
      .catch(error => {
        // eslint-disable-next-line
        console.error(error);
      });
  }
  function startTestset() {
    const path = "http://rum-cherezov-dt:5000/api/start_testset";
    axios
      .get(path)
      .then(response  => {
        console.log(response.data);
      });
  }
</script>


<style>
  h2 {
    text-align: center;
  }
  h3 {
    margin-top: 30px;
  }
   .btn-style {
    padding: 5px 15px;
    border-radius: 5px;
    font-weight: bold;
    color: white;
    background-color: green;
  }
</style>

<h2>Find Setups and start Testset</h2>
<h3>Input build tag</h3>
<input size="50" maxlength="50" bind:value={tag} />
<h3>Input build number</h3>
<input size="4" maxlength="4" bind:value={build} />

<h3>Select products:</h3>
{#each prodList as prod}
  <label>
    <input type="checkbox" bind:group={checkedNames} value={prod} />
    {prod}
  </label>
  <br />
{/each}

<h3>Select subdir:</h3>
<label>
  <input type="radio" bind:group={subdir} value={''} />
  \
</label>
<br />
<label>
  <input type="radio" bind:group={subdir} value={'_Internal'} />
  _Internal
</label>
<br />
<label>
  <input type="radio" bind:group={subdir} value={'_Main'} />
  _Main
</label>
<br />
<br />
<button class="btn-style" on:click={findSetups}>Find Setups</button>
<hr />

{#if showParam}
  <h2>{setupCount} setup(s) was found</h2>
  <ul>
    {#each resp_cfg as item}
      <li>{item}</li>
    {/each}
  </ul>
{/if}
<br />
{#if setupCount}
  <button class="btn-style" on:click={makeXls}>Make XLS config</button>
  <hr />
  <h2>{cfgCount} record(s) was created for Testset</h2>
{/if}

{#if cfgCount}
  <button class="btn-style" on:click={startTestset}>Start Testset</button>
{/if}

<!-- {#each fullCfg as item}
  <ul>
    <li>{item}</li>
  </ul>
{/each} -->
