# dev/debugging.md

There\'s a lot that happens behind the covers, and Syncthing is generally quite silent about it. A number of environment variables can be used to set the logging to verbose for various parts of the program, and to enable profiling.

Enabling any of the STTRACE facilities will also change the log format to include microsecond timestamps and file names plus line numbers. This can be used to enable this extra information on the normal logging level, without enabling any debugging: `STTRACE=somethingnonexistent` for example.

Under Unix \(including Mac\) the easiest way to run Syncthing with an environment variable set is to prepend the variable to the command line. I.e:

`$ STTRACE=model syncthing`

On windows, it needs to be set prior to running Syncthing.

```text
C:\> set STTRACE=model
C:\> syncthing
```

## Environment Variables

## Stepping with breakpoints

If you like to step through the running program, build a non-optimized binary and run with [https://github.com/derekparker/delve](https://github.com/derekparker/delve).

Follow these steps:

```text
$ go run build.go -debug-binary build
$ STNODEFAULTFOLDER=1 STNOUPGRADE=1  STNORESTART=1 dlv --listen=:2345 --headless=true --api-version=2 exec ./syncthing -- -home=./_test_config -no-browser
```

For installing and using delve itself see:

* VSCode \(Microsoft\):

  [https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code](https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code)

* Goland \(JetBrains\): create remote run configuration and follow the

  two steps displayed

