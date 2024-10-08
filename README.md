# Node.js Cleanup

[![GitHub Release](https://img.shields.io/github/v/release/ryohidaka/action-nodejs-cleanup)](https://github.com/ryohidaka/action-nodejs-cleanup/releases/)
[![Test Action](https://github.com/ryohidaka/action-nodejs-cleanup/actions/workflows/test.yml/badge.svg)](https://github.com/ryohidaka/action-nodejs-cleanup/actions/workflows/test.yml)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://opensource.org/licenses/MIT)

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/B0B6TVH92)

A GitHub Action that cleanup Node.js template configures.

## Usage

```yml
on:
  push:
    branches:
      - main

jobs:
  template-cleanup:
    name: Template Cleanup
    runs-on: ubuntu-latest
    if: github.event.repository.name != 'nodejs-cleanup'
    permissions:
      contents: write
    steps:
      - uses: ryohidaka/action-nodejs-cleanup@v1.5.1
        with:
          description: "new description"
          version: "1.0.0"
          remove-license: true
          excluded: "test-dir, test.txt"
          pre-commit-script: |
            npm run build
            npm run lint
```

## Inputs

| Input                 | Default                                                                    | Description                                                          |
| --------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `description`         |                                                                            | The description of the project.                                      |
| `version`             | `0.0.0`                                                                    | The version of the project.                                          |
| `email`               |                                                                            | The email address to be used in the project.                         |
| `bugs-url`            |                                                                            | The URL where the project's bugs are tracked.                        |
| `homepage`            |                                                                            | The URL of the project's homepage.                                   |
| `remove-license`      | `false`                                                                    | A boolean value that indicates whether to remove the license.        |
| `excluded`            |                                                                            | Comma-separated list of file or directory paths to remove.           |
| `template-dir`        |                                                                            | The path to the project's template directory.                        |
| `remove-template-dir` | `false`                                                                    | A boolean value indicating whether to remove the template directory. |
| `placeholders`        | `{"name": "%NAME%", "description": "%DESCRIPTION%", "author": "%AUTHOR%"}` | A JSON string to specify the placeholders for the project            |
| `node-version`        | `latest`                                                                   | Version Spec of the version to use in SemVer notation.               |
| `pre-commit-script`   |                                                                            | The shell script code to execute before committing changes.          |
| `commit-user-name`    | `GitHub Actions`                                                           | The username for the commit.                                         |
| `commit-user-email`   | `actions@github.com`                                                       | The user email for the commit.                                       |
| `commit-message`      | `Template cleanup`                                                         | The commit message.                                                  |
| `dryrun`              | `false`                                                                    | Execute the process, but do not push the commit at the end.          |

> [!IMPORTANT]
> GitHub Actions workflow files must be placed in the `workflows` directory in the template directory.
>
> If you place them in any other directory, they will not be copied to the correct directory.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
