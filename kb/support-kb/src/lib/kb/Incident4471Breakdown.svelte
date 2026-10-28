<script lang="ts">
  import reports from '#lib/data/reports-4471.json';
  import notes from '#lib/data/desk-notes.json';
  import { causeOf, uniqueById, type Cause, type Report } from '#lib/kb/causes';
  import { tenantOf } from '#lib/kb/locales';

  const unique = uniqueById(reports as Report[]);
  const oneDayMoves = new Set(notes.oneDayMove);
  const causes: readonly Cause[] = ['parser', 'hint'];
  const groups = [
    ...causes.map((cause) => ({
      cause,
      count: unique.filter((r) => !oneDayMoves.has(r.id) && causeOf(r, tenantOf(r)) === cause).length,
    })),
    { cause: 'one-day moves', count: unique.filter((r) => oneDayMoves.has(r.id)).length },
  ];
  const flaggedIds = [...oneDayMoves].sort();
</script>

<p><strong>{unique.length}</strong> unique reports in the export; the export contains {reports.length} rows because pages overlap.</p>

<table>
  <thead>
    <tr><th>problem</th><th>reports</th><th>finding</th></tr>
  </thead>
  <tbody>
    {#each groups as group (group.cause)}
      <tr>
        <td><code>{group.cause}</code></td>
        <td>{group.count}</td>
        <td>
          {#if group.cause === 'parser'}
            The shared parser reads month first, flipping dates for day-first tenants.
          {:else if group.cause === 'hint'}
            The booking-v3 form shows MM/DD/YYYY while these tenants use day-first dates.
          {:else}
            Desk notes flag one-day moves; these reports describe timezone or timing symptoms, not a month flip.
          {/if}
        </td>
      </tr>
    {/each}
  </tbody>
</table>

<p>Desk-noted one-day-move reports: {flaggedIds.join(', ')}.</p>
