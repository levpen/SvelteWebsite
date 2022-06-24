<script lang="ts">
	import BodyHeader from "./components/BodyHeader.svelte";
	import BodyFooter from "./components/BodyFooter.svelte";
	import BodyMain from "./components/BodyMain.svelte";
</script>

<main>
    <BodyHeader/>
	<BodyMain/>
	<BodyFooter/>
</main>

<style>
	* {
		background-image:url('../images/site-background.jpg');
		background-size: 150%;
		color: grey;
		font-family:sans-serif;
		font-size: 16px;
		line-height: 1.6em;
		margin:0;
		text-align: center;
	}
</style>