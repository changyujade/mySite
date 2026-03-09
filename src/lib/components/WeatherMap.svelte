<script>
  import { browser } from "$app/environment";
  import { onMount } from "svelte";
  import { DefaultMarker, MapLibre } from "svelte-maplibre";

  let { lon, lat, zoom = 10 } = $props();
  let isMounted = $state(false);

  onMount(() => {
    isMounted = true;
  });
</script>

{#if browser && isMounted}
  <MapLibre
    center={[lon, lat]}
    {zoom}
    class="h-[400px] w-full rounded-lg"
    style="https://basemaps.cartocdn.com/gl/voyager-gl-style/style.json"
  >
    <DefaultMarker lngLat={[lon, lat]} />
  </MapLibre>
{/if}
