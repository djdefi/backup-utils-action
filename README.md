# GitHub Enterprise Server `backup-utils` Action

[GitHub Enterprise Server Backup Utilities](https://github.com/github/backup-utils) running in GitHub Actions.

## Example workflow

Save the workflow as: [`.github/workflows/ghes-backup-utils.yml`](.github/workflows/ghes-backup-utils.yml) in your repository:

```yaml
name: 'GitHub Enterprise Server Backup and Restore Workflow'
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
      backup-utils-tag:
        description: 'Specify the backup-utils tag to use'
        required: false

  schedule:
    # Hourly
    - cron: '0 * * * *'
  
jobs:

  backup:
    runs-on: ubuntu-latest
    steps:
      - name: Backup GitHub Enterprise
        env:
          SCHEDULED_HOSTNAME: 'github.example.com'
        uses: djdefi/backup-utils-action@main
        with:
          ghe-hostname: ${{ github.event.inputs.ghe-hostname || env.SCHEDULED_HOSTNAME }}
          verbose: ${{ github.event.inputs.verbose }}
          restore: ${{ github.event.inputs.restore }}
          ssh-private-key: ${{ secrets.SSH_PRIVATE_KEY }}
          backup-utils-tag: 'v2.22.1' # Specify the version of backup-utils to use
```

* Requires adding a repository or organization level Actions secret `SSH_PRIVATE_KEY` containing a valid private SSH key with [access to the GitHub Enterprise Server adminstrative shell](https://docs.github.com/enterprise-server/admin/configuration/configuring-your-enterprise/accessing-the-administrative-shell-ssh). RSA and ED25519 keys are supported.

## Running

Run via workflow dispatch, providing the hostname of the appliance to backup.

## Restoring

1. Set `restore = true` in the workflow dispatch along with a target hostname or IP.
2. Not fully implemented - Coming soon!

## Customization of `backup-utils` configuration options 

You can now specify the `backup-utils` tag to use by setting the `backup-utils-tag` input in your workflow file. This allows for the use of a specific version of the backup-utils for your backup or restore operations.

## Multiple snapshots

Coming soon!

## Self-hosted runners

Coming soon!
