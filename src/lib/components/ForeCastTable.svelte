<script>
  import * as Table from "$lib/components/ui/table";

  let { forecast } = $props();

  function formatDayLabel(dateString) {
    const [year, month, day] = dateString.split("-").map(Number);
    const date = new Date(year, month - 1, day);
    const weekday = new Intl.DateTimeFormat("en-US", { weekday: "short" }).format(date);
    return `${weekday} ${month}/${day}`;
  }

  function isRainyDay(index) {
    return forecast?.precipitation_probability_max?.[index] >= 50;
  }
</script>

{#if forecast}
  <Table.Root>
    <Table.Header>
      <Table.Row>
        <Table.Head>Date</Table.Head>
        <Table.Head>High</Table.Head>
        <Table.Head>Low</Table.Head>
        <Table.Head>Wind</Table.Head>
        <Table.Head>Precipitation</Table.Head>
      </Table.Row>
    </Table.Header>
    <Table.Body>
      {#each forecast.time as day, i}
        <Table.Row class={isRainyDay(i) ? "bg-sky-50/80 border-l-4 border-l-sky-500" : ""}>
          <Table.Cell>{formatDayLabel(day)}</Table.Cell>
          <Table.Cell>{forecast.temperature_2m_max[i]} C</Table.Cell>
          <Table.Cell>{forecast.temperature_2m_min[i]} C</Table.Cell>
          <Table.Cell>{forecast.wind_speed_10m_max[i]} mph</Table.Cell>
          <Table.Cell class={isRainyDay(i) ? "font-semibold text-sky-700" : ""}>
            {forecast.precipitation_probability_max[i]}%
          </Table.Cell>
        </Table.Row>
      {/each}
    </Table.Body>
  </Table.Root>
{/if}
