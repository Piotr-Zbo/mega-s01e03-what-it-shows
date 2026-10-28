# [4471 split] Investigate five one-day moves — 5 reports

## Problem
Five reports in #4471 describe one-day shifts or timing behavior rather than month/day flips. The support desk's `desk-notes.json` explicitly identifies them as one-day moves.

## Scope
5 unique reports: R-41202, R-41209, R-41236, R-41344, and R-41620.

## Evidence
The reports include an invite arriving before its booking, different days shown in Lisbon and Toronto, and Tuesday/Monday shifts. These symptoms do not fit either the shared month-first parser bug or the booking-v3 form-hint bug.

## Requested action
Investigate timezone and timing behavior separately. Do not include these reports in the parser or form-hint fixes until their cause is confirmed.
