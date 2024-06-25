+++
title = 'How to print a struct in Go?'
date = 2024-06-25T22:33:05+02:00
draft = false
tags = ['struct', 'print']
categories = ['go']
summary = """\
    Sometimes it's very useful to be able to display the contents of a variable. \
    On this page, you can find out how to display the contents of a structure in a variable, for example.\
    """
+++

## Introduction

Sometimes it's very useful to be able to display the contents of a variable.

On this page, you can find out how to display the contents of a structure in a variable, for example.

### Beginner, using the `fmt` package

[Go Playground](https://go.dev/play/p/I7c1lgZQfQC)

Use `%+v` in a `fmt.Printf` func.

```go
theStructToPrint := struct {
	Name string
}{
	Name: "Julien",
}
fmt.Printf("%+v\n", theStructToPrint)
```

Output:
```shell
{Name:Julien}
```

### Intermediary, using the `json.Marshal` func

[Go Playground](https://go.dev/play/p/2WJQxhuRS_6)

Use `json.Marshal` func from encoding json package.

```go
theStructToPrint := struct {
	Name string
}{
	Name: "Julien",
}
result, _ := json.Marshal(theStructToPrint)
fmt.Println(string(result))
```

Output:
```shell
{Name:Julien}
```

### Advance, using the `json.MarshalIndent` func

[Go Playground](https://go.dev/play/p/lsr0lAOoy3u)

Use `json.MarshalIndent` func from encoding json package.

```go
theStructToPrint := struct {
	Name string
}{
	Name: "Julien",
}
result, _ := json.MarshalIndent(theStructToPrint, "", "\t")
fmt.Println(string(result))
```

Output:
```shell
{
	"Name": "Julien"
}
```

## Not recommended, using an external package

Because we only need to print the contents of a variable. 
We often avoid multiplying dependencies.

For example, you can use the package `go-spew`.

[Playground](https://go.dev/play/p/40e0VrNtBAC)

Get the package:

```shell
go get -u github.com/davecgh/go-spew/spew
```

```go
theStructToPrint := struct {
	Name string
}{
	Name: "Julien",
}
spew.Dump(theStructToPrint)
```

Output:
```shell
(struct { Name string }) {
 Name: (string) (len=6) "Julien"
}
```