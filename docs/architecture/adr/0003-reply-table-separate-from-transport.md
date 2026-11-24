# ADR 0003: Keep reply texts in `responses.py`, apart from the Discord transport

## Status

Accepted. Introduced in commit `0e1a2ee`.

## Context

In `legacy.py` the reply texts and the Discord calls sit in 1 event method, so each new trigger adds an `if` block
next to a `send` call.

## Decision

`responses.get_response(msg)` maps a message text to a reply text and has no Discord import. `send_msg()` in
`ksalol_chan.py` calls it and sends the reply to the channel, or to the author when the message starts with `?`.

## Consequences

- Reply texts can change without touching Discord code.
- `get_response()` returns the string `'None'` for an unknown message, and `send_msg()` sends that string; a caller
  must filter it.
- The entry point in the README, `ksalol-chan-dev.py`, does not use `responses.py` yet.

## Evidence

- `responses.py`
- `send_msg()` and `run_ksalol_sama()` in `ksalol_chan.py`
- `legacy.py`
- commit `0e1a2ee`
