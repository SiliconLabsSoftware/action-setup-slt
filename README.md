# Setup SLT

This GitHub Action downloads and install SLT, conan_engine and conan

## Features

- Download the latest SLT available
- Installs conan_engine and conan
- Sets the CONAN_HOME env variable to match the slt install and export it
- Exports the path to slt, conan_engine and conan

## Inputs

| Input           | Description                 | Required           |
| --------------- | --------------------------- | ------------------ |
| `install-conan` | Install conan alongside slt | No (default: true) |

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

  - name: Setup SLT
    id: test-action
    uses: SiliconLabsInternal/action-setup-slt@main

  - name: Check SLT version
    run: |
      echo "SLT version installed: ${{ steps.test-action.outputs.slt-version }}"
      echo "SLT executable path : ${{ steps.test-action.outputs.slt-path }}"
      echo "conan_engine version installed: ${{ steps.test-action.outputs.conan-engine-version }}"
      echo "conan_engine executable path: ${{ steps.test-action.outputs.conan-engine-path }}"
      echo "conan version installed: ${{ steps.test-action.outputs.conan-version }}"
      echo "conan executable path: ${{ steps.test-action.outputs.conan-path }}"
```

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
