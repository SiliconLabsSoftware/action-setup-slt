# Setup SLT

This GitHub Action downloads and install SLT, conan_engine and conan

## Features

- Download the latest SLT available
- Installs conan_engine and conan
- Sets the CONAN_HOME env variable to match the slt install and export it
- Exports the path to slt, conan_engine and conan

## Inputs

| Input           | Description                                                            | Required            |
| --------------- | ---------------------------------------------------------------------- | ------------------- |
| `install-conan` | Install conan alongside slt                                            | No (default: true)  |
| `use-unstable`  | If true, download SLT from the unstable channel instead of daily build | No (default: false) |

## Outputs

| Output                 | Description                        |
| ---------------------- | ---------------------------------- |
| `slt-version`          | The slt version installed          |
| `slt-path`             | The slt executable path            |
| `conan-engine-version` | The conan_engine version installed |
| `conan-engine-path`    | The conan_engine executable path   |
| `conan-version`        | The conan version installed        |
| `conan-path`           | The conan executable path          |

## Usage

```yaml
steps:
  - uses: actions/checkout@v4

  - name: Setup SLT (daily channel)
    id: slt-daily
    uses: SiliconLabsInternal/action-setup-slt@main
    with:
      install-conan: true          # optional (default true)
      use-unstable: false          # default, can be omitted

  - name: Setup SLT (unstable channel)
    id: slt-unstable
    if: ${{ always() }} # example of calling again with a different channel
    uses: SiliconLabsInternal/action-setup-slt@main
    with:
      use-unstable: true
      install-conan: true

  - name: Check SLT version (unstable)
    run: |
      echo "(unstable) SLT version: ${{ steps.slt-unstable.outputs.slt-version }}"
      echo "(unstable) SLT path    : ${{ steps.slt-unstable.outputs.slt-path }}"
      echo "conan_engine version  : ${{ steps.slt-unstable.outputs.conan-engine-version }}"
      echo "conan_engine path     : ${{ steps.slt-unstable.outputs.conan-engine-path }}"
      echo "conan version         : ${{ steps.slt-unstable.outputs.conan-version }}"
      echo "conan path            : ${{ steps.slt-unstable.outputs.conan-path }}"
```

### Channels

The action selects between two SLT artifact channels:

* Daily (default): `studio-generic-development/v6/update-sites/daily/tools/slt`
* Unstable (experimental): `studio-generic-development/v6/update-sites/unstable/tools/slt`

Set `use-unstable: true` to target the unstable channel when you need the very latest changes that have not yet stabilized. Leave it `false` (or omit) for routine CI.

## Development

### Prerequisites

- curl

## Contributing

1. Clone the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file
for details.
