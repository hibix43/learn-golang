# Note - [How to Write Go Code - The Go Programming Language](https://golang.org/doc/code.html)

## Build Enviroment and 1st program

* `brew install go`
* write to `~/.bash_profile`
  * `export GOPATH=~/workspaces/golang`
  * `export PATH=$PATH:$GOPATH/bin`
* make directory to become the tree below
* make `hello.go` and write the code

```tree
~/workspaces/golang
├── bin
│   └── hello
└── src
    └── github.com
        └── res0nanz(github-username, this repository)
            ├── .git
            ├── README.md
            └── hello
                └── hello.go
```

Q. Where is `.git` directory ?

A. [Where to initialise git in Go project - Stack Overflow](https://stackoverflow.com/questions/29660362/where-to-initialise-git-in-go-project)

* build the hello command (produce binary)
  * `go install github.com/res0nanz/hello`
  * or `cd $GOPATH/src/github.com/res0nanz/hello; go install`
  * Only `hello` directory is root directory, become `github.com/res0nanz/hello`
* run (the binary)
  * `$GOPATH/bin/hello`
  * or `hello`

## 1st library

* `mkdir $GOPATH/src/github.com/res0nanz/stringutil`
* write `stringutil.go`
* `go build (github.com/res0nanz/stringutil)`
  * No output file. It saves the compiled package in local cache
* add `hello.go` import path (`github.com/res0nanz/stringutil`)
  * In `hello.go`, use as `stringutil`
  * Only package name is `stringutil`
  * Package name: `package xxx (1st line in go file)`
  * ex) `stringutil.Reverse()`
* re-install: `go install github.com/res0nanz/hello`
* run new version: `hello`
