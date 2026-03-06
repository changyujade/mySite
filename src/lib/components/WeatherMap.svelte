<script>
  import { DefaultMarker, MapLibre } from "svelte-maplibre";

  let { lon, lat, zoom = 10 } = $props();
</script>

<MapLibre
  center={[lon, lat]}
  {zoom}
  class="h-[400px] w-full rounded-lg"
  style="https://basemaps.cartocdn.com/gl/voyager-gl-style/style.json"
>
  <DefaultMarker lngLat={[lon, lat]} />
</MapLibre>
