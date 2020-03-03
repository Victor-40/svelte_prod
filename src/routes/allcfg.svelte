<script>
  import axios from "axios";
  import { onMount } from "svelte";

  const path = "http://rum-cherezov-dt:5000/api/allcfg";

  let freeVm = [];
  let busyVm = [];
  let allCfg = {};
  let selectedCfg1 = {};
  let selectedCfg2 = {};
  let selectedKeys = [];
  let winClear = 'Unselect all'
  let langClear = 'Clear all'

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
    return (
      checkedWin.includes(
        it
          .split(" ")
          .slice(0, 2)
          .join(" ")
      ) && checkedLang.includes(allCfg[it]["lang"])
    );
  }

  function showSelected() {
    selectedCfg1 = {};
    selectedCfg2 = {};
    selectedKeys = Object.keys(allCfg).filter(fil);

    for (let key of selectedKeys) {
      if (selectedKeys.indexOf(key) % 2 == 0) {
        selectedCfg1[key] = allCfg[key];
      } else {
        selectedCfg2[key] = allCfg[key];
      }
    }
  }
  function togllWin() {
    if (winClear == 'Select all') {
      winClear = 'Unselect all';
      checkedWin = ["Windows 10", "Windows 7", "Windows 8"];
      // checkedWin = checkedWin;
    }
    else {
      winClear = 'Select all';
      checkedWin = [];
      // checkedWin = checkedWin;
    }
  }
  function togllLang() {
    if (langClear == 'Select all') {
      langClear = 'Unselect all';
      checkedLang = [
        "English",
        "Chinese",
        "French",
        "German",
        "Italian",
        "Japanese",
        "Russian",
        "Turkish"
      ];
      // checkedWin = checkedWin;
    }
    else {
      langClear = 'Select all';
      checkedLang = [];
      // checkedWin = checkedWin;
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
        <button on:click={togllWin}>{winClear}</button>
        <br /><br> 

        {#each allWin as win}
          <label>
            <input type="checkbox" bind:group={checkedWin} value={win} />
            {win}
          </label>
          <br />
        {/each}
      </td>
      <td>
        <button on:click={togllLang}>{langClear}</button>
        <br /><br> 

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
  <table>
    <tr>
      <td>
        {#each Object.keys(selectedCfg1) as item}
          <p class="un">{item}</p>
          <!-- <p>{allCfg[item]}</p> -->
          <ul>
            {#each selectedCfg1[item]['snap'] as snap}
              <li>{snap}</li>
            {/each}
          </ul>
        {/each}
      </td>
      <td>
        {#each Object.keys(selectedCfg2) as item}
          <p class="un">{item}</p>
          <!-- <p>{allCfg[item]}</p> -->
          <ul>
            {#each selectedCfg2[item]['snap'] as snap}
              <li>{snap}</li>
            {/each}
          </ul>
        {/each}
      </td>
    </tr>
  </table>

</div>
