# Learn golang

Go言語勉強リポジトリ

* `go version go1.12 darwin/amd64`
* [How to Write Go Code - The Go Programming Language](https://golang.org/doc/code.html)

## Build Enviroment and 1st program

* `brew install go`
* write to `~/.bash_profile`
  * `export GOPATH=~/workspaces/golang`
  * `export PATH=$PATH:$GOPATH/bin`
* make directory to become the tree
* make hello.go and write code

```tree
~/workspaces/golang
├── bin
│   └── hello
└── src
    └── github.com
        └── res0nanz(github-username)
            └── golang
                ├── .git
                ├── README.md
                └── hello
                    └── hello.go
```

Q. `git init`をどこでするか？

A. [Where to initialise git in Go project - Stack Overflow](https://stackoverflow.com/questions/29660362/where-to-initialise-git-in-go-project)

* build
  * `go install github.com/username/(golang)/hello`
  * `cd $GOPATH/src/github.com/username/(golang)/hello; go install`
  * `hello`をプロジェクトのルートとするならば`github.com/username/hello`
* run
  * `$GOPATH/bin/hello`
  * `hello`
