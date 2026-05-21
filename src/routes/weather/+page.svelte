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
          weatherData.daily.temperature_2m_max.reduce((/** @type {number} */ sum, /** @type {number} */ t) => sum + t, 0) /
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

  function getWeatherIcon(/** @type {number} */ code) {
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

<div class="page-shell">
  <section class="hero-panel weather-hero">
    <div>
      <h2>Weather Tool</h2>
      <h1>Current Weather</h1>
      <p class="lead">
        A compact weather interface that turns live forecast data into an immediate, readable city snapshot.
      </p>
    </div>

    <form class="search-panel" onsubmit={(e) => { e.preventDefault(); searchCity(); }}>
      <Input placeholder="Enter a city..." bind:value={city} class="weather-input" />
      <Button type="submit" variant="outline" class="weather-button">
        {loading ? "Searching..." : "Search"}
      </Button>
    </form>
  </section>

  {#if loading}
    <p class="status">Loading weather data...</p>
  {/if}

  {#if errorMsg}
    <p class="status error">{errorMsg}</p>
  {/if}

  {#if weatherData}
    <section class="weather-grid">
      <Card.Root class="weather-card">
        <Card.Header class="weather-card-header">
          <div>
            <Card.Title class="weather-title">{weatherData.cityName}</Card.Title>
            <Card.Description class="weather-description">Current Conditions</Card.Description>
          </div>
          <img
            src={getWeatherIcon(weatherData.current.weather_code)}
            alt={weatherDescriptions[weatherData.current.weather_code] || "Weather icon"}
            class="weather-icon"
          />
        </Card.Header>
        <Card.Content class="weather-content">
          <p class="temperature">{weatherData.current.temperature_2m} C</p>
          <p>Condition: {weatherDescriptions[weatherData.current.weather_code] || "Unknown"}</p>
          <p>Wind Speed: {weatherData.current.wind_speed_10m} mph</p>
          {#if avgHigh !== null}
            <p class="avg">7-day avg high: {avgHigh} C</p>
          {/if}
        </Card.Content>
      </Card.Root>

      <div class="map-shell">
        <WeatherMap lon={mapLon} lat={mapLat} />
      </div>
    </section>

    <section class="forecast-shell">
      <ForeCastTable forecast={weatherData.daily} />
    </section>
  {/if}
</div>

<style>
  .weather-hero {
    display: grid;
    grid-template-columns: minmax(0, 1fr) minmax(280px, 420px);
    gap: clamp(34px, 6vw, 72px);
    align-items: end;
  }

  .search-panel {
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 18px;
    border: 0;
    border-top: 1px solid #000000;
    border-radius: 0;
    padding: 28px 0 0;
    background: transparent;
  }

  :global(.weather-input) {
    min-height: 44px;
    border-color: #000000 !important;
    background: transparent !important;
    color: var(--text) !important;
  }

  :global(.weather-input::placeholder) {
    color: var(--soft) !important;
  }

  :global(.weather-button) {
    min-height: 44px;
    border-color: rgba(0, 0, 0, 0.35) !important;
    background: transparent !important;
    color: var(--text) !important;
  }

  .status {
    margin: 0;
    color: var(--soft);
  }

  .error {
    color: var(--text);
    text-decoration: underline;
  }

  .weather-grid {
    display: grid;
    grid-template-columns: minmax(280px, 0.75fr) minmax(0, 1.25fr);
    gap: clamp(34px, 6vw, 72px);
    align-items: stretch;
  }

  :global(.weather-card),
  .map-shell,
  .forecast-shell {
    overflow: hidden;
    border: 0 !important;
    border-top: 1px solid #000000 !important;
    border-radius: 0 !important;
    background: transparent !important;
    color: var(--text) !important;
    box-shadow: none;
  }

  :global(.weather-card-header) {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 18px;
    border-bottom: 1px solid var(--line);
    padding: 22px !important;
  }

  :global(.weather-title) {
    color: var(--text);
    font-size: clamp(2rem, 4vw, 4rem);
    font-family: var(--font-heading);
    line-height: 0.95;
  }

  :global(.weather-description) {
    color: var(--soft);
  }

  .weather-icon {
    width: 112px;
    height: 112px;
    filter: drop-shadow(0 12px 26px rgba(0, 0, 0, 0.28));
  }

  :global(.weather-content) {
    padding: 22px !important;
    color: var(--soft);
  }

  .temperature {
    margin: 0 0 12px;
    color: var(--accent);
    font-size: clamp(4rem, 10vw, 8rem);
    font-weight: 850;
    line-height: 0.9;
    font-family: var(--font-heading);
  }

  .avg {
    margin-top: 18px;
    color: var(--accent-strong);
    font-weight: 800;
  }

  .forecast-shell {
    padding: 8px;
  }

  @media (max-width: 860px) {
    .weather-hero,
    .weather-grid {
      grid-template-columns: 1fr;
    }
  }

  @media (max-width: 560px) {
    .search-panel {
      grid-template-columns: 1fr;
    }
  }
</style>
