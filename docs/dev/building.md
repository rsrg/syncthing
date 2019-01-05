# dev/building.md

## Building Syncthing <a id="building"></a>

::: {.note} ::: {.admonition-title} Note :::

You probably only need to go through the build process if you are going to do development on Syncthing or if you need to do a special packaging of it. For all other purposes we recommend using the official binary releases instead. :::

### Branches and Tags

You should base your work on the `master` branch when doing your development. This branch is usually what will be going into the next release and always what pull requests should be based on.

If you\'re looking to build and package a release of Syncthing you should instead use the latest tag \(`vX.Y.Z`\) as the contents of `master` may be unstable and unsuitable for general consumption.

### Prerequisites

* The latest stable version of Go. Earlier releases may work, but we

  recommend always using the latest stable version. At the time of

  writing this is **Go 1.11**.

* Git

If you\'re not already a Go developer, the easiest way to get going is to download the latest version of Go as instructed in [https://golang.org/doc/install](https://golang.org/doc/install) and `export GOPATH=~/go`.

::: {.note} ::: {.admonition-title} Note :::

You need to set `GOPATH` correctly and the source **must** be checked out into `$GOPATH/src/github.com/syncthing/syncthing`. The instructions below accomplish this correctly. On Go 1.8 and newer you can use the default `GOPATH` of `~/go` instead of setting the environment variable. :::

### Building \(Unix\)

* Install the prerequisites.
* Open a terminal.

\`\`\` {.sourceCode .bash}

## This should output "go version go1.11" or higher.

$ go version

## Go is particular about file locations; use this path unless you know very

## well what you're doing and have set GOPATH to something other than ~/go.

$ mkdir -p ~/go/src/github.com/syncthing $ cd ~/go/src/github.com/syncthing

## Note that if you are building from a source code archive, you need to

## rename the directory from syncthing-XX.YY.ZZ to syncthing

$ git clone [https://github.com/syncthing/syncthing](https://github.com/syncthing/syncthing)

## Now we have the source. Time to build!

$ cd syncthing

## You should be inside ~/go/src/github.com/syncthing/syncthing right now.

$ go run build.go

\`\`\`

Unless something goes wrong, you will have a `syncthing` binary built and ready in `~/go/src/github.com/syncthing/syncthing/bin`.

### Building \(Windows\)

* Install the prerequisites.
* Open a `cmd` Window:

  ```text
  # This should output "go version go1.11" or higher.
  > go version

  # Go is particular about file locations; use this path unless you know very
  # well what you're doing.
  > mkdir %USERPROFILE%\go\src\github.com\syncthing
  > cd %USERPROFILE%\go\src\github.com\syncthing
  # Note that if you are building from a source code archive, you need to
  # rename the directory from syncthing-XX.YY.ZZ to syncthing
  > git clone https://github.com/syncthing/syncthing

  # Now we have the source. Time to build!
  > cd syncthing
  > go run build.go
  ```

Unless something goes wrong, you will have a `syncthing.exe` binary built and ready in `%USERPROFILE%\go\src\github.com\syncthing\syncthing\bin`.

### Subcommands and Options

The following `build.go` subcommands and options exist.

`go run build.go install`

: Installs binaries in `./bin` \(default command, this is what happens when build.go is run without any commands or parameters\).

`go run build.go build`

: Builds just the named target, or `syncthing` by default, to the current directory. Use when cross compiling.

`go run build.go test`

: Runs the tests.

`go run build.go tar`

: Creates a Syncthing tar.gz dist file in the current directory. Assumes a Unixy build.

`go run build.go zip`

: Creates a Syncthing zip dist file in the current directory. Assumes a Windows build.

The options `-no-upgrade`, `-goos` and `-goarch` can be given to influence `install`, `build`, `tar` and `zip`. Examples:

`go run build.go -goos linux -goarch 386 tar`

: Builds a tar.gz distribution of Syncthing for linux-386.

`go run build.go -goos windows -no-upgrade zip`

: Builds a zip distribution of Syncthing for Windows \(current architecture\) with upgrading disabled.

### Building without Git

Syncthing can be built perfectly fine from a source tarball of course. If the tarball is from our build server it contains a file called `RELEASE` that informs the build system of the version being built. If you\'re building from a different source package, for example one automatically generated by Github, you must instead pass the `-version` flag to `build.go`.

If you are building something that will be installed as a package \(Debian, RPM, ...\) you almost certainly want to use `-no-upgrade` as well to prevent the built in upgrade system from being activated.

`go run build.go -version v0.10.26 -no-upgrade tar`

: Builds a tar.gz distribution of Syncthing for the current OS/arch, tagged as `v0.10.26`, with upgrades disabled.
