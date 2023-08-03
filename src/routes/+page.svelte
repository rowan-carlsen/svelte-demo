<script>
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
</script>

<main>
	<h1>Hello {name}!</h1>
	<h2>"A" Detector: {name.includes('A') || name.includes('a') ? 'Found' : 'Not found'}</h2>
	<input bind:value={name} />
	<div id="list-holder">
		<ul class="list" id="todo-list">
			{#each items.filter((i) => !i.done) as item}
				<li>
					<button
						type="button"
						on:click={() => {
							item.done = true;
							items = [...items.filter((i) => i !== item), item];
						}}
					>
						{item.label}</button
					>
				</li>
			{/each}
		</ul>
		<ul class="list" id="completed-list">
			{#each items.filter((i) => i.done) as item}
				<li>
					<button
						type="button"
						on:click={() => {
							item.done = false;
							items = [...items.filter((i) => i !== item), item];
						}}
					>
						{item.label}</button
					>
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
