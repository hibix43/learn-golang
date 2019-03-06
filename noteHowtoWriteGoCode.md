# Note - [How to Write Go Code - The Go Programming Language](https://golang.org/doc/code.html)

## Build Enviroment and 1st program

* `brew install go`
* write to `~/.bash_profile`
  * `export GOPATH=~/workspaces/golang`
  * `export PATH=$PATH:$GOPATH/bin`
* make directory to become the tree below
* make `hello.go` and write the code
* build the hello command (produce binary)
  * `go install github.com/res0nanz/hello`
    * Only `hello` directory is root directory, become `github.com/res0nanz/hello`
  * or `cd $GOPATH/src/github.com/res0nanz/hello; go install`
* run (the binary)
  * `$GOPATH/bin/hello`
  * or `hello`

```tree
~/workspaces/golang
├── bin
│   └── hello
└── src
    └── github.com
        └── res0nanz(github-username, this repository)
            ├── .git
            └── hello
                └── hello.go
```

Q. Where is `.git` directory ?

A. [Where to initialise git in Go project - Stack Overflow](https://stackoverflow.com/questions/29660362/where-to-initialise-git-in-go-project)

## 1st library, Package name

* `mkdir $GOPATH/src/github.com/res0nanz/stringutil`
* write `reverse.go`
* `go build (github.com/res0nanz/stringutil)`
  * No output file. It saves the compiled package in local cache
* add `hello.go` import path (`github.com/res0nanz/stringutil`)
  * Only package name is `stringutil`
  * Package name: `package xxx (1st line in go file)`
  * In `hello.go`, use as `stringutil`
  * ex) `stringutil.Reverse()`
* re-install: `go install github.com/res0nanz/hello`
* run new version: `hello`

## Testing

* Go has a lightweight test framework
* test file
  * Test file name checking `xxx.go` is `xxx_test.go`
  * The file contain a function named `TestXXX`
  * That function's argument is `t *testing.T`
  * In the function, call `t.Errror` or `t.Fail` to cause fail
* make `reverse_test.go` for `stringutil.go`'s `Reverse` function
  * put `reverse_test.go` in `stringutil` directory
* Run test: `go test (github.com/res0nanz/stringutil)`
  * No need to type file name because follow Go rules

```tree
~/workspaces/golang
├── bin
│   └── hello
└── src
    └── github.com
        └── res0nanz
            ├── hello
            │   └── hello.go
            └── stringutil
                ├── reverse.go
                └── reverse_test.go
```

## Remote Package

* An import path describe how to get the package source using Git
* Fetch, build, install package from remote: `go get "repository url"`
  * If getting source from this repository, `go get github.com/res0nanz/learn-golang`
* Use remote official package
  * `go get github.com/golang/example` to get official repository
  * rewrite import path in `hello.go`
  * reisntall `get install github.com/res0nanz/hello`
  * run `hello`

```tree
~/workspaces/golang
├── bin
│   └── hello
└── src
    └── github.com
        ├── golang (official repository)
        │   └── example
        │       ├── stringutil
        │       │   ├── reverse.go
        │       │   └── reverse_test.go
        │       └── etc.
        └── res0nanz (in Github, repository name is "learn-golang")
            ├── hell
            │   └── hello.go
            └── stringutil
                ├── reverse.go
                └── reverse_test.go
```