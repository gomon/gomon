# gomon

[![Build Status](https://travis-ci.org/gomon/gomon.svg?branch=master)](https://travis-ci.org/gomon/gomon)
[![GoDoc](https://godoc.org/github.com/gomon/gomon?status.svg)](http://godoc.org/github.com/gomon/gomon)

mgo session clone middleware

## Example

Handler for alice to clone sessions and set to context using gorilla/context.

    session, _ := mgo.Dial("127.0.0.1:27017")

    mgoh := gomon.Handler(session, "db_name")
    chain := alice.New(mgoh, ...)

Create your own getter.

    func GetDB(req *http.Request) *mgo.Database {
      return context.Get(req, "db_name").(*mgo.Database)
    }

*The `db_name` is the context key*

Define a context key.

    mgoh := gomon.Handler(session, "db_name", "my_key")

    func GetDB(req *http.Request) *mgo.Database {
      return context.Get(req, "my_key").(*mgo.Database)
    }

Get the db within the middleware chain.

    func(w http.ResponseWriter, req *http.Request) {
      db := GetDB(req)
    }

## License 

MIT