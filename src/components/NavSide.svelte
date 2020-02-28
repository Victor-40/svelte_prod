<script>
  export let segment;
</script>

<style>
  a {
    padding: 6px 8px 6px 16px;
    text-decoration: none;
    font-size: 18px;
    color: #2196f3;
    display: block;
  }

  a:hover {
    color: #064579;
  }
</style>

<div>
  <a class:selected={segment === undefined} href=".">Home</a>
  <a class:selected={segment === 'allcfg'} href="allcfg">All configs</a>
  <a class:selected={segment === 'status'} href="status">Status VM</a>
  <a class:selected={segment === 'find'} href="find">Start Testset</a>
  <a class:selected={segment === 'startclear'} href="startclear">Start clear VM</a>
</div>
