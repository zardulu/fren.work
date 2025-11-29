<script lang="ts">
	import { onMount } from 'svelte';

	function optimizedBase(src: string): string {
		return src.replace('/pepes/', '/pepes_optimized/').replace('.png', '');
	}

	const pepeImagesDesktop = [
		{ src: '/pepes/pepe1.png', top: '8%', left: '20%', rotate: -10, width: 200 },
		{ src: '/pepes/pepe2.png', top: '10%', left: '78%', rotate: 8, width: 250 },
		{ src: '/pepes/pepe3.png', top: '65%', left: '10%', rotate: 6, width: 250 },
		{ src: '/pepes/pepe4.png', top: '40%', left: '72%', rotate: -6, width: 250 },
		{ src: '/pepes/pepe5.png', top: '30%', left: '5%', rotate: 12, width: 250 },
		{ src: '/pepes/pepe6.png', top: '65%', left: '80%', rotate: -12, width: 250 },
	];

	const pepeImagesMobile = [
		{ src: '/pepes/pepe1.png', top: '5%', left: '5%', rotate: -10, width: 120 },
		{ src: '/pepes/pepe2.png', top: '8%', left: '70%', rotate: 8, width: 140 },
		{ src: '/pepes/pepe3.png', top: '70%', left: '6%', rotate: 6, width: 140 },
		{ src: '/pepes/pepe4.png', top: '42%', left: '72%', rotate: -6, width: 140 },
		{ src: '/pepes/pepe5.png', top: '28%', left: '3%', rotate: 12, width: 130 },
		{ src: '/pepes/pepe6.png', top: '74%', left: '75%', rotate: -12, width: 140 },
	];

	let isMobile = $state(false);
	let pepeImages = $derived(isMobile ? pepeImagesMobile : pepeImagesDesktop);

	onMount(() => {
		if (typeof window !== 'undefined') {
			const mq = window.matchMedia('(max-width: 768px)');
			const update = () => (isMobile = mq.matches);
			mq.addEventListener?.('change', update);
			update();
			return () => mq.removeEventListener?.('change', update);
		}
	});
</script>

<div class="pointer-events-none fixed inset-0 z-0 overflow-hidden">
	{#each pepeImages as img, i (img.src)}
		<img
			src={`${optimizedBase(img.src)}-256.png`}
			srcset={`${optimizedBase(img.src)}-256.png 256w, ${optimizedBase(img.src)}-512.png 512w`}
			sizes={`${img.width}px`}
			alt="Pepe"
			loading="lazy"
			decoding="async"
			fetchpriority="low"
			width={img.width}
			class="absolute select-none floating-frog-{i}"
			style={`top:${img.top};left:${img.left};--base-rotate:${img.rotate}deg;width:${img.width}px;`}
		/>
	{/each}
</div>

<style>
	@keyframes float0 {
		0%, 100% { transform: rotate(var(--base-rotate)) translateY(0px) translateX(0px); }
		33% { transform: rotate(calc(var(--base-rotate) + 4deg)) translateY(-14px) translateX(8px); }
		66% { transform: rotate(calc(var(--base-rotate) - 3deg)) translateY(-8px) translateX(-5px); }
	}
	@keyframes float1 {
		0%, 100% { transform: rotate(var(--base-rotate)) translateY(0px) translateX(0px); }
		25% { transform: rotate(calc(var(--base-rotate) - 5deg)) translateY(-10px) translateX(-6px); }
		50% { transform: rotate(calc(var(--base-rotate) + 3deg)) translateY(-18px) translateX(4px); }
		75% { transform: rotate(calc(var(--base-rotate) - 2deg)) translateY(-6px) translateX(-2px); }
	}
	@keyframes float2 {
		0%, 100% { transform: rotate(var(--base-rotate)) translateY(0px) translateX(0px); }
		20% { transform: rotate(calc(var(--base-rotate) + 6deg)) translateY(-12px) translateX(10px); }
		50% { transform: rotate(calc(var(--base-rotate) - 4deg)) translateY(-20px) translateX(-8px); }
		80% { transform: rotate(calc(var(--base-rotate) + 2deg)) translateY(-5px) translateX(3px); }
	}
	@keyframes float3 {
		0%, 100% { transform: rotate(var(--base-rotate)) translateY(0px) translateX(0px); }
		30% { transform: rotate(calc(var(--base-rotate) - 6deg)) translateY(-16px) translateX(-10px); }
		60% { transform: rotate(calc(var(--base-rotate) + 5deg)) translateY(-8px) translateX(7px); }
	}
	@keyframes float4 {
		0%, 100% { transform: rotate(var(--base-rotate)) translateY(0px) translateX(0px); }
		15% { transform: rotate(calc(var(--base-rotate) + 3deg)) translateY(-8px) translateX(5px); }
		45% { transform: rotate(calc(var(--base-rotate) - 5deg)) translateY(-22px) translateX(-6px); }
		70% { transform: rotate(calc(var(--base-rotate) + 4deg)) translateY(-12px) translateX(8px); }
	}
	@keyframes float5 {
		0%, 100% { transform: rotate(var(--base-rotate)) translateY(0px) translateX(0px); }
		40% { transform: rotate(calc(var(--base-rotate) - 4deg)) translateY(-18px) translateX(-12px); }
		70% { transform: rotate(calc(var(--base-rotate) + 6deg)) translateY(-6px) translateX(6px); }
	}

	:global(.floating-frog-0) { animation: float0 10s ease-in-out infinite; }
	:global(.floating-frog-1) { animation: float1 15s ease-in-out infinite; }
	:global(.floating-frog-2) { animation: float2 15s ease-in-out infinite; }
	:global(.floating-frog-3) { animation: float3 20s ease-in-out infinite; }
	:global(.floating-frog-4) { animation: float4 12s ease-in-out infinite; }
	:global(.floating-frog-5) { animation: float5 18s ease-in-out infinite; }

	@media (prefers-reduced-motion: reduce) {
		:global(.floating-frog-0),
		:global(.floating-frog-1),
		:global(.floating-frog-2),
		:global(.floating-frog-3),
		:global(.floating-frog-4),
		:global(.floating-frog-5) {
			animation: none;
		}
	}
</style>