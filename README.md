# Sleet

Live infrastructure, written back into code.

Sleet reads the live cloud and updates your Terraform and Hoopoe files so they match. Comments, blank lines, and indentation stay in place.

Documentation: [hoopoelabs.io/docs/sleet](https://hoopoelabs.io/docs/sleet)

## Install

Binaries for the current release, v0.1.2. Each archive contains the `sleet` binary and this README. `checksums.txt` is on the same release.

### macOS (Apple Silicon)

```bash
curl -fsSL -o sleet_0.1.2_darwin_arm64.tar.gz https://github.com/hoopoelabs/sleet-releases/releases/download/v0.1.2/sleet_0.1.2_darwin_arm64.tar.gz
tar -xzf sleet_0.1.2_darwin_arm64.tar.gz
sudo mv sleet /usr/local/bin/
sleet version
```

### macOS (Intel)

```bash
curl -fsSL -o sleet_0.1.2_darwin_amd64.tar.gz https://github.com/hoopoelabs/sleet-releases/releases/download/v0.1.2/sleet_0.1.2_darwin_amd64.tar.gz
tar -xzf sleet_0.1.2_darwin_amd64.tar.gz
sudo mv sleet /usr/local/bin/
sleet version
```

### Linux (x86_64)

```bash
curl -fsSL -o sleet_0.1.2_linux_amd64.tar.gz https://github.com/hoopoelabs/sleet-releases/releases/download/v0.1.2/sleet_0.1.2_linux_amd64.tar.gz
tar -xzf sleet_0.1.2_linux_amd64.tar.gz
sudo mv sleet /usr/local/bin/
sleet version
```

### Linux (ARM64)

```bash
curl -fsSL -o sleet_0.1.2_linux_arm64.tar.gz https://github.com/hoopoelabs/sleet-releases/releases/download/v0.1.2/sleet_0.1.2_linux_arm64.tar.gz
tar -xzf sleet_0.1.2_linux_arm64.tar.gz
sudo mv sleet /usr/local/bin/
sleet version
```

### Windows (x86_64)

```powershell
Invoke-WebRequest -Uri https://github.com/hoopoelabs/sleet-releases/releases/download/v0.1.2/sleet_0.1.2_windows_amd64.zip -OutFile sleet_0.1.2_windows_amd64.zip
Expand-Archive -Path sleet_0.1.2_windows_amd64.zip -DestinationPath .
Move-Item -Path .\sleet.exe -Destination C:\Windows\System32\sleet.exe
sleet version
```

### Windows (ARM64)

```powershell
Invoke-WebRequest -Uri https://github.com/hoopoelabs/sleet-releases/releases/download/v0.1.2/sleet_0.1.2_windows_arm64.zip -OutFile sleet_0.1.2_windows_arm64.zip
Expand-Archive -Path sleet_0.1.2_windows_arm64.zip -DestinationPath .
Move-Item -Path .\sleet.exe -Destination C:\Windows\System32\sleet.exe
sleet version
```

## Use

Sleet needs `terraform` or `tofu` on your `PATH`, cloud credentials in the environment, and a directory where `terraform init` has already been run.

Preview a reconciliation:

```bash
sleet sync --dry-run --diff
```

Write live values into the local files:

```bash
sleet sync
```

Fail a CI job when drift exists:

```bash
sleet sync --check --dry-run
```

Root module files are always writable. To allow edits inside a child module, add `.sleetrc` next to the configuration:

```json
{
  "module_write": ["vpc", "vpc.public"]
}
```

`vpc` and `vpc.public` are exact module paths. Listing `vpc` does not include `vpc.public`.

## License

Apache 2.0. Copyright (c) Hoopoe Labs.
