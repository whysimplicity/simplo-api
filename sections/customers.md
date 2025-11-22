Customers
==========

Endpoints:

- [Create a customer](#create-a-customer)


Create a customer
-----------------

* `POST /api/v1/customers.json` creates a new customer within the current account.

**Required parameters**:
The request body must contain a JSON object with a `customer` key.
* `name` - The full name of the customer.
* `email` - The primary email address of the customer. Must be unique within the account.
* `identifier` - The customer's document number (e.g., CPF or CNPJ).

_Optional parameters_:
* `external_code` - An identifier for the customer in an external system.
* `phone` - The customer's phone number.
* `address` - A nested object containing address details.
    * `zip_code`
    * `street`
    * `number`
    * `district`
    * `city`
    * `state`
    * `country`
    * `complement`


###### Example JSON Request

``` json
{
  "customer": {
    "name": "João da Silva",
    "email": "joao.silva@example.com.br",
    "identifier": "123.456.789-00",
    "external_code": "USR-456-XYZ",
    "phone": "11999998888",
    "address": {
      "zip_code": "01001-000",
      "street": "Praça da Sé",
      "number": "s/n",
      "district": "Sé",
      "city": "São Paulo",
      "state": "SP",
      "country": "BR",
      "complement": "Lado ímpar"
    }
  }
}
```

This will return `201 Created` with a JSON representation of the newly created customer if the creation was successful.

###### Example JSON Response (Success)
```json
{
  "customer": {
    "id": 101,
    "external_code": "USR-456-XYZ",
    "identifier": "123.456.789-00",
    "name": "João da Silva",
    "email": "joao.silva@example.com.br",
    "address": {
      "zip_code": "01001-000",
      "street": "Praça da Sé",
      "number": "s/n",
      "district": "Sé",
      "city": "São Paulo",
      "state": "SP",
      "country": "BR",
      "complement": "Lado ímpar"
    }
  }
}
```

###### Copy as cURL

``` shell
curl -s -H "Authorization: ApiKey $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{ "customer": { "name": "João da Silva", "email": "joao.silva@example.com.br", "identifier": "123.456.789-00" } }' \
  https://simplo.works/api/v1/customers
```
