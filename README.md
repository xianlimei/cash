# Cash

Cash is a super-simple, in-memory key/value cache for Go.

#### Install

    go get github.com/daryl/cash

#### Usage

```go
package main

import (
    "fmt"
    "github.com/daryl/cash"
    "time"
)

var c *cash.Cash

func main() {
    c = cash.New(cash.Conf{
        // Default expiration.
        10 * time.Minute,
        // Clean interval.
        30 * time.Minute,
    })

    // Cache forever (cash.Forever or -1).
    c.Set("foo", "bar", cash.Forever)

    // Default expiration (cash.Default or 0).
    c.Set("abcd", 1234, cash.Default)

    // Custom expiration time.
    c.Set("efgh", 5678, 3 * time.Minute)

    var foo string
    // Since you can store anything in the
    // cache, when you retrieve the value
    // you must use type assertion
    //
    // Also, each time a value is fetched
    // the expiration time will be updated
    // from that point on.
    if v, ok := c.Get("foo"); ok {
        foo = v.(string)
    }

    fmt.Println(foo) // bar
}
```

#### Documentation

For further documentation, check out [GoDoc](http://godoc.org/github.com/daryl/cash).
