<script>
  import axios from "axios";
  import { onMount } from "svelte";

  const path = "http://localhost:5000/api/cfg";
  
  let freeVm = [];
  let busyVm = [];
  
  function test_cfg(c) {
    console.log(c);
    for (let key in c) {
      if (c[key].status === "free") {
        freeVm.push(key.replace(".vmx", ""));
        freeVm = freeVm;
      } else {
        busyVm.push(key.replace(".vmx", ""));
        busyVm = busyVm;
      }
    }
  };

// onMount(getTodos());

// function getTodos() {
axios
  .get(path)
  .then(response  => {
    test_cfg(response.data);
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
  .layer {
    width: 80%;
    margin: 0 auto;
  }
  h2 {
    text-align: center;
    margin-bottom: 30px;
  }
  ul {
    list-style: none;
    padding-left: 0;
    /* vertical-align: top; */
  }
	.busy {
		color: red;
	}
</style>

<svelte:head>
  <title>About</title>
</svelte:head>

<div>
  <h2>Virtual Machines status</h2>
  <table class="layer">
    <tr>
      <th>Free VM(s)</th>
      <th>Busy VM(s)</th>
    </tr>
    <tr>
      <td>
        <ul>
          {#each freeVm as free}
            <li>{free}</li>
          {/each}
        </ul>
      </td>

      <td>
        <ul class="busy">
          {#each busyVm as busy}
            <li>{busy}</li>
          {/each}
        </ul>
      </td>
    </tr>
  </table>
</div>
