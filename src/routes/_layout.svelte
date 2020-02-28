<script>
  // import Nav from '../components/Nav.svelte';
  import NavSide from "../components/NavSide.svelte";

  export let segment;
</script>

<style>
  .sidenav {
    width: 160px;
    position: fixed;
    z-index: 1;
    top: 20px;
    left: 10px;
    background: #eee;
    overflow-x: hidden;
    padding: 8px 0;
  }

  .main {
    margin-left: 170px; /* Same width as the sidebar + left position in px */
    /* font-size: 18px; Increased text to enable scrolling */
    padding: 0px 20px;
  }
</style>

<!-- <Nav {segment}/> -->

<div class="sidenav">
  <NavSide {segment} />
</div>

<div class="main">
  <slot />
</div>
