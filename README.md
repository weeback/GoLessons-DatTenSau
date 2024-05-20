# Lesson 01

## Setup project

* Add config skip IDE directories to `.gitignore` \
  command: `echo "<content>" >> .gitignore`
```shell
echo "
# IDE generate directories
.idea/
.vscode/

# Output binary file built with `go build -o bin/myapp`
bin/
" >> .gitignore
```

* Init go module with name \
  command: `go mod init <app-name-or-path-to-project>
```shell
go mod init myapp
```

* Note:
  >If you use GoLand IDE, please Enable Go modules integration:
  > 
  > Open Setting > Go > Go Modules
  >+ Check to [v] Enable Go modules integration.
  >+ Check to [v] Enable vendoring support automatically.

## Hello World!

* Create main.go file \
  command: `mkdir -p cmd/<app-name-or-version> && echo "<content of file main.go>" >> cmd/<app-name-or-version>/main.go`
```shell
# remove old main.go file
rm -rf cmd/v1/main.go 

# create new main.go file
mkdir -p cmd/v1; echo "package main
  
import \"fmt\"

func main() {
    fmt.Println(\"Hello, world! \")
}
" >> cmd/v1/main.go
```


* Run app \
  command: `go run <path-to-main-package>/main.go`
```shell
go run cmd/v1/main.go
```

## Build app

* Build app \
  command: `go build -o bin/<filename> -trimpath <path-to-main-package>/*.go`
```shell
go build -o bin/myapp \
  -trimpath cmd/v1/main.go
```

* Build app with flags \
  command: `go build -ldflags "-s -w" -o bin/<filename> <path-to-main-package>/*.go`
```shell
go build -ldflags "-s -w" \
  -o bin/myapp \
  -trimpath cmd/v1/main.go
```

* Build app with static built variable \
  command: `go build -ldflags "-s -w -extldflags '-static' -X <package.Variable>=<value>" -o bin/<filename> -trimpath <path-to-main-package>/*.go`
```shell
# Add file static_variable.go; (remove the comment below to execute it)
# echo "package myapp
#
# // Version is the version of the application
# var Version string
# " >> static_variable.go

# From main.go, add the import of the package "myapp" and print the version
# import "myapp"
#
# func main() {
#   fmt.Println(\"Hello, world! \")
#   fmt.Println(\"Version: \", myapp.Version)
# }
#

go build -ldflags "-s -w -extldflags '-static' -X myapp.Version=beta-1.0.0" \
  -o bin/myapp \
  -trimpath cmd/v1/main.go
```

* Run built app \
  command: `./bin/<filename>`
```shell
./bin/myapp
```