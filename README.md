# 🔬 attest

This is a simple tool to verify the contents of a GitHub release tarball against the original repository.

## 📋 What This Script Does

- Extracts a `.tar.gz` archive.
- Compares each Git-tracked file against its counterpart in the archive.
- Verifies:
  - File content (SHA-256 hash)
  - File permission modes (e.g., `0644`, `0755`)
- Reports:
  - Missing files in the archive
  - Extra files in the archive
  - Mismatches in content or mode

## 🧪 Getting Started

### 🔧 Prerequisites

#### ✅ System Requirements

- **Operating System**: Unix-like system (Linux, macOS, WSL)
- **Bash**: Bash 4.x or higher (required for associative arrays)
- **git**: Used to list and verify tracked files (`git ls-files`)

#### ✅ Required Command-Line Tools

The following standard tools must be available in your system's `PATH`:

| Tool         | Purpose                                   |
|--------------|-------------------------------------------|
| `tar`        | Extract `.tar.gz` files                   |
| `sha256sum`  | Compute and compare file content hashes   |
| `stat`       | Check file permission modes               |
| `realpath`   | Resolve absolute paths                    |
| `find`       | Enumerate files in the archive            |
| `awk`        | Extract values from CLI output            |
| `mktemp`     | Safely create temporary directories       |

##### macOS Users

MacOS includes BSD versions of `stat` and does not include `sha256sum`.
Install GNU core utilities using Homebrew:

```sh
brew install coreutils
```

Then update the script to use:

- `gsha256sum` instead of `sha256sum`
- `gstat` instead of `stat`

## 🚀 Installation

1. **Download the Script**
    Save the [`attest`](./attest) file to your local machine.
2. **Make It Executable**

    ```sh
    chmod +x attest
    ```

## 🏁 Usage

```sh
./attest [-v] <archive.tar.gz> [repo-dir]
```

### Options

- `-v`, `--verbose`: Print each file as it's verified (default: silent unless mismatch occurs)

### Arguments

- `archive.tar.gz`: Path to the `.tar.gz` archive
- `repo-dir` (optional): Path to the Git repository (defaults to `.`)

## ✅ Example

```sh
./attest -v dist/myproject-v1.2.3.tar.gz .
```

Expected output:

```sh
✅ Match: main.go
✅ Match: go.mod
❌ Mismatch: README.md
❌ Extra file in archive not tracked by Git: debug.log
```

## 🛑 Exit Codes

- `0`: All checks passed
- `1`: One or more mismatches found

## 🧹 Cleanup

The script automatically deletes any temporary directories it creates.

## 🙋‍♀️ Need Help?

Feel free to open an issue or reach out with questions!
