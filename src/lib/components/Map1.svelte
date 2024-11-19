<script lang="ts">
	import MapView from '@arcgis/core/views/MapView';
	import '@arcgis/core/assets/esri/themes/light/main.css';

	let mapText: string = $state('');

	const createMapDiv = (mapDiv: HTMLDivElement) => {
		const view = new MapView({
			container: mapDiv,
			map: {
				basemap: 'gray'
			},
			zoom: 12,
			center: [-123.3700367, 48.4201456]
		});

		view.watch('center', (center) => {
			let { longitude, latitude } = center;
            let zoomLevel = view.zoom;
			mapText = `Lon/Lat: ${longitude.toFixed(3)}, ${latitude.toFixed(3)} | Zoom: ${zoomLevel.toFixed(0)}`;
		});
	};
</script>

<main>
	<div class="flex h-screen flex-col">
		<div class="flex-1">
			<div class="view" use:createMapDiv></div>
		</div>

		<div class="flex-none">
			{#if mapText}
				<p class="flex justify-center text-2xl font-bold">{mapText}</p>
			{/if}
		</div>
	</div>
</main>

<style>
	.view {
		height: 100%;
	}
</style>
