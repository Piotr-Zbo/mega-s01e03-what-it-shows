# [4471 split] Shared parser flips dates for day-first tenants — 374 reports

## Problem
The shared date parser reads month first. Reports from day-first tenants therefore land on the wrong day, across multiple tenants and intake channels.

## Scope
374 unique reports after excluding the separately classified 33 booking-v3 form-hint reports and the five desk-noted one-day-move reports.

## Evidence
The kb export classifies reports using tenant locale and booking form. The parser is the cause for the remaining day-first tenant reports; intake tags are only guesses and are not a reliable grouping key.

## Requested action
Track and fix the shared parser behavior for day-first tenant dates. Keep the booking-v3 hint and one-day-move problems in separate issues.
