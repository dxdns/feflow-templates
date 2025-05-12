<script lang="ts">
	import { onMount, type Snippet } from "svelte"
	import {
		Avatar,
		Button,
		Drawer,
		getThemeConfig,
		themeModeUtil,
		ThemeProvider,
		type ThemeModeType
	} from "@dxdns/feflow"
	import "./globals.css"
	import {
		DarkModeIcon,
		GithubIcon,
		LightModeIcon,
		LinkedinIcon,
		RedditIcon
	} from "$lib/icons"
	import avatar from "$lib/assets/avatar.jpeg"

	let { children }: { children: Snippet } = $props()

	const { getThemeMode, toggleThemeMode } = themeModeUtil()

	let activeThemeMode: ThemeModeType = $state("dark")

	onMount(() => {
		const _themeMode = getThemeMode()
		activeThemeMode = _themeMode
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
		<aside>
			<Drawer variant="permanent">
				{#snippet header()}
					<div
						style="display: flex; flex-direction: column; align-items: center; gap: .5rem; text-align: center;"
					>
						<Avatar src={avatar} />
						<div>
							<h4>Diógenes Rodrigues</h4>
							<p class="text-muted">Full Stack Developer at TechSolutions</p>
						</div>
					</div>
				{/snippet}
				{#snippet content()}
					<nav>
						<ul style="padding: 2rem; line-height: 2;">
							<li><a href="#about">About</a></li>
							<li><a href="#projects">Projects</a></li>
							<li><a href="#work-experience">Experience</a></li>
							<li><a href="#blog">Blog</a></li>
							<li><a href="#connect">Connect</a></li>
						</ul>
					</nav>
					<footer class="footer">
						<div class="social">
							<a href="https://linkedin.com/in/dxdns" target="_blank">
								<LinkedinIcon />
							</a>
							<a href="https://github.com/dxdns" target="_blank">
								<GithubIcon />
							</a>
							<a href="https://reddit.com/user/dxdns_dev" target="_blank">
								<RedditIcon />
							</a>
						</div>
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
				{/snippet}
			</Drawer>
		</aside>

		<main>
			{@render children()}
		</main>
	</div>
</ThemeProvider>

<style>
	.container {
		display: grid;
		grid-template-columns: auto auto;
		grid-template-areas: "sidebar main";
	}

	aside {
		grid-area: sidebar;
	}

	main {
		grid-area: main;
		margin: 3rem auto;
	}

	.social {
		display: flex;
		gap: 0.5rem;
		align-items: center;
	}

	.footer {
		margin-top: 1rem;
		padding: 1rem;
		border-top: 1px solid var(--feflow-color-border);
		display: flex;
		align-items: center;
		justify-content: space-between;
		position: fixed;
		bottom: 0;
		right: 0;
		left: 0;
	}
</style>
