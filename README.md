# `arduino/arduino-lint-action`

[![Tests Status](https://github.com/arduino/arduino-lint-action/workflows/Test%20Action/badge.svg)](https://github.com/arduino/arduino-lint-action/actions?workflow=Test+Action)
[![Integration Tests Status](https://github.com/arduino/arduino-lint-action/workflows/Integration%20Tests/badge.svg)](https://github.com/arduino/arduino-lint-action/actions?workflow=Integration+Tests)
[![Spellcheck Status](https://github.com/arduino/arduino-lint-action/workflows/Spell%20Check/badge.svg)](https://github.com/arduino/arduino-lint-action/actions?workflow=Spell+Check)

[GitHub Actions](https://docs.github.com/en/free-pro-team@latest/actions) action that uses
[Arduino Lint](https://github.com/arduino/arduino-lint) to check for problems with [Arduino](https://www.arduino.cc/)
projects:

- Libraries
- Sketches
- Boards platforms

## Table of contents

<!-- toc -->

- [Inputs](#inputs)
  - [`path`](#path)
  - [`version`](#version)
  - [`compliance`](#compliance)
  - [`format`](#format)
  - [`library-manager`](#library-manager)
  - [`project-type`](#project-type)
  - [`recursive`](#recursive)
  - [`report-file`](#report-file)
  - [`token`](#token)
- [Usage](#usage)

<!-- tocstop -->

## Inputs

### `path`

Path containing Arduino project(s).

**Default**: `./`

### `version`

The version of [Arduino Lint](https://github.com/arduino/arduino-lint) to use.
Can be an exact version (e.g., `1.0.0`) or a version range (e.g., `1.x`).

**Default**: `1.x`

### `compliance`

Configure how strict the tool is about which checks are considered errors vs warnings if they don't pass.

#### Supported values

- `strict` - enforces best practices, above and beyond the minimum requirements for specification compliance. Use this setting to ensure the best experience for the users of the project.
- `specification` - enforces compliance with the official Arduino project specifications.
- `permissive` - will cause the checks to fail only when severe problems are found. Although a project that passes at the permissive setting will work with the current Arduino development software versions, it may not be fully specification-compliant, risking incompatibility or a poor experience for the users.

**Default**: `specification`

### `library-manager`

Configure the checks for libraries in the [Arduino Library Manager](https://github.com/arduino/Arduino/wiki/Library-Manager-FAQ) index.

#### Supported values

- `submit` - Also run additional checks required to pass before a library is accepted for inclusion in the index.
- `update`- Also run additional checks required to pass before a library is accepted for inclusion in the index.
- `false` - Don't run any Library Manager-specific checks.

**Default**: `submit` for libraries, `false` for other project types

### `project-type`

Configures which types of projects to check, along with their subprojects.

#### Supported values

- `sketch`
- `library`
- `all` - Run checks on any type of project that is detected

**Default**: `all`

### `recursive`

Set to `true` to search path recursively for Arduino projects to check.

**Default**: `false`

### `report-file`

Save a JSON formatted report on the checks to this file.

### `verbose`

Set to `true` to show more information in the log about the checks being run.

**Default**: `false`

### `token`

GitHub access token used to get information from the GitHub API.

**Default**: [`GITHUB_TOKEN`](https://docs.github.com/en/free-pro-team@latest/actions/reference/authentication-in-a-workflow)

## Usage

The minimal workflow to run the default checks on the projects in the repository:

```yaml
on: [push, pull_request]
jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: arduino/arduino-lint-action@v1
```

## Development

To work on the codebase you have to install all the dependencies:

```sh
# npm install
```

To run tests set the environment variable `GITHUB_TOKEN` with a valid Personal Access Token and then:

```sh
# npm run test
```

See the [official Github documentation][pat-docs] to know more about Personal Access Tokens.

## Release

1. `npm install` to add all the dependencies, included development.
2. `npm run build` to build the Action under the `./lib` folder.
3. `npm run test` to see everything works as expected.
4. `npm run pack` to package for distribution
5. `git add src dist` to check in the code that matters.
6. open a PR and request a review.

[pat-docs]: https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token
