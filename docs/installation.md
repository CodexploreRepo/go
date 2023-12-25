# Go Installation

- Add go's bin folder (`/Users/codexplore/go/bin`) to PATH into `.zshrc`
  - `go env GOPATH` returns `/Users/codexplore/go`

```shell
export PATH=$PATH:$(go env GOPATH)/bin
```
