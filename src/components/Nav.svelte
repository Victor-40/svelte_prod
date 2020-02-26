<script>
	export let segment;
</script>

<style>
	nav {
		border-bottom: 1px solid rgba(255,62,0,0.1);
		font-weight: 300;
		padding: 0 1em;
		margin-bottom: 10px;
	}

	ul {
		margin: 0;
		padding: 0;
	}

	/* clearfix */
	ul::after {
		content: '';
		display: block;
		clear: both;
	}

	li {
		display: block;
		float: left;
	}

	.selected {
		position: relative;
		display: inline-block;
	}

	.selected::after {
		position: absolute;
		content: '';
		width: calc(100% - 1em);
		height: 2px;
		background-color: rgb(255,62,0);
		display: block;
		bottom: -1px;
	}

	a {
		text-decoration: none;
		padding: 1em 0.5em;
		display: block;
	}
</style>

<nav>
	<ul>
		<li><a class:selected='{segment === undefined}' href='.'>Home</a></li>
		<li><a class:selected='{segment === "allcfg"}' href='allcfg'>All_configs</a></li>
		<li><a class:selected='{segment === "status"}' href='status'>Status_VM</a></li>
		<li><a class:selected='{segment === "find"}' href='find'>Start_Testset</a></li>
		<li><a class:selected='{segment === "startclear"}' href='startclear'>Start_clear_VM</a></li>

		<!-- for the blog link, we're using rel=prefetch so that Sapper prefetches
		     the blog data when we hover over the link or tap it on a touchscreen -->
		<!-- <li><a rel=prefetch class:selected='{segment === "blog"}' href='blog'>blog</a></li> -->
	</ul>
</nav>
