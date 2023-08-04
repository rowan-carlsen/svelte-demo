<script>
	import { crossfade } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	const [send, receive] = crossfade({
		duration: (d) => Math.sqrt(d * 200),
		fallback() {
			return {
				duration: 600,
				easing: quintOut,
				css: (t) => `
				transform: scale(${t});
				opacity: ${t}
			`
			};
		}
	});
	let name = 'World',
		items = [
			{
				label: 'Do laundry',
				done: false
			},
			{
				label: 'Brush teeth',
				done: true
			},
			{
				label: 'Plot world domination',
				done: false
			},
			{
				label: 'Clean floors',
				done: false
			},
			{
				label: 'Buy groceries',
				done: false
			},
			{
				label: 'Call Grandma',
				done: false
			}
		];
	function check(item) {
		item.done = !item.done;
		items = [...items.filter((i) => i !== item), item];
	}
</script>

<main>
	<h1>Hello {name}!</h1>
	<h2>"A" Detector: {name.includes('A') || name.includes('a') ? 'Found' : 'Not found'}</h2>
	<input bind:value={name} />
	<div id="list-holder">
		<ul class="list" id="todo-list">
			{#each items.filter((i) => !i.done) as item (item.label)}
				<li in:receive={{ key: item.label }} out:send={{ key: item.label }}>
					<button type="button" on:click={() => check(item)}> {item.label}</button>
				</li>
			{/each}
		</ul>
		<ul class="list" id="completed-list">
			{#each items.filter((i) => i.done) as item (item.label)}
				<li in:receive={{ key: item.label }} out:send={{ key: item.label }}>
					<button type="button" on:click={() => check(item)}> {item.label}</button>
				</li>
			{/each}
		</ul>
	</div>
</main>

<style>
	h1,
	h2 {
		text-align: center;
	}
	input {
		width: 10em;
		margin: 0 auto;
		display: block;
		font-size: 1rem;
	}
	#list-holder {
		display: grid;
		gap: 1em;
		grid-template-columns: 1fr 1fr;
		width: max-content;
		margin: 0 auto;
	}
	ul {
		list-style-type: none;
		padding: 0;
	}
	li {
		border: 1px solid white;
	}
	button {
		font-family: inherit;
		font-size: 1rem;
		padding: 0.5em;
		background: none;
		border: none;
		color: inherit;
		cursor: pointer;
		width: 100%;
		text-align-last: left;
	}
</style>
