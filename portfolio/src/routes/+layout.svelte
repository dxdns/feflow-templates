<script lang="ts">
	import { onMount, type Snippet } from "svelte"
	import {
		Avatar,
		Button,
		Drawer,
		getThemeConfig,
		themeMode,
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
	import styles from "./layout.module.css"

	let { children }: { children: Snippet } = $props()

	const { getThemeMode, toggleThemeMode } = themeMode()

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
	<div class={styles.container}>
		<aside class={styles.sidebar}>
			<Drawer class={styles.drawer} variant="permanent">
				{#snippet header()}
					<div class={styles.header}>
						<Avatar src={avatar} width="80px" height="80px" />
						<div>
							<h4>Diógenes Rodrigues</h4>
							<small class="text-muted">Full Stack Developer</small>
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
					<footer class={styles.footer}>
						<div class={styles.social}>
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

		<main class={styles.content}>
			{@render children()}
		</main>
	</div>
</ThemeProvider>
