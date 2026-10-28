# [4471 split] Shared parser flips dates for day-first tenants — 379 reports

## Problem
The shared date parser reads month first. Reports from day-first tenants therefore land on the wrong day, across multiple tenants and intake channels.

## Scope
379 unique reports in the parser cause group. This count includes the five reports that the support desk flags as one-day moves.

## Evidence
The kb export classifies reports using tenant locale and booking form. The parser is the cause for the remaining day-first tenant reports; intake tags are only guesses and are not a reliable grouping key.

## Requested action
Track and fix the shared parser behavior for day-first tenant dates. Keep the booking-v3 form-hint cause in a separate issue; investigate the five flagged one-day-move reports as a subset of this group.
