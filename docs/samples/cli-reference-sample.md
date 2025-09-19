# CLI Reference (Sample)

Short, scannable reference entries.

## `acme login`
**Synopsis:** Authenticate to Acme Cloud.

```bash
acme login [--token TOKEN] [--profile NAME]
```

**Options**
- `--token` string. Personal access token.
- `--profile` string. Named profile to update.

## `acme deploy`
**Synopsis:** Deploy a service.

```bash
acme deploy --service NAME [--env prod|staging] [--wait]
```

**Options**
- `--service` string. Required.
- `--env` enum. Default `staging`.
- `--wait` flag. Block until rollout completes.