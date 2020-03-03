<script>
  import axios from "axios";
  import { onMount } from "svelte";

  const path = "http://rum-cherezov-dt:5000/api/allcfg";

  let freeVm = [];
  let busyVm = [];
  let allCfg = {};
  let selectedCfg = {};

  let allWin = ["Windows 10", "Windows 7", "Windows 8"];
  let checkedWin = ["Windows 10", "Windows 7", "Windows 8"];

  let allLang = [
    "English",
    "Chinese",
    "French",
    "German",
    "Italian",
    "Japanese",
    "Russian",
    "Turkish"
  ];
  let checkedLang = [
    "English",
    "Chinese",
    "French",
    "German",
    "Italian",
    "Japanese",
    "Russian",
    "Turkish"
  ];

  function test_cfg(c) {
    allCfg = c;
    selectedCfg = c;
  }

  function fil(it) {
    return checkedWin.includes(it.split(' ').slice(0, 2).join(' ')) && checkedLang.includes(allCfg[it]["lang"]);
  } 

  function showSelected() {
    selectedCfg = {};
    let selectedKeys = Object.keys(allCfg).filter(fil);
    console.log(selectedKeys);

    for (let key of selectedKeys) {
          selectedCfg[key] = allCfg[key];
    }
  }

  // onMount(getTodos());

  // function getTodos() {
  axios.get(path).then(response => {
    test_cfg(response.data);
  });
</script>

<style>
  /* table {
    border: 1px solid;
  } */
  h2 {
    text-align: center;
    margin-bottom: 30px;
  }
  .un {
    text-decoration: underline;
  }
  td,
  th {
    padding-left: 7em;
    text-align: left;
    vertical-align: top;
  }
</style>

<svelte:head>
  <title>All cfg</title>
</svelte:head>

<div>
  <h2>All available configurations</h2>

  <table>
    <tr>
      <th>
        <h3>Windows version:</h3>
      </th>
      <th>
        <h3>Language:</h3>
      </th>
    </tr>
    <tr>
      <td>
        {#each allWin as win}
          <label>
            <input type="checkbox" bind:group={checkedWin} value={win} />
            {win}
          </label>
          <br />
        {/each}
      </td>
      <td>
        {#each allLang as lang}
          <label>
            <input type="checkbox" bind:group={checkedLang} value={lang} />
            {lang}
          </label>
          <br />
        {/each}
      </td>
    </tr>
    <tr />
  </table>

  <br />
  <button on:click={showSelected}>Show selected</button>
  <hr />

  {#each Object.keys(selectedCfg) as item}
    <p class="un">{item}</p>
    <!-- <p>{allCfg[item]}</p> -->
    <ul>
      {#each selectedCfg[item]['snap'] as snap}
        <li>{snap}</li>
      {/each}
    </ul>
  {/each}
</div>
