# gow

gow is a command line program to watch go files changes to re-build or to re-run tests.

Uses <https://github.com/gopsql/watch>.

Install:

```
go install -v github.com/gopsql/gow@latest
```

Usage:

```
Usage: gow [options] -- [go build/test args] -- [app run args]

Options:
  -cd string
        set working directory of commands
  -clean
        run go clean -cache or -testcache (if -test) first
  -ext value
        add extra file extensions to watch (default .go, .mod)
  -go string
        path to the go executable
  -ignore value
        add extra directory name to ignore (default node_modules, .git, dist)
  -no-run
        do not run the executable after go build
  -prebuild string
        run command before go build or go test
  -rebuild-key string
        key to rebuild (default "r")
  -test
        run go test instead of go build
```

Run:

```
# this watches all go files in current directory:
gow

# gow by default ignores node_modules, .git, dist,
# to ignore extra directory names:
gow -ignore vendor -ignore another-dir

# to add extra go build arguments:
gow -- -v -race -o another-name

# to add extra app run arguments:
gow -- -v -race -o another-name -- --custom-flag-of-my-app

# clean test cache before running "go test -v ./..." in "tests" directory
gow -cd tests -test -clean -- -v ./...

# --no-run
GOOS=js GOARCH=wasm gow --no-run -- -o my.wasm -v

# run extra command before build
gow -prebuild "swag init --markdownFiles docs" -- -v -race
```
