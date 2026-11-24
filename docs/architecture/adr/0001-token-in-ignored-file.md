# ADR 0001: Keep the bot token in an ignored `token.txt`

## Status

Accepted. The helper appeared in commit `f2496ff` (as `tokenhelper.py`); `legacy.py` moved to it in commit
`726faec`.

## Context

A Discord bot logs in with a secret token. A token in the source reaches every clone and stays in the Git history.

## Decision

`token_helper.get_token()` reads the first line of `./token.txt`. `.gitignore` lists `token.txt`. The README tells
the owner to create the file by hand. `ksalol-chan-dev.py`, `ksalol_chan.py` and `legacy.py` all call
`get_token()`.

## Consequences

- New commits carry no token.
- The bot must start in the folder that holds `token.txt`.
- The history before commit `726faec` still holds the token that `legacy.py` had in its source; that token needs
  revocation if it is still valid.

## Evidence

- `token_helper.py`, `.gitignore`, `README.md` step 2
- commits `f2496ff`, `a89b94b` (rename to `token_helper.py`), `726faec`
