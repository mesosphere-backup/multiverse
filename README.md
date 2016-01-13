# Mesosphere Multiverse [![Build Status](https://teamcity.mesosphere.io/guestAuth/app/rest/builds/buildType:(id:Oss_Multiverse_Ci)/statusIcon)](https://teamcity.mesosphere.io/viewType.html?buildTypeId=Oss_Multiverse_Ci&guest=1)

The DCOS package repository for experimental packages.

Certified packages can be found in the [Universe repository](https://github.com/mesosphere/universe). The Mesosphere Universe sets the standard for all services to be added to DCOS and should be the point of reference for all certifications, standards, verification scripts and tests.

## Installation

The [DCOS CLI](https://docs.mesosphere.com/install/cli/) **does not** come pre-configured to use the Multiverse repository.

To install and use the Multiverse:

```sh
dcos config prepend package.sources https://github.com/mesosphere/multiverse/archive/version-1.x.zip
dcos package update --validate
```

## Branches

The default branch for this repository is `version-1.x`, which reflects the current schema for the Multiverse. In the future, if the format changes significantly, there will be additional branches.

## Contributing a Package

Interested in making your package or service available to the world? The instructions below will help you set up a local copy of the Multiverse for development.

### Local Set Up

1. Clone the repo (or you may wish to fork it first):

    ```
    git clone https://github.com/mesosphere/multiverse.git /path/to/multiverse
    ```

2. You may need to install the `jsonschema` Python package if you don't have it:

    ```
    sudo pip install jsonschema
    ```

3. Install pre-commit hook:

    ```
    bash /path/to/universe/scripts/install-git-hooks.sh
    ```

4. To use the local cloned repository from the DCOS CLI for testing your own package:

    ```
    dcos config prepend package.sources "file:///path/to/multiverse"
    ```

The pre-commit hook will run [build.sh](scripts/build.sh) before allowing you to commit. This script validates your package definitions and regenerates the index file. You may need to `git add repo/meta/index.json` after running it once before you are able to pass validation and commit your changes.

Whenever you make changes locally, be sure to update the CLI's cache to pick them up:
```
dcos package update
```

### Merging to Multiverse

Before merging to Multiverse, you **must** run build.sh to regenerate the package index. If you have installed the pre-commit hook as above, this will be done automatically on commit.

Packages in the Universe are required to pass Mesosphere certification. The certification requirements for the [Multiverse repository](https://github.com/mesosphere/multiverse) are less strict, which is preferable for alpha or beta quality packages. Full certification requirements are available from [Mesosphere support](https://docs.mesosphere.com/support/).

Once your package meets these requirements, please submit a pull request against the `version-1.x` branch with your changes.

## Package Entries

Full documentation on the repository specification is available in the [Universe README](https://github.com/mesosphere/universe/blob/version-1.x/README.md).
