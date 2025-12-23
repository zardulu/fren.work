<script lang="ts">
	import { goto } from '$app/navigation';
	import { page } from '$app/stores';

	function createBoard() {
		goto('/create-job-board');
	}
</script>

<div class="min-h-[100svh] bg-bg flex flex-col font-brutal overflow-x-hidden">
	<!-- Brutalist Navbar -->
	<nav class="bg-primary">
	</nav>

	<!-- Main content -->
	<main class="relative flex flex-1 flex-col items-center justify-center gap-6 p-4 md:p-8 overflow-hidden">
		<!-- Success message for deleted board -->
		{#if $page?.url?.searchParams?.get('deleted')}
			<div class="bg-success text-text px-8 py-4 border-3 border-border shadow-brutal-sm font-black uppercase max-w-md">
				🗑️ JOB BOARD DELETED SUCCESSFULLY.
			</div>
		{/if}
		
		<!-- Hero Section -->
		<div class="relative z-10 text-center max-w-4xl">
			<h2 class="text-3xl md:text-8xl font-black c text-text mb-6 uppercase tracking-tighter leading-none">
				WELCOME TO<br>
				<span class="bg-green-400 text-white px-4 py-2 inline-block transform shadow-brutal">FREN.WORK</span>
			</h2>
			<p class="text-brutal-lg text-text mb-12 font-bold uppercase tracking-wide max-w-2xl mx-auto">
				START HIRING FROM YOUR COMMUNITY
			</p>
			
			<button 
				class="text-text bg-teal-50 py-3 px-6 md:py-6 md:px-12 border-4 border-border font-bold text-base md:text-brutal-lg tracking-wide shadow-brutal-soft hover:bg-green-400 hover:shadow-brutal-hover hover:translate-x-1 hover:translate-y-1 cursor-pointer disabled:opacity-50 disabled:cursor-not-allowed disabled:hover:translate-x-0 disabled:hover:translate-y-0 disabled:hover:shadow-brutal-soft transition-all duration-150 rounded-brutal"
				onclick={createBoard}
			>
				+ CREATE JOB BOARD
			</button>
			<p class="text-sm md:text-brutal-sm text-green-400 mt-3 font-medium italic tracking-wide max-w-2xl mx-auto">
				No signups required!
			</p>
		</div>
	</main>

	<!-- Footer -->
	<footer class="bg-primary relative z-10">
		<div class="flex items-center justify-between p-6">
			<div class="flex gap-6">
				<a 
					href="/contact" 
					class="text-text font-bold uppercase tracking-wide hover:text-green-400 transition-colors text-sm"
				>
					CONTACT
				</a>
				<a 
					href="/privacy" 
					class="text-text font-bold uppercase tracking-wide hover:text-green-400 transition-colors text-sm"
				>
					PRIVACY
				</a>
			</div>
			<div class="text-text font-bold uppercase tracking-wide text-sm">
			</div>
		</div>
	</footer>
</div>
