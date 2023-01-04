<script lang="ts">
	import { onMount } from 'svelte';

	let mounted: boolean;
	let aframe: any;
	let ar: any;
	$: ready = aframe && ar && mounted;

	const aframeLoaded = () => {
		console.log('aframe');
		aframe = true;
	};

	const arLoaded = () => {
		console.log('ar');
		ar = true;
	};

	onMount(() => {
		console.log('mounted');
		mounted = true;
	});

	let width = 1280;
	let height = 720;
</script>

<svelte:head>
	{#if mounted}
		<script src="https://aframe.io/releases/1.0.0/aframe.min.js" on:load={aframeLoaded}></script>
		<script
			src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"
			on:load={arLoaded}
		></script>
	{/if}
</svelte:head>

{#if ready}
	<a-scene embedded arjs>
		<a-marker preset="hiro">
			<a-entity position="0 0 0" scale="1 1 1" gltf-model="/models/crystal-model.gltf" />
		</a-marker>
		<a-entity camera />
	</a-scene>
{/if}

<style>
	:global(html, body) {
		height: 100%;
		margin: 0;
		overflow: hidden;
	}

	:global(body) {
		position: relative;
	}

	:global(.a-canvas, #arjs-video) {
		display: block;
		width: 100% !important;
		height: 100% !important;
		margin: 0 !important;
		object-fit: contain !important;
	}
</style>
