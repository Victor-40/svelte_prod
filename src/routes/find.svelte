<script>
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
  
  function findSetups() {
    // alert('Q');
    showParam = true;
  }
</script>

<style>
  h2 {
    text-align: center;
  }
  h3 {
    margin-top: 30px;
  }
</style>

<h2>Find Setups</h2>
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
<br><br>
<button on:click={findSetups}>Find Setups</button>
<hr />
{#if showParam}
  <p>{checkedNames}</p>
  <p>{subdir}</p>
  <p>tag-{tag}</p>
  <p>build-{build}</p>
{/if}
