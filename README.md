# USearch for GoLang

## Installation

```
wget https://github.com/gurgenyegoryan/usearch/releases/download/v0.1.1/usearch.deb
sudo dpkg -i usearch.deb
go get github.com/davvard/usearch-go
```

## Quickstart

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