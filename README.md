# 🍕 A Pizza API Kata

Write yourself an API to make a pizza in `ASP.Net`.

This project includes tests to validate your API. Run them using `dotnet test ./APizzaApi.Tests/`. The `/APizzaApi.Api` directory contains the default `ASP.Net` web API template project. Change this project to solve the tests!

Instructions for the API design are below.

## API

The API you write must...

### PUT to create a new pizza order

``` text
PUT: /pizza
BODY: pizza
```

The `/pizza` route must take a `PUT` request with a `JSON` body matching the [pizza object](#the-pizza-object).

#### Response

If the pizza object is correctly formatted, create the pizza and store it somewhere for retrieval. You can choose whether to just store the data in memory for that session (this will please the tests) or push yourself to store the pizza data more permanently in a database.

The response should include the `price` of the pizza based on the tables in [Calculating pizza price](#calculating-pizza-price) and a "pizza identification number" or `pid`. This string should be unique for each pizza. It can be used to read, update, or delete a pizza.

``` json
Status: 201 Created
{
  "price": number,
  "pid": string,
  "pizza": pizza
}
```

### PATCH to add a topping to a pizza

Using the pizza identification number, add a topping to the pizza.

``` text
PATCH: /pizza/{pid}/toppings
BODY: { "sauce" | "cheese" | "pepperoni" | "peppers" | "onions" }
```

#### Response

``` json
Status: 200 OK
{
  "price": number,
  "pid": string,
  "pizza": pizza
}
```

### DELETE to remove a topping from a pizza

Using the pizza identification number, add a topping to the pizza.

``` text
DELETE: /pizza/{pid}/toppings
BODY: { "sauce" | "cheese" | "pepperoni" | "peppers" | "onions" }
```

#### Response

``` json
Status: 200 OK
{
  "price": number,
  "pid": string,
  "pizza": pizza
}
```

### HEAD check if a pizza exists

``` text
HEAD /pizza/{pid}
```

#### Response

If the pizza exists

``` json
Status: 200 OK
```

otherwise

``` json
Status: 404 NOT FOUND
```

### GET info on a pizza

``` text
GET /pizza/{pid}
```

#### Response

``` json
Status: 200 OK
{
  "price": number,
  "pid": string,
  "pizza": pizza
}
```

### DELETE to cancel a pizza order

``` text
DELETE /pizza/{pid}
```

#### Response

If the pizza exists

``` json
Status: 200 OK
```

otherwise

``` json
Status: 404 NOT FOUND
```

## The `pizza` object

``` json
{
  "size": {"small" | "medium" | "large"},
  "toppings": [
    "sauce", "cheese", "pepperoni", "peppers", "onions"
  ],
}
```

## Calculating pizza price

The price of a pizza depends on its size and the toppings on it.

| Size   | Price (USD) |
| ------ | ----------- |
| small  | 10.00       |
| medium | 13.00       |
| large  | 16.00       |

| Topping   | Price (USD) |
| --------- | ----------- |
| sauce     | 0.50        |
| cheese    | 0.70        |
| pepperoni | 1.20        |
| peppers   | 1.20        |
| onions    | 1.20        |
