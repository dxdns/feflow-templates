<script lang="ts">
	import { onMount } from "svelte"
	import {
		Button,
		getThemeConfig,
		themeModeState,
		themeModeUtil,
		ThemeProvider,
		type ThemeModeType
	} from "@dxdns/feflow"
	import "./globals.css"
	import { DarkModeIcon, LightModeIcon } from "$lib/icons"

	let { children } = $props()

	const { getThemeMode, toggleThemeMode } = themeModeUtil()

	let activeThemeMode: ThemeModeType = $state("dark")

	function initTheme() {
		const _themeModeState = themeModeState()
		const _themeMode = getThemeMode()
		activeThemeMode = _themeMode
		_themeModeState.setThemeMode(_themeMode)
	}

	onMount(() => {
		initTheme()
	})
</script>

<svelte:head>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link
		rel="preconnect"
		href="https://fonts.gstatic.com"
		crossorigin="anonymous"
	/>
	<link
		href="https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<ThemeProvider>
	<div class="container">
		{@render children()}
		<footer class="footer">
			<span>
				<div class="text-muted">
					{@html "&copy;"}
					{new Date().getFullYear()}
					|
				</div>
				<a href="https://dxdns.dev" target="_blank">dxdns</a>
			</span>
			<Button
				variant="outlined"
				onclick={() => {
					toggleThemeMode((t) => {
						activeThemeMode = t
					})
				}}
			>
				{@const colors = getThemeConfig()}
				{#if activeThemeMode === "dark"}
					<LightModeIcon fill={colors.colorText} />
				{:else}
					<DarkModeIcon fill={colors.colorText} />
				{/if}
			</Button>
		</footer>
	</div>
</ThemeProvider>

<style>
	.container {
		padding: 3rem 0;
		width: 600px;
		margin: 0 auto;
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		justify-content: center;
		gap: 2rem;
	}

	.footer {
		margin-top: 1rem;
		padding: 1rem;
		border-top: 1px solid var(--feflow-color-border);
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.footer > span {
		display: flex;
		align-items: center;
		gap: 0.3rem;
	}

	@media (max-width: 425px) {
		.container {
			width: 80%;
		}
	}
</style>
