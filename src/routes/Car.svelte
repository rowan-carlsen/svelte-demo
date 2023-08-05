<script>
	export let speed = 1;
</script>

<div id="road" style="animation-duration: {0.5 / speed}s;">
	<div id="car" />
</div>

<style>
	#road {
		background-color: black;
		background-image: linear-gradient(to right, transparent 50%, black 50%),
			linear-gradient(to bottom, black 48.5%, yellow 48.5%, yellow 51.5%, black 51.5%);
		background-size: 100px 100%;
		background-position: 0 0;
		background-repeat: repeat-x;
		position: relative;
		margin: 0 auto;
		width: 80vw;
		height: 20vw;
		animation: drive 0.5s linear infinite;
	}
	#car {
		position: absolute;
		height: 35%;
		width: 20%;
		background-color: red;
		border-radius: 20px;
		bottom: 5%;
		left: 10%;
		background-image: linear-gradient(
				to bottom,
				transparent 10%,
				black 10%,
				black 90%,
				transparent 90%
			),
			conic-gradient(white 0deg, white 90deg, transparent 90deg),
			conic-gradient(transparent 90deg, white 90deg, white 180deg, transparent 180deg);
		background-repeat: no-repeat;
		background-size: 30% 100%, 20% 30%, 20% 30%;
		background-position: 82% 0, 100% 0, 100% 100%;
		animation: steer 2s infinite ease-in-out;
		transform: translateY(10%);
	}
	@keyframes drive {
		to {
			background-position: -100px 0;
		}
	}
	@keyframes steer {
		50% {
			transform: translateY(-10%);
		}
		100% {
			transform: translateY(10%);
		}
	}
</style>
