# go-casbin-rabc-csv-example
An example of how to use casbin as an RABC service with CSV configuration

# Setup
## Install dependencies
```
$ go install github.com/casbin/casbin/v2@latest
$ go get github.com/casbin/casbin/v2
```

## Compiling
```
$ go build server/main.go
```

# Configuration
The ACL policy is provided in `policy.csv`
```
p, alice, data1, read
p, data2_admin, data2, read
p, data2_admin, data2, write
g, alice, data2_admin
```

The definition of each line within the file defines that:
1. `alice` has `read` access to `data1`
2. `data2_admin` has `read` access to `data2`
3. `data2_admin` has `write` access to `data2`
4. `alice` has `data2_admin` role

# Running
To run the application, execute this following line:
```
$ go run server/main.go <user> <resource> <action>
```

The following table provides the expected result of `go run` execution
| User | Resource | Action | Result |
| --- | --- | --- | --- |
| alice | data1 | read | Access allowed |
| alice | data1 | write | Access denied |
| alice | data2 | read | Access allowed |
| alice | data2 | write | Access allowed |
| bob | data1 | read | Access denied |
