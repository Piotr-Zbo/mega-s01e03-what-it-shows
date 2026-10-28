# [4471 split] booking-v3 date hint conflicts with day-first tenants — 33 reports

## Problem
The booking-v3 form displays MM/DD/YYYY, while these tenants use day-first date conventions. People follow the hint, but the form interprets the value according to the tenant locale.

## Scope
33 unique reports: alder.physio (12), copper.studio (11), and pale.harbour (10).

## Evidence
The kb's cause classifier identifies booking-v3 form submissions for day-first tenants as the `hint` cause. This is separate from the shared parser bug, so the parser fix queued for #4471 does not resolve it.

## Requested action
Correct the form hint or its input parsing so displayed date order matches the tenant locale. Track this independently from the shared parser issue.

## Resolution
Engineering marked this won't fix because the booking-v3 form was retired. Close this issue as not planned.
