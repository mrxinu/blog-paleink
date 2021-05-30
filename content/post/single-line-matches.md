---
title: "Single-Line Matches"
date: 2019-03-05T19:10:00-08:00
slug: "single"
---

I feel like I've had to learn this particular lesson multiple times so I'm
blogging about it for reference.

If you have a Cisco configuration and you're trying to match only interfaces
where a particular command exists, you can do it with the `(?s)` or single-line
flag in the regular expression to span the newlines with wildcards.

Sample Configuration:

```plain
interface Vlan23
 ip address 198.51.100.10 255.255.255.0
 no ip redirects
 no ip proxy-arp
 ip ospf hello-interval 1
 ip ospf cost 15
!
interface Vlan801
 ip address 198.51.100.10 255.255.255.0
 ip helper-address 198.51.100.99
 ip helper-address 198.51.100.100
 no ip redirects
 no ip proxy-arp
!
```

Since I can match from the interface start to the `!` at the end and look
through the former to see if it has the string `ip helper-address` in it before
taking the latter, this code works out:

```go
func getInterfacesWithHelpers(config string) []string {
	re := regexp.MustCompile(`(?s)interface (\S+).*?\n!\n`)

	matches := re.FindAllStringSubmatch(config, -1)

	interfaces := make([]string, 0)
	for _, match := range matches {
		if strings.Contains(match[0], "ip helper-address") {
			interfaces = append(interfaces, match[1])
		}
	}

	return interfaces
}
```
