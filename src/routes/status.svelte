<script>
  const freeVm = [
    "111111111111",
    "2222222222222",
    "3333333333333333",
    "4444444444444",
    "5555555555555"
  ];
  const busyVm = ["3333333333333333", "4444444444444", "5555555555555"];
</script>

<style>
  table {
    border: 1px solid;
  }
  td,
  th {
    padding-left: 5em;
    text-align: left;
    vertical-align: top;
  }
  .layer {
    width: 80%;
    margin: 0 auto;
  }
  h2 {
    text-align: center;
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
