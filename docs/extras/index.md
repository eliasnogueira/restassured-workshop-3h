# Extras Labs

## Extra Lab 1

In this lab, you need to implement the client and service abstraction for the **Simulations API**

## Extra Lab 2

In this lab, you will create the basic tests for the **Simulations API**.

## Extra exercises

You can add even more tests to exercise your skills.
This is the list of tests you can implement:

### Restrictions tests

| Test | Expected result |
|------|-----------------|
| Find a restriction using the `/v2` endpoint | Response body with `detail` and `returnMessage` attributes |

### Simulations tests

| Test | Expected result |
|------|-----------------|
| Create a new simulation using an existing CPF | HTTP 409 with a custom message in the response body | 
| Delete a simulation that does not exist | HTTP 404 | 
| Update a simulation that does not exist | HTTP 404 | 
| Retrieve a simulation that does not exist | HTTP 404 | 
| Create a simulation with an invalid email | HTTP 422 with a custom message in the response body | 
| Create a simulation with installments less than 2 or greater than 48 | HTTP 422 with a custom message in the response body | 
| Create a simulation with an amount less than 1000 or greater than 40000 | HTTP 422 with a custom message in the response body | 
