# Export Issues

Exports all issues as markdown documents

## Inputs

### `repo`

**Required** 

### `org`

**Required**

### `out`

**Required**

## Example usage

1. Create a `.github/workflows/export.yml` file in your GitHub repo, if one doesn't exist already.
2. Add the following code to the `export.yml` file.
```yaml
name: Export issues
on:
  schedule:
    # run every 8 hours
    - cron:  '0 0,8,16 * * *'
jobs:
  deploy:
    name: Export issues to S3
    runs-on: ubuntu-latest
    steps:
    - name: Export issues
      uses: niteoweb/export-issues-action@v2
      with:
        repo: ${{ github.repository }}
        org: ${{ github.repository_owner }}
        repo-token: ${{ secrets.GITHUB_TOKEN }}
        out: issues
    - name: Archive production artifacts
      uses: actions/upload-artifact@v2
      with:
        name: issues
        path: "issues/*.md"
```

# Extra

We also include script that is able to convert BackHub backed issues to Markdown documents.

To run:
```shell
bash convert-backup.sh issues-backuply issues-md
```