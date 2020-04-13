<script>
  import axios from "axios";
  import { onMount } from "svelte";

  const path = "http://rum-cherezov-dt:5000/api/cfg";

  let freeVm = [];
  let busyVm = [];

  function test_cfg(c) {
    // console.log(c);
    for (let key in c) {
      if (c[key].status === "free") {
        freeVm.push(key.replace(".vmx", ""));
        freeVm = freeVm;
      } else {
        busyVm.push(key.replace(".vmx", ""));
        busyVm = busyVm;
      }
    }
  }

  // onMount(getTodos());

  // function getTodos() {
  axios.get(path).then(response => {
    test_cfg(response.data);
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
  ul {
    list-style: none;
    padding-left: 0;
    /* vertical-align: top; */
  }
  .busy {
    color: red;
  }
  .wrapper {
    margin-top: 30px;
    display: grid;
    grid-template-columns: 250px 250px;
    grid-column-gap: 30px;
    justify-content: center;
  }
  .card {
    padding: 10px;
    /* background-color: aquamarine; */
  }
</style>

<svelte:head>
  <title>About</title>
</svelte:head>

<h2>Virtual machines status</h2>
  <div class="wrapper">
    <div class="card">
    <h3>Free VM(s)</h3>
       <ul>
          {#each freeVm as free}
            <li>{free}</li>
          {/each}
        </ul>
    </div>
    <div class="card">
    <h3>Busy VM(s)</h3>
      <ul class="busy">
          {#each busyVm as busy}
            <li>{busy}</li>
          {/each}
        </ul>
    </div>
  </div>

