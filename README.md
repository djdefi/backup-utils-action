# backup-utils-action

[GitHub Enterprise Backup Utilities](https://github.com/github/backup-utils) running in GitHub Actions.

## Example workflow

```yaml
on: 

  workflow_dispatch:
    inputs:
      ghe-hostname:
        description: 'GitHub Enterprise Hostname'
        required: true
        default: 'github.example.com'
      verbose:
        description: 'Verbose output'
        required: false
        default: 'true'
      restore:
        description: 'Restore from backup'
        required: false
        default: 'false'

  #schedule:
    # Hourly
  #  - cron: '0 * * * *'

jobs:

  backup:
    runs-on: ubuntu-latest
    steps:
      - name: Backup GitHub Enterprise
        uses: djdefi/backup-utils-action@main
        with:
          ghe-hostname: ${{ github.event.inputs.ghe-hostname }}
          verbose: ${{ github.event.inputs.verbose }}
          restore: ${{ github.event.inputs.restore }}
          ssh-private-key: ${{ secrets.SSH_PRIVATE_KEY }}
```

Requires a secret containing a valid private SSH key with access to the GitHub Enterprise Server.

## Running

Run via workflow dispatch, providing the hostname of the applaince to backup (or restore if restore = true)

## Restoring

Coming soon!

## Multiple snapshots

Coming soon!

## Self-hosted runners

Coming soon!
