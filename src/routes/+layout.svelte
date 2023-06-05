<script lang="ts">
	// The ordering of these imports is critical to your app working properly
	import '@skeletonlabs/skeleton/themes/theme-rocket.css';
	// If you have source.organizeImports set to true in VSCode, then it will auto change this ordering
	import '@skeletonlabs/skeleton/styles/skeleton.css';
	// Most of your app wide CSS should be put in this file
	import '../app.postcss';
	import { AppShell, AppBar } from '@skeletonlabs/skeleton';
	import { LightSwitch } from '@skeletonlabs/skeleton';

	import { Drawer, drawerStore } from '@skeletonlabs/skeleton';
	import type { DrawerSettings } from '@skeletonlabs/skeleton';

	function instruction() {
		const drawerSettings: DrawerSettings = {
			id: 'example-3',
			// Provide your property overrides:
			bgDrawer: 'variant-glass-surface text-white',
			bgBackdrop: 'bg-gradient-to-tr from-surface-500/50 via-secondary-500/50 to-primary-500/50',
			width: 'w-[280px] md:w-[480px]',
			padding: 'p-4',
			rounded: 'rounded-3xl'
		};
		drawerStore.open(drawerSettings);
	}
</script>

<!-- App Shell -->
<svelte:head>
	<title>TicTacToe</title>
	<meta name="description" content="TicTacToe" />
</svelte:head>

<Drawer>
	<div class="space-y-10 text-center p-10">
		<h2 class="h2">How to play?</h2>
		<div class="text-left">
			<p>The game is played on a grid of 3x3.</p><br>
			<p>Two players participate, one using "X" and the other using "O".</p><br>
			<p>The first player places their symbol (X or O) on an empty square of the grid.</p><br>
			<p>The second player then places their symbol on another empty square.</p><br>
			<p>Players take turns placing their symbols on empty squares until the grid is full or one player wins.</p><br>
			<p>A player wins by getting three of their symbols in a row horizontally, vertically, or diagonally.</p><br>
			<p>If the grid is full and no player has won, the game is a draw.</p><br>
		</div>
	</div>
</Drawer>

<AppShell>
	<svelte:fragment slot="header">
		<AppBar>
			<svelte:fragment slot="lead">
				<strong class="text-xl">TicTacToe</strong>
			</svelte:fragment>
			<svelte:fragment slot="trail">
				<button class="btn btn-sm variant-ghost-surface" on:click={() => {
					instruction();
				}}>
					How to play
				</button>
				
				<LightSwitch />
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>
	<slot />
</AppShell>
