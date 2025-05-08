<script>
	import {
		GithubIcon,
		LinkedinIcon,
		OpenInNewIcon,
		RedditIcon
	} from "$lib/icons"
	import { Button, Card, getThemeConfig, HoverFollower } from "@dxdns/feflow"
	import styles from "./home.module.css"

	const theme = $derived(getThemeConfig())
</script>

<header>
	<a href="/">
		<h3>Jhon Doe</h3>
	</a>
	<p class="text-muted">Full Stack Developer at TechSolutions</p>
	<div class="social">
		<a href="https://linkedin.com/in/dxdns" target="_blank">
			<LinkedinIcon fill={theme.colorText} />
		</a>
		<a href="https://github.com/dxdns" target="_blank">
			<GithubIcon fill={theme.colorText} />
		</a>
		<a href="https://reddit.com/user/dxdns_dev" target="_blank">
			<RedditIcon fill={theme.colorText} />
		</a>
	</div>
</header>

<section class={styles.projects} id="projects">
	<h2>Projects</h2>
	<div class={styles.content}>
		<a href="/">
			<Card class={styles.card}>
				<h4>TaskMaster</h4>
				<p class="text-muted">
					A project management tool for teams to collaborate on tasks and track
					progress with an intuitive interface.
				</p>
			</Card>
		</a>
		<a href="/">
			<Card class={styles.card}>
				<h4>ChatWave</h4>
				<p class="text-muted">
					A real-time chat application with voice and video integration, built
					with WebSockets and React.
				</p>
			</Card>
		</a>
	</div>
	<Button
		onclick={() => {
			window.open("https://github.com/dxdns?tab=repositories", "_blank")
		}}
	>
		<GithubIcon />
		See all projects
	</Button>
</section>

<section class={styles.workExperience} id="work-experience">
	<h2>Work Experience</h2>
	<Card>
		<div class={styles.cardContent}>
			<div>
				<h4>Lead Developer</h4>
				<p class="text-muted">TechSolutions Inc.</p>
			</div>
			<span class="text-muted">2022 - Present</span>
		</div>
	</Card>
</section>

<section class={styles.blog} id="blog">
	<h2>Blog</h2>
	<HoverFollower>
		<a href="/">
			<Card class={styles.card}>
				<h4>The Future of Full Stack Development: Trends to Watch</h4>
				<p class="text-muted">
					Exploring emerging technologies and practices that will shape the
					future of full stack development.
				</p>
			</Card>
		</a>
		<a href="/">
			<Card class={styles.card}>
				<h4>My Journey to Becoming a Software Engineer</h4>
				<p class="text-muted">
					From a beginner to a full stack developer, I share my personal journey
					and the lessons learned along the way.
				</p>
			</Card>
		</a>
	</HoverFollower>
	<Button>
		See more posts
		<OpenInNewIcon height="14px" width="14px" />
	</Button>
</section>

<style>
	a::after {
		all: unset;
	}
	
	.social {
		display: flex;
		gap: 1rem;
		align-items: center;
		padding: 1rem 0;
	}
</style>
