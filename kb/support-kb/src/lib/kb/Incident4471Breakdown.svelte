<script lang="ts">
  import reports from '#lib/data/reports-4471.json';
  import notes from '#lib/data/desk-notes.json';
  import { causeOf, uniqueById, type Cause, type Report } from '#lib/kb/causes';
  import { tenantOf } from '#lib/kb/locales';

  const unique = uniqueById(reports as Report[]);
  const oneDayMoves = new Set(notes.oneDayMove);
  const causes: readonly Cause[] = ['parser', 'hint'];
  const groups = causes.map((cause) => ({
    cause,
    count: unique.filter((r) => causeOf(r, tenantOf(r)) === cause).length,
  }));
  const oneDayMoveCount = unique.filter((r) => oneDayMoves.has(r.id)).length;
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
        <td>{group.cause === 'parser'
          ? 'The shared parser reads month first, flipping dates for day-first tenants.'
          : 'The booking-v3 form shows MM/DD/YYYY while these tenants use day-first dates.'}</td>
      </tr>
    {/each}
  </tbody>
</table>

<p>{oneDayMoveCount} reports in the parser group are flagged by desk notes as one-day moves: {flaggedIds.join(', ')}. They remain part of the parser group's exported count.</p>
