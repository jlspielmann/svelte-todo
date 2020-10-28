<script lang="ts">
	import TailWind from "./TailWind.svelte";

	export let name: string;
</script>

<TailWind />

<main>
	<h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
</main>