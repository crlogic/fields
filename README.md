[![Go](https://github.com/crlogic/fields/actions/workflows/go.yml/badge.svg)](https://github.com/crlogic/fields/actions/workflows/go.yml)
![coverage](https://raw.githubusercontent.com/crlogic/fields/badges/.badges/main/coverage.svg)
[![Go Report Card](https://goreportcard.com/badge/github.com/crlogic/fields)](https://goreportcard.com/report/github.com/crlogic/fields)
![version](https://img.shields.io/github/v/release/crlogic/fields)
# fields
Rest Partial Response (aka Field Selection) Pattern middleware for [Gin](https://gin-gonic.com/). This gin middleware allows you to select a subset of fields to be returned from your endpoints.

e.g. Imagine that you have the following rest endpoint that returns a product with the fields, `code, price, description, manufacturedBy`:
> /products/1
```json
{
 "code": "1",
 "price": "200",
 "description": "Very nice product",
 "manufacturedBy": "company"
}
```
We can call the endpoint and, with the query parameter fields, filter out the fields that we are interested:
> /products/1?**fields=code,price**
```json
{
 "code": "1",
 "price": "200"
}
```

## 📝 How To Install It And Use It

- Run the command:

> go get -u -d github.com/crlogic/fields

- Add fields middleware
```go
r := gin.Default()
r.Use(fields())
```

- Call your endpoints adding the query parameter `fields` with the fields you want to filter:

> /users/1?**fields=name,surname**


## ✨ Features

- [Support for multiple fields filtering](./examples/simple). 

> /users/manuel?fields=name,surname
```json
{
 "name": "Manuel",
 "surname": "Example"
}
```

- [Support for arrays](./examples/simple-array)

> /users?fields=name
```json
[
  {
    "name": "Manuel"
  }
]
```

- [Support for nested jsons](./examples/nested).

> /users/manuel?fields=name,surname,address(street,number)
```json
{
 "name": "Manuel",
 "surname": "Example",
 "address": {
   "street": "mystreet",
   "zipcode": "myzipcode"
 }
}
```

- [Support for wrapped json](./examples/wrapped). 
> /users/manuel?fields=name
```json
{
 "data": {
    "name": "Manuel"
 }
}
```

- [Middleware applied to route groups with different configuration](./example/routeGroups)

fields middleware, as any other gin middleware, can be applied to different route groups with different configurations.

## 🤝 Contributing

Feel free to create a PR or suggest improvements or ideas.

## 🔗 Contact

- 📧 manueldoncelmartos@gmail.com
