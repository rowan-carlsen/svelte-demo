<script>
	import { crossfade } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import Car from './Car.svelte';
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
				task: 'Do laundry',
				done: false
			},
			{
				task: 'Brush teeth',
				done: true
			},
			{
				task: 'Plot world domination',
				done: false
			},
			{
				task: 'Clean floors',
				done: false
			},
			{
				task: 'Buy groceries',
				done: false
			},
			{
				task: 'Call Grandma',
				done: false
			}
		],
		speed = 1,
		showCar = false;
	function check(item) {
		item.done = !item.done;
		items = [...items.filter((i) => i !== item), item];
	}
</script>

<main>
	<h1>Hello {name}!</h1>
	<h2>"A" Detector: {name.includes('A') || name.includes('a') ? 'Found' : 'Not found'}</h2>
	<input type="text" bind:value={name} />
	<div id="list-holder">
		<ul class="list" id="todo-list">
			{#each items.filter((i) => !i.done) as item (item.task)}
				<li in:receive={{ key: item.label }} out:send={{ key: item.label }}>
					<label>
						<input type="checkbox" checked={item.done} on:change={check(item)} />
						{item.task}
					</label>
				</li>
			{/each}
		</ul>
		<ul class="list" id="completed-list">
			{#each items.filter((i) => i.done) as item (item.task)}
				<li in:receive={{ key: item.label }} out:send={{ key: item.label }}>
					<label>
						<input type="checkbox" checked on:change={check(item)} />
						{item.task}
					</label>
				</li>
			{/each}
		</ul>
	</div>
	{#if !showCar}
		<button on:click={() => (showCar = !showCar)} type="button">Let's Drive!</button>
	{:else}
		<label>Speed:<input type="range" min="1" max="5" bind:value={speed} /></label>
		<Car {speed} />
	{/if}
</main>

<style>
	h1,
	h2 {
		text-align: center;
	}
	input[type='text'] {
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
	label {
		padding: 0.5em;
		display: flex;
		align-items: center;
		gap: 0.5em;
		cursor: pointer;
	}
	input[type='checkbox'] {
		width: 1rem;
		height: 1rem;
	}
	button {
		font-size: 1rem;
		font-family: inherit;
		background: teal;
		cursor: pointer;
		border: 2px solid white;
		padding: 0.5em;
		display: block;
		margin: 2em auto 0 auto;
	}
</style>
