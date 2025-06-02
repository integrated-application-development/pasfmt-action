# `pasfmt` Action

This GitHub Action checks the formatting of your Delphi files using [pasfmt](https://github.com/integrated-application-development/pasfmt).

## Inputs

| Name                | Description                                           | Default              |
| ------------------- | ----------------------------------------------------- | -------------------- |
| `args`              | Arguments passed to `pasfmt`.                         | `--mode check .`     |
| `release-name`      | The pasfmt release to use (e.g., `latest`, `v0.5.1`). | `latest`             |
| `working-directory` | Directory where `pasfmt` will run.                    | `.` (root directory) |

## Examples

Check the formatting of all Delphi files in the repository, using the latest `pasfmt` release.

```yml
jobs:
  check-formatting:
    runs-on: windows-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Run pasfmt
        uses: integrated-application-development/pasfmt-action@v1
```

Check the formatting of all Delphi files in `./src`, using `pasfmt` release `v0.5.1`.

```yml
jobs:
  check-formatting:
    runs-on: windows-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Run pasfmt
        uses: integrated-application-development/pasfmt-action@v1
        with:
          args: "--mode check ./src"
          release-name: "v0.5.1"
```

Check the formatting of all Delphi files in the repository, using CRLF line endings.

```yml
jobs:
  check-formatting:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Run pasfmt
        uses: integrated-application-development/pasfmt-action@v1
        with:
          args: "--mode check -C line_ending=crlf ."
```

## Supported Platforms

- Windows
- Linux
> [!WARNING]
>
> The default value of the `line_ending` option is `native`, which is platform-dependent.
>
> If this action formats files with `CRLF` line endings on a non-windows machine, native line
> endings will cause `pasfmt` to flip the line endings (`CRLF` -> `LF`)  and fail the check.
>
> You can configure your `.gitattributes` to handle line endings automatically. \
> See: [Configuring Git to handle line endings](https://docs.github.com/en/get-started/getting-started-with-git/configuring-git-to-handle-line-endings?platform=windows)
>
> Alternatively, you can configure `pasfmt` to use CRLF line endings. \
> See the above example where `-C line_ending=crlf` is passed via `args`.
