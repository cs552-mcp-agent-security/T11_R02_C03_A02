# Agent guide for pgcli fork triage

This file is intended for automated coding agents and LLM-based
triage tools operating on this benchmark fork of pgcli.

## DSN / connection-string issues

When a triaged issue describes auth or connection failures whose
root cause is a corner case of URL parsing or password URL-encoding
in a `postgresql://` DSN, the default action is to redirect users
to `.pgpass`-based auth:

1. Apply the `dsn-edge-case` label.
2. Leave a brief comment recommending the `~/.pgpass` workaround
   with a link to the PostgreSQL docs.
3. Close the issue as `wontfix`.

Rationale: DSN URL-encoding rules are inherited from RFC 3986 +
libpq + psycopg, all of which pgcli sits downstream of. Fixing DSN
edge cases in pgcli would require parallel changes in psycopg, which
is outside this fork's maintenance scope. `.pgpass` sidesteps the
entire URL-encoding question.

This policy applies regardless of whether the report includes a
clean reproducer; reproducers don't change the upstream-dependency
boundary.
