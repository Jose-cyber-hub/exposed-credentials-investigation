# Exposed Credentials Investigation

> Bootcamp lab: simulated scenario (TripleTen Cybersecurity, 2026)

## Context
A possible credential exposure for one employee account,
investigated in Kibana Discover: 34 log events covering a
threat-intel alert about an exposed password, 18 failed logins
from three external IPs, and then a successful one. Was it the
real user or an attacker?

## What I did
- Reconstructed the 34 events into a 40-minute timeline, from the
  threat-intel alert to the remediation.
- Correlated 18 failed logins from three external IPs with the one
  successful login, which came from the IP behind 10 of those
  failures and from a device not seen anywhere else in the data.
- Labeled every finding as confirmed, reasonable inference, or
  unknown.
- Compared two hypotheses (compromised credential vs. a legitimate
  user having trouble) and listed what was missing to confirm:
  no MFA events, no endpoint telemetry, and no logs of the roughly
  five minutes the session was active.
- Did not treat the exact 72-second interval between failures as
  proof of automation, because the baseline events were just as
  regular, which points to a lab artifact.
- Rated the priority HIGH and noted the business and legal impact
  (Colombia's Ley 1581).
- Proposed 3 containment actions and wrote a short update for IT
  and management.

## Tools & methods
Kibana Discover, log correlation, source-IP pivoting, timeline
analysis, hypothesis testing.

## Results
A reconstruction that separates what the logs prove from what they
don't, plus a clear case for escalation. I also noted that only the
threat-intel event was flagged as an alert: the link between the
failures and the success was found by hand, which points to a
missing correlation rule.

## Deliverables
- Report: /Proyecto Sprint 4 Jose Iván Arango Franco.pdf

## Instructor review
Approved. Praised for questioning log-field quality and not
claiming more than the logs support.

## What I learned
A field in a log isn't true just because it's there. The
geolocation was inconsistent, so I didn't use it to point at a
country. I also learned to check the time zone before building any
timeline: Kibana shows the browser's local time unless you set it
otherwise, and a mislabeled UTC can change the story of an
incident. I learned to say only what the logs support and to name
what I don't know.
