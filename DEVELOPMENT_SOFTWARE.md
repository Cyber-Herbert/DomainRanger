# Entwicklungssoftware (WSL Debian)

Stand: 2025-10-18

Ziel: Überblick über die im WSL (Debian 13/trixie) eingerichtete Entwicklungsumgebung, damit klar ist, welche Tools ich direkt nutzen kann.

## C# / .NET
- .NET SDK: 8.0.415 (LTS)
- `dotnet` CLI verfügbar (PATH gesetzt)
- Umgebungsvariablen: `DOTNET_ROOT=$HOME/.dotnet`, `DOTNET_ROOT_X64=$HOME/.dotnet`
- .NET Global Tools (installiert):
  - `dotnet-format`
  - `dotnet-trace`
  - `dotnet-dump`
  - `dotnet-counters`
  - `reportgenerator` (dotnet-reportgenerator-globaltool)
  - `dotnet-sos` (LLDB/SOS-Erweiterung verfügbar)

Prüfen:
- `dotnet --info`
- `dotnet tool list -g`

## C++ Toolchain
- Compiler: GCC 14.2.0 (`gcc`/`g++`), Clang 19.x (`clang`/`clang++`)
- Debugger: GDB 16.x, LLDB 19.x
- Buildsystem: CMake 3.31.x, Ninja 1.12.x
- Build-Helfer: `pkg-config`

Prüfen:
- `g++ --version`, `clang++ --version`, `cmake --version`, `ninja --version`

## Paketmanager (C++)
- vcpkg: installiert unter `~/vcpkg` (Umgebungsvariablen/Path gesetzt)
- Conan 2.x: installiert via `pipx` (Profil detektiert)

Prüfen:
- `~/vcpkg/vcpkg version`
- `conan --version`

## CLI-Extras / Produktivität
- Code-Qualität/Formatierung: `clang-format`
- Suche/Navigation: `ripgrep (rg)`, `fd` (Symlink zu `fdfind`), `fzf`
- Debug/Analyse: `valgrind`, `strace`, `lsof`
- Build-Beschleunigung: `ccache`
- System/Allgemein: `git`, `curl`, `unzip`, `zip`, `ca-certificates`, `gnupg`, `python3`, `pipx`

## Go (Golang)
- Installation: per offizielles Tarball unter `/usr/local/go` (präferiert) oder via APT
- Umgebungsvariablen: `GOROOT=/usr/local/go`, `GOPATH=$HOME/go`, `GOBIN=$GOPATH/bin`, PATH inkl. `GOROOT/bin` und `GOBIN`
- Go-Tools: `gopls` (Language Server), `dlv` (Delve Debugger)

Prüfen:
- `go version`, `gopls version` (oder `gopls -v`), `dlv version`

Prüfen:
- `rg --version`, `fd --version`, `fzf --version`, `valgrind --version`, `ccache --version`

## Samples (unter ~/ws)
- C++: `hello-cpp` (CMake + Ninja) — baubar mit `cmake --build ~/ws/hello-cpp/build`
- C#: `hello-cs` — lauffähig mit `dotnet run` im Projektordner
- Go: `hello-go` — lauffähig mit `go run ~/ws/hello-go`

## Hinweise
- Performance: Projekte unter `$HOME` halten (nicht unter `/mnt/c`).
- VS Code ist optional; kompletter Workflow ist per Terminal möglich.
- Microsoft APT-Repo ist auf Debian 13 derzeit deaktiviert (Signaturen). .NET wird via Script unter `~/.dotnet` bereitgestellt.

## Kurze Befehlsreferenz
- Neues C#-Projekt: `dotnet new console -o app && cd app && dotnet run`
- Neues C++-Projekt (CMake/Ninja): `cmake -S . -B build -G Ninja && cmake --build build`
- CCache in CMake aktivieren: `-DCMAKE_C_COMPILER_LAUNCHER=ccache -DCMAKE_CXX_COMPILER_LAUNCHER=ccache`
