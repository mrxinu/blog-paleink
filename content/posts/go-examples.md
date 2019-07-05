---
title: "More SolarWinds Examples"
date: 2017-07-13T00:30:00-07:00
slug: "go-examples"
---

Today I sat down to write a group and dependency creation program for a colleague and
what came out of that were a couple more examples for the [SolarWinds GitHub repository](https://github.com/solarwinds/OrionSDK)
for their API. Of course they both use my SolarWinds package [github.com/mrxinu/gosolar](https://github.com/mrxinu/gosolar)
because why not, right?

These are modeled after the [PowerShell examples](https://github.com/solarwinds/OrionSDK/tree/master/Samples/PowerShell) they already have in place which include
the username and password right there at the top. Of course don't actually put the authentication
in your code if you're following the [12 Factor App](https://12factor.net/config) way of doing things and go with [some environment
variables](https://mrxinu.github.io/post/config-env/) instead.

Here is the actual [pull request](https://github.com/solarwinds/OrionSDK/pull/83) that adds the new
samples.

One of the things I've learned by doing these is to embrace `interface{}` when building these requests
because the types will vary. And thankfully `json.Marshal()` doesn't care what you give it as long as it
can convert it to a valid JSON document. That way the `parentID` and `childID` (integers) can stay integers
even though the rest of the map has string values.

```go
// you would get these using SWQL queries, but we'll set them statically
// as an example
parentID := 1
parentURI := "swis://example.com/Orion/Orion.Nodes/NodeID=1"
parentType := "Orion.Nodes"

childID := 4
childURI := "swis://example.com/Orion/Orion.Nodes/NodeID=4"
childType := "Orion.Nodes"

req := map[string]interface{}{
    "Name":              "Sample Dependency",
    "ParentUri":         parentURI,
    "ChildUri":          childURI,
    "ParentEntityType":  parentType,
    "ChildEntityType":   childType,
    "ParentNetObjectID": parentID,
    "ChildNetObjectID":  childID,
}
```

As I was writing this I also realized that `gosolar` didn't have a `Create()` method yet so I dashed
over there and added one. Since everything is using the unpublished method `post()` ultimately to do the
heavy lifting it was a quick one:

```go
func (c *Client) Create(entity, body interface{}) ([]byte, error) {
    endpoint := fmt.Sprintf("Create/%s", entity)

    return c.post(endpoint, body)
}
```
