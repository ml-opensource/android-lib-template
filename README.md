# Android Library Template

This is a template for creating Android Open Source libraries. This template features

- :rocket: Basis Project structure that includes demo and library modules
- :octocat: CI/CD with GitHub Actions for release and snapshot builds, documentation generation
- :mag: Code Quality checks with Detekt, Spotless and Tests
- :book: Documentation setup with Dokka and MkDocs
- :package: Dependency management with Version Catalogue
- :memo: CHANGELOG following a keepchangelog.com format
- :wrench: Gradle Convention Plugins for consistent build configuration across modules
- 🌐 GH pages to host the documentation

## Table of Contents
  - [Usage](#usage)
  - [Branching Strategy](#branching-strategy)
  - [CI/CD](#cicd)
  - [Release Management](#release-management)
    - [Draft Releases \& Snapshots](#draft-releases--snapshots)
    - [Release](#release)
  - [Changelog](#changelog)
  - [Documentation](#documentation)
    - [Github Pages](#github-pages)
  - [Contributing](#contributing)
  - [Resources](#resources)

## Usage
1. Click on the `Use this template` button to create a new repository from this template.
2. Update the `gradle.properties` files with the correct values for your library.
3. Add following secrets to your repository to enable publishing to Maven Central (For more information about following properties, please refer to [Gradle Maven Publish Plugin](https://vanniktech.github.io/gradle-maven-publish-plugin/central/))
   - `ORG_GRADLE_PROJECT_MAVENCENTRALPASSWORD` - Your Maven Central password
   - `ORG_GRADLE_PROJECT_MAVENCENTRALUSERNAME` - Your Maven Central username
   - `ORG_GRADLE_PROJECT_SIGNINGINMEMORYKEY` - Your GPG key
   - `ORG_GRADLE_PROJECT_SIGNINGINMEMORYKEYPASSWORD` - Your GPG key password
   - `ORG_GRADLE_PROJECT_SIGNINGINMEMORYKEYID` - Your GPG key ID


## Branching Strategy

This templates follows a trunk-based approach using its `main` branch as the single source of truth
for all changes.
Feature/Fixes and etc branches are created from `main` and are merged back using pull requests.

## CI/CD

This template uses GitHub Actions for CI/CD. The following workflows are set up:

- **Verify Pull Request**: Checks code quality with Detekt and Spotless, and runs tests
- **Publish Snapshot**: Publishes a snapshot version of the library to GitHub Packages
- **Publish Release**: Publishes a release version of the library to GitHub Packages
- **Generate Docs**: Generates documentation with Dokka and MkDocs


## Release Management

The release management is tied to the GitHub Releases.

### Draft Releases & Snapshots

Every push to the `main` triggers main workflow that will create a draft release. The draft release
version is set to the current version located in `gradle.properties` and the release notes for it
are taken from the `CHANGELOG.md`.

> In case the Draft Release exists already, it will be deleted and replaced with new one, so that
> there is only one draft release.

Together with Draft Releases the snapshot is published
This is done by applying `-SNAPSHOT` suffix to the version and publishing it to the Maven Central.

### Release

By promoting a Draft Release, the release workflow is triggered. It will publish the library to the
to the Maven Central.

## Changelog

This template follows the [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format for
changelog entries. The changelog is stored in the `CHANGELOG.md` file.
When Draft Release is created, the script `get_changelog.sh`
will be executed to update the release notes with the latest changes according
to the latest version specified in the `gradle.properties` file.

## Documentation

This template uses Dokka for code documentation and MkDocs Material for project documentation.
For more information on how to use MkDocs, please refer to
the [MkDocs documentation](https://www.mkdocs.org/) and Mkdocs
Material [documentation](https://squidfunk.github.io/mkdocs-material/).

The Dokka plugin is applied to the library module and generates KDocks documentation for the
library. The generated documentation is published together with the project documentation and can be
accessed using github pages.

### Github Pages
Every push to the `main` branch triggers the `Generate Docs` workflow that will generate the documentation and 
publish it to the `gh-pages` branch. The documentation can be accessed using the following link: 
`https://<username>.github.io/<repository-name>/`


## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
Please make sure to update tests as appropriate.


## Resources
- [Gradle Maven Publish Plugin](https://vanniktech.github.io/gradle-maven-publish-plugin/central/)
- [Keep a Changelog](https://keepachangelog.com/en/1.0.0/)
- [MkDocs](https://www.mkdocs.org/)
- [Mkdocs Material](https://squidfunk.github.io/mkdocs-material/)
- [Dokka](https://github.com/Kotlin/dokka)
- [GitHub Actions](https://docs.github.com/en/actions)
- [Detekt](https://detekt.github.io/detekt/)
- [Spotless](https://github.com/diffplug/spotless)

