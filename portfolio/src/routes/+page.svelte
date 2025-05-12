<script lang="ts">
	import {
		GithubIcon,
		LinkedinIcon,
		OpenInNewIcon,
		RedditIcon
	} from "$lib/icons"
	import {
		Actions,
		Avatar,
		Button,
		Card,
		CustomLink,
		HoverFollower
	} from "@dxdns/feflow"
	import type { PageData } from "./$types"

	let { data }: { data: PageData } = $props()
</script>

<svelte:head>
	<title>{data.title} - portfolio demo example</title>
	<meta
		name="description"
		content="feflow svelte components ui - portfolio demo example"
	/>
</svelte:head>

<section id="about">
	<h2>About</h2>
</section>

<section id="projects">
	<h2>Projects</h2>
	<div class="projectsContent">
		<a href="/">
			<Card style="min-height: 250px; max-height: 250px;">
				<h4>TaskMaster</h4>
				<p class="text-muted">
					A project management tool for teams to collaborate on tasks and track
					progress with an intuitive interface.
				</p>
			</Card>
		</a>
		<a href="/">
			<Card style="min-height: 250px; max-height: 250px;">
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

<section id="work-experience">
	<h2>Work Experience</h2>
	<div use:Actions.glowOnHoverAction>
		<Card>
			<div class="workExperienceContent">
				<div>
					<h4>Lead Developer</h4>
					<p class="text-muted">TechSolutions Inc.</p>
				</div>
				<p class="text-muted">2022 - Present</p>
			</div>
		</Card>
	</div>
</section>

<section id="blog">
	<h2>Blog</h2>
	<HoverFollower>
		<a href="/">
			<Card>
				<h4>The Future of Full Stack Development: Trends to Watch</h4>
				<p class="text-muted">
					Exploring emerging technologies and practices that will shape the
					future of full stack development.
				</p>
			</Card>
		</a>
		<a href="/">
			<Card>
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

<section id="connect">
	<h2>Connect</h2>
	<p class="text-muted">
		Feel free to contact me at
		<CustomLink pathname="mailto:dxdns@hotmail.com" hoverUnderline="center">
			dxdns@hotmail.com
		</CustomLink>
	</p>
</section>

<style>
	section {
		text-align: center;
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		justify-content: center;
		scroll-snap-align: center;
		padding: 40px;
		box-sizing: border-box;
	}

	p,
	h2 {
		text-align: left;
	}

	.projectsContent {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(210px, 1fr));
		gap: 1rem;
		padding: 1rem 0;
	}

	.workExperienceContent {
		display: flex;
		justify-content: space-between;
		align-items: center;
		gap: 1rem;
	}

	#connect {
		line-height: 3;
	}

	@media screen and (max-width: 425px) {
		.projectsContent {
			gap: 0;
		}
	}
</style>
