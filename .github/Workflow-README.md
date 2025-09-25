# GitHub Actions Workflows for spoon-cli

This directory contains GitHub Actions workflows for automated building and publishing of the spoon-cli package.

## Workflows

### Release Workflow (`release.yml`)

Automatically builds and publishes the spoon-cli package to PyPI when a new release is created.

#### Triggers
- When a release is published
- Manual trigger via `workflow_dispatch`

#### Requirements

To use this workflow, you need to configure the following repository secret:

**`PYPI_API_TOKEN`**
- Go to https://pypi.org/manage/account/
- Generate an API token
- Add it as a repository secret named `PYPI_API_TOKEN`

#### How it works

1. **Build Job**: Builds the Python package distributions
   - Checks out the code
   - Sets up Python 3.11
   - Installs build dependencies
   - Builds wheel and source distributions
   - Uploads artifacts

2. **Publish Job**: Publishes to PyPI
   - Downloads the built distributions
   - Publishes to PyPI using the configured API token

#### Manual Release Process

1. Update version in `pyproject.toml`
2. Commit and push changes
3. Create a new GitHub release (tag should match version)
4. The workflow will automatically build and publish to PyPI

#### Security Notes

- The workflow uses trusted PyPI publishing action
- API token is stored as a repository secret
- Only runs on release events or manual dispatch
