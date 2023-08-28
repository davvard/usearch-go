# usearch-go

`usearch-go` is a Go library that provides functionality for creating and utilizing similarity search indexes.

## Installation

```
go get github.com/davvard/usearch-go
```

## Example Usage

```go
package main

import (
	"fmt"
	usearch "github.com/davvard/usearch-go"
)

func main() {
	// Create Index
	conf := usearch.DefaultConfig(128)
	index, err := usearch.NewIndex(conf)
	if err != nil {
		fmt.Println("Failed to create Index")
		return
	}

	// Add to Index
	index.Reserve(1)
	v := make([]float32, 128)
	index.Add(42, v)

	// Search
	keys, distances, err := index.Search(v, 1)
	if err != nil {
		fmt.Println("Failed to search")
		return
	}
	fmt.Println(keys, distances)
}
```


## Linking USearch
```
CGO_ENABLED=1 CGO_LDFLAGS="-L/path/to/lib -lusearch" CGO_CFLAGS="-I/path/to/include" go run example.go 
```

