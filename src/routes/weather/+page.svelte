<script>
  import { Button } from "$lib/components/ui/button";
  import * as Card from "$lib/components/ui/card";
  import { Input } from "$lib/components/ui/input";
  import WeatherMap from "$lib/components/WeatherMap.svelte";
  import ForeCastTable from "$lib/components/ForeCastTable.svelte";

  let city = $state("Chicago");
  let loading = $state(false);
  let errorMsg = $state("");
  let weatherData = $state(/** @type {any} */ (null));

  let mapLon = $state(-87.63); // Chicago longitude
  let mapLat = $state(41.88); // Chicago latitude
  let searchedCity = $state("Chicago");

  let avgHigh = $derived(
    weatherData?.daily?.temperature_2m_max?.length
      ? Math.round(
          weatherData.daily.temperature_2m_max.reduce((sum, t) => sum + t, 0) /
            weatherData.daily.temperature_2m_max.length
        )
      : null
  );

  // Save the last searched city to the browser
  $effect(() => {
  if (searchedCity) {
  localStorage.setItem("lastCity", searchedCity);
  }
  });

  const weatherDescriptions = /** @type {Record<number, string>} */ ({
    0: "Clear",
    1: "Mainly clear",
    2: "Partly cloudy",
    3: "Overcast",
    45: "Fog",
    48: "Depositing rime fog",
    51: "Light drizzle",
    53: "Moderate drizzle",
    55: "Dense drizzle",
    61: "Slight rain",
    63: "Moderate rain",
    65: "Heavy rain",
    71: "Slight snow",
    73: "Moderate snow",
    75: "Heavy snow",
    80: "Rain showers",
    81: "Rain showers",
    82: "Violent rain showers",
    95: "Thunderstorm"
  });

  function getWeatherIcon(code) {
    // OpenWeather icon set used as lightweight visual badges.
    if ([0, 1].includes(code)) return "https://openweathermap.org/img/wn/01d@2x.png";
    if ([2].includes(code)) return "https://openweathermap.org/img/wn/02d@2x.png";
    if ([3].includes(code)) return "https://openweathermap.org/img/wn/03d@2x.png";
    if ([45, 48].includes(code)) return "https://openweathermap.org/img/wn/50d@2x.png";
    if ([51, 53, 55].includes(code)) return "https://openweathermap.org/img/wn/09d@2x.png";
    if ([61, 63, 65, 80, 81, 82].includes(code)) return "https://openweathermap.org/img/wn/10d@2x.png";
    if ([71, 73, 75].includes(code)) return "https://openweathermap.org/img/wn/13d@2x.png";
    if ([95].includes(code)) return "https://openweathermap.org/img/wn/11d@2x.png";
    return "https://openweathermap.org/img/wn/04d@2x.png";
  }

  async function searchCity() {
    if (!city.trim()) {
      return;
    }

    loading = true;
    errorMsg = "";
    weatherData = null;

    try {
      const geoUrl = `https://geocoding-api.open-meteo.com/v1/search?name=${encodeURIComponent(city)}&count=1`;
      const geoRes = await fetch(geoUrl);
      const geoData = await geoRes.json();

      if (!geoData?.results?.length) {
        errorMsg = "City not found.";
        return;
      }

      const { latitude, longitude, name } = geoData.results[0];

      const weatherUrl = `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&current=temperature_2m,weather_code,wind_speed_10m&daily=temperature_2m_max,temperature_2m_min,precipitation_probability_max,wind_speed_10m_max&temperature_unit=celsius&wind_speed_unit=mph&timezone=auto`;
      const res = await fetch(weatherUrl);

      if (!res.ok) {
        throw new Error("Failed to fetch weather.");
      }

      const data = await res.json();
      weatherData = { ...data, cityName: name };

      mapLon = longitude;
      mapLat = latitude;
      searchedCity = name;
    } catch (error) {
      errorMsg = "Unable to fetch weather data right now.";
    } finally {
      loading = false;
    }
  }
</script>

<h1 class="text-3xl font-bold mb-4">Current Weather</h1>

<form class="flex gap-2 mb-6" onsubmit={(e) => { e.preventDefault(); searchCity(); }}>
  <Input placeholder="Enter a city..." bind:value={city} />
  <Button type="submit" variant="outline" class="bg-[#f8a484] text-[#fdfcfa]">
    Search
  </Button>
</form>

{#if loading}
  <p>Loading...</p>
{/if}

{#if errorMsg}
  <p class="text-red-500 mb-4">{errorMsg}</p>
{/if}

{#if weatherData}
  <div class="grid grid-cols-1 lg:grid-cols-2 gap-6 items-start mb-6">
    <Card.Root class="w-full bg-white rounded shadow">
      <Card.Header class="p-4 border-b">
        <div class="flex items-center justify-between gap-3">
          <div>
            <Card.Title class="text-xl font-semibold">{weatherData.cityName}</Card.Title>
            <Card.Description class="text-sm text-gray-500">Current Conditions</Card.Description>
          </div>
          <img
            src={getWeatherIcon(weatherData.current.weather_code)}
            alt={weatherDescriptions[weatherData.current.weather_code] || "Weather icon"}
            class="h-32 w-32 md:h-32 md:w-32 shrink-0"
          />
        </div>
      </Card.Header>
      <Card.Content class="p-4 space-y-2">
        <p class="text-3xl font-bold">{weatherData.current.temperature_2m} C</p>
        <p>Condition: {weatherDescriptions[weatherData.current.weather_code] || "Unknown"}</p>
        <p>Wind Speed: {weatherData.current.wind_speed_10m} mph</p>
      </Card.Content>
    </Card.Root>

    <WeatherMap lon={mapLon} lat={mapLat} />
  </div>

  <ForeCastTable forecast={weatherData.daily} />
{/if}

{#if avgHigh !== null}
  <hr class="my-4 border-t border-gray-300" />
  <p class="text-lg font-semibold">
    7-day avg high: {avgHigh}C
  </p>
{/if}
