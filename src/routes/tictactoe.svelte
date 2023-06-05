<script lang="ts">
	import { Modal, modalStore } from '@skeletonlabs/skeleton';
	import type { ModalSettings, ModalComponent } from '@skeletonlabs/skeleton';

	let buttons = new Array(9).fill(null);
	let result = null;
	let xWinsCounter = 0;
	let oWinsCounter = 0;
	let drawCounter = 0;
	let turn = 'X';
	const winCombinations = [
		//rows
		[0, 1, 2],
		[3, 4, 5],
		[6, 7, 8],
		//columns
		[0, 3, 6],
		[1, 4, 7],
		[2, 5, 8],
		//diagonals
		[0, 4, 8],
		[2, 4, 6]
	];

	function resetGame() {
		buttons = new Array(9).fill(null);
		result = null;
		turn = 'X';
	}

	function setValue(i) {
		if (buttons[i] === null) {
			buttons[i] = turn;
			buttons = [...buttons];
			turn = turn == 'X' ? 'O' : 'X';
			checkWinner();
		}

		function checkWinner() {
			for (let i = 0; i < winCombinations.length; i++) {
				if (buttons[winCombinations[i][0]] != null) {
					if (
						buttons[winCombinations[i][0]] == buttons[winCombinations[i][1]] &&
						buttons[winCombinations[i][1]] == buttons[winCombinations[i][2]]
					) {
						if (buttons[winCombinations[i][0]] == 'X') {
							result = 'X';
							turn = '';
							xWinsCounter++;
							const modal: ModalSettings = {
								type: 'alert',
								title: 'The winner is X!'
							};
							modalStore.trigger(modal);
						} else if (buttons[winCombinations[i][0]] == 'O') {
							result = 'O';
							turn = '';
							oWinsCounter++;
							const modal: ModalSettings = {
								type: 'alert',
								title: 'The winner is O!'
							};
							modalStore.trigger(modal);
						}
						break;
					} else if (!buttons.includes(null)) {
						result = 'Draw';
						turn = '';
						drawCounter++;
						const modal: ModalSettings = {
							type: 'alert',
							title: 'Draw!'
						};
						modalStore.trigger(modal);
						break;
					}
				}
			}
		}
	}
</script>

<Modal />

<span class="text-xl font-semibold m-5">
	X wins: {xWinsCounter} | O wins: {oWinsCounter} | Draws: {drawCounter}
</span>

{#if !result}
	<div class="grid grid-cols-3 grid-row-3">
		{#each buttons as button, i}
			<button
				class="w-20 h-20 m-2 p-2 btn-icon variant-glass-surface font-semibold"
				on:click={() => {
					setValue(i);
				}}
			>
				{button ? button : ''}
			</button>
		{/each}
	</div>
{:else}
	<div class="grid grid-cols-3 grid-row-3">
		{#each buttons as button, i}
			<button class="w-20 h-20 m-2 p-2 btn-icon variant-glass-surface">
				{button ? button : ''}
			</button>
		{/each}
	</div>
	<div class="m-5">
		<button
			class="btn-lg variant-glass-secondary rounded-xl hover:variant-glass-primary hover:duration-300 focus:scale-95 focus:duration-100"
			on:click={() => {
				resetGame();
			}}
		>
			Reset!
		</button>
	</div>
{/if}

{#if turn == 'X'}
	<span class="text-xl text-primary-500 font-semibold m-5 "> X turn </span>
{:else if turn == 'O'}
	<span class="text-xl text-secondary-500 font-semibold m-5"> O turn </span>
{/if}
