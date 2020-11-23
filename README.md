# Basic Authentication

[![build status](https://img.shields.io/travis/com/kataras/basicauth/main.svg?style=for-the-badge&logo=travis)](https://travis-ci.com/github/kataras/basicauth) [![report card](https://img.shields.io/badge/report%20card-a%2B-ff3333.svg?style=for-the-badge)](https://goreportcard.com/report/github.com/kataras/basicauth) [![godocs](https://img.shields.io/badge/go-%20docs-488AC7.svg?style=for-the-badge)](https://pkg.go.dev/github.com/kataras/basicauth)

The most advanced and powerful Go HTTP middleware to handle basic authentication. It is fully compatible with the [net/http](https://golang.org/pkg/net/http/) package and third-party frameworks.

In the context of an HTTP transaction, basic access authentication is a method for an HTTP user agent (e.g. a web browser) to provide a user name and password when making a request [RFC 7617](https://tools.ietf.org/html/rfc7617).

> Looking for JWT? Navigate [here](https://github.com/kataras/jwt) instead

## Installation

The only requirement is the [Go Programming Language](https://golang.org/dl).

```sh
$ go get github.com/kataras/basicauth
```

Please star this open source project to attract more developers so that together we can improve it even more!

### Examples

- [Basic](_examples/basic/main.go)
- [Load from a slice of Users](_examples/users_list/main.go)
- [Load from a file & encrypted passwords](_examples/users_file_bcrypt/main.go)
- [Fetch & validate a User from a Database (MySQL)](_examples/database)

## Getting Started

Import the package:

```go
import "github.com/kataras/basicauth"
```

Initialize the middleware with a simple map of username:password (see [Options](https://pkg.go.dev/github.com/kataras/basicauth#Options) type and [New](https://pkg.go.dev/github.com/kataras/basicauth#New) function for real-world scenarios):

```go
auth := basicauth.Default(map[string]string{
	"admin":       "admin",
	"my_username": "my_password",
})
```

Wrap any `http.Handler` with the `auth` middleware, e.g. `*http.ServeMux`:

```go
mux := http.NewServeMux()
// [...routes]

http.ListenAndServe(":8080", auth(mux))
```

Or register the middleware to a single `http.HandlerFunc` route:

```go
mux.HandleFunc("/", basicauth.HandlerFunc(auth, routeHandlerFunc))
```

For a more detailed technical documentation you can head over to our [godocs](https://pkg.go.dev/github.com/kataras/basicauth).

## License

This software is licensed under the [MIT License](LICENSE).