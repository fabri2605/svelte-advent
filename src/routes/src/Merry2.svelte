<script>
	let cookies = 0;
	let face = ':)';

	const changable = (action) => {
		switch (action) {
			case 'sum':
				cookies++;
				break;
			case 'rest':
				cookies--;
				break;
			case 'reset':
				cookies = 0;
				break;
			default:
				cookies++;
		}
		if (cookies > 5) {
			face = ';;)';
		} else if (cookies === 0) {
			face = ':(';
		} else if (cookies < 0) {
			face = ':\'(';
		} else {
			face = ':)';
		}
	};
</script>

<section>
	<h3>Santas eaten cookies dilemma!</h3>

	<div id="cookies">
		<h1>{cookies}</h1>
		<h1 id="face">{face}</h1>
	</div>
	<div>
		<button class="but" on:click={() => changable('rest')}>-</button>
		&nbsp;
		<button class="but" on:click={() => changable('sum')}>+</button>
		<button on:click={() => changable('reset')}>RESET</button>
	</div>
</section>

<style>
	section {
		text-align: center;
	}
	#cookies {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: center;
		gap: 60px;
	}
	.but {
		padding: 10px;
		width: 50px;
		height: 50px;
	}
	#face {
        display: block;
		transition: 1s;
		transform: rotate(90deg);
	}
    #face:hover{
        transform: rotate(450deg);
    }
</style>
