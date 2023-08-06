<script>
	import { fade, fly, slide, blur, scale } from 'svelte/transition';
	let index = 0;
</script>

<svelte:window on:click={() => index++} />
<main>
	<h1>Why Use Svelte/SvelteKit?</h1>
	<ul class:done={index > 5}>
		{#if index >= 1}
			<li in:fade class:active={index === 1}>
				<strong>Do more with less code:</strong> Development is faster and less frustrating, while easy-to-read
				syntax helps with debugging and reduces cognitive load.
			</li>
		{/if}
		{#if index >= 2}
			<li in:fly={{ x: -200 }} class:active={index === 2}>
				<strong>High performance:</strong> Much smaller package sizes are delivered to the client, so
				your pages load and run faster.
			</li>
		{/if}
		{#if index >= 3}
			<li in:slide class:active={index === 3}>
				<strong>SSR by default:</strong> Svelte can create static HTML pages, SPA's, MPA's, and everything
				in between. But the default settings produce Server-Side-Rendered pages, increasing speed even
				further with caching and fewer server requests.
			</li>
		{/if}
		{#if index >= 4}
			<li in:blur class:active={index === 4}>
				<strong>Built-in toolkit:</strong> Svelte comes bundled with standard transitions and animations
				that can be implemented with shockingly little code, as you can see here!
			</li>
		{/if}
		{#if index >= 5}
			<li in:scale class:active={index === 5}>
				<strong>Full TypeScript support...IF you want it:</strong> I don't even use TypeScript, but if
				YOU do, you'll get full intellisense and type safety within your SvelteKit projects.
			</li>
		{/if}
	</ul>
</main>

<style>
	ul {
		font-size: 1.2em;
		line-height: 1.5;
	}
	li {
		padding: 1em;
		border: 2px solid orange;
		background: orange;
		color: black;
		margin-bottom: 0.5em;
		user-select: none;
		transition: opacity 0.2s, filter 0.2s;
	}
	ul:not(.done) li:not(.active) {
		opacity: 0.5;
		filter: grayscale(1);
	}
	strong {
		font-size: 1.2em;
	}
	:global(html) {
		cursor: pointer;
	}
</style>
