# Getting Started

With `mike`, we can easily render a new version of the documentation and deploy it to the `gh-pages` (by default) branch.

## How to create a new version of the documentation with `mike`

First of all, we have to make sure that `mike` and `mkdocs-material` are installed in our environment. They can be installed with `pip` as below.

!!! note
    The following commands install the packages to the global environment by default. If it is not desired, remember to activate any virtual environment you are using.

```bash
pip install mike mkdocs-material
```

Then, we have to make sure we are at the correct commit, which we will use to render the documentation.

```bash
git checkout <commit-hash|tag-name>
```

After that, we can render the documentation with the following command:

```bash
mike deploy --update-aliases 0.1 latest
```

where `0.1` is the newly created version, and `latest` is the alias for the latest version, pointing to `0.1` in this case.

!!! tips
    There are some other common options that you can use with `mike`.

    - `--branch`: Deploy the documentation to a different branch (default: `gh-pages`).
    - `--push`: Push the changes to the remote repository. By default, `mike` will only deploy the documentation to the local repository.

If this is the first deployment, we will also have to make `mike` redirect the root to the latest version:

```bash
mike set-default latest
```

Similar to the `deploy` command, the `--branch` and `--push` options are also available for the `set-default` command.

After all these steps, the documentation should be properly deployed to the target branch.

!!! note
    To make the versioning feature of `mkdocs-material` work, the `site_url` in the `mkdocs.yml` file must be configured correctly.

## Test the documentation locally

To properly test the documentation locally, we should stay on the main branch (instead of `gh-pages`) and call the following command:

```bash
mike serve
```

This will start a local server at `http://localhost:8000` (by default), and we can see all the versions that have been deployed.

!!! note
    In my testing environment, it works much slower than the `mkdocs serve` command. Checking out the `gh-pages` branch and serving the documentation with `python -m http.server` works much faster, but I am not sure if there is any potential issue.



