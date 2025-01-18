<script lang="ts">
	import Button from '$lib/components/ui/button/button.svelte';
	import { Github, Pen } from 'lucide-svelte';
	import { onMount } from 'svelte';

	const m = [
		'Magical',
		'Massive',
		'Magnificent',
		'Majestic',
		'Marvelous',
		'Mighty',
		'Modern',
		'Mysterious',
		'Mythical',
		'Micro',
		'Mixed',
		'Minty'
	];

	const n = ['Nut', 'Nuts', 'Nutty', 'Number', 'Nutsack', 'Nutcase'
	];

	const t = [
		'Transformer',
		'Tree',
		'Terminal',
		'Transport',
		'Terminator',
		'Teleporter',
		'Tool',
		'Tunnel',
		'Thunder',
		'Temple'
	];

	let currentM = m[0];
	let currentN = n[0];
	let currentT = t[0];

	const switchWord = async () => {
		const r = Math.random() * 3;
		const next = m[Math.floor(Math.random() * m.length)];
			currentM = scramble(next);
			for (let i = 0; i <= next.length; i++) {
				await new Promise(r => setTimeout(r, 75));
				currentM = unscrambleOne(next ,i);
			}
		if (r < 1) {
			const next = m[Math.floor(Math.random() * m.length)];
			currentM = scramble(next);
			for (let i = 0; i <= next.length; i++) {
				await new Promise(r => setTimeout(r, 75));
				currentM = unscrambleOne(next ,i);
			}
		} else if (r < 2) {
			const next = n[Math.floor(Math.random() * n.length)];
			currentN = scramble(next);
			for (let i = 0; i <= next.length; i++) {
				await new Promise(r => setTimeout(r, 75));
				currentN = unscrambleOne(next ,i);
			}
		} else {
			const next = t[Math.floor(Math.random() * t.length)];
			currentT = scramble(next);
			for (let i = 0; i <= next.length; i++) {
				await new Promise(r => setTimeout(r, 75));
				currentT = unscrambleOne(next ,i);
			}
		}
	};

	const randomString = (l: number) => {
		const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789*%&#!$@';
  
		let r = ''
		while (l--)
			r+=chars[Math.ceil(Math.random() * chars.length-1)]
		return r;
	};
	const scramble = (text: string) => {
		return randomString(text.length);
	};

	function unscrambleOne(original: string, iteration: number) {
		let solved = original.slice(0, iteration);
 		return solved + randomString(original.length-iteration);
	}

	onMount(() => {
		const interval = setInterval(() => switchWord(), 5000);
		return () => {
			clearInterval(interval);
		};
	});
</script>

<div
	class=" flex flex-col gap-5 h-64 w-96 items-center justify-center rounded-lg border border-white bg-black bg-opacity-40 backdrop-blur-sm"
>
	<div class="grid w-80 grid-cols-3">
		<p class="flex items-center justify-center text-7xl font-bold">M</p>
		<p class="flex items-center justify-center text-7xl font-bold">N</p>
		<p class="flex items-center justify-center text-7xl font-bold">T</p>
		<p class="flex w-full items-center justify-center">{currentM}</p>
		<p class="flex w-full items-center justify-center">{currentN}</p>
		<p class="flex w-full items-center justify-center">{currentT}</p>
	</div>
	<p> 
		<Button class='rounded-full' href='https://github.com/gandlafbtc/mint'>
			<Github></Github>
		</Button>
	</p>
</div>
