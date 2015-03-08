# (web) Clients

## Accepting the regulations
This API provides a call to mark regulations as accepted.
<aside class="notice">
Please note, that the regulations are accepted per role, not per user!
It means, that if a user wants to both coach and be a client, one must accept two types of regulations.
</aside>

> To accept regulations for (authenticated previously) user (client) of ID 5:

```coffee
$.ajax
  dataType: "json"
  type: "put"
  data:
  url: "http://users.allforbody.pl/clients/5/accept_regulations"
  success: (data, status, jqXHR) ->
    processSomehow(data)
```

> To accept regulations for (authenticated previously) coach of ID 5:

```coffee
$.ajax
  dataType: "json"
  type: "put"
  data:
    role: 'coach'
  url: "http://users.allforbody.pl/clients/5/accept_regulations"
  success: (data, status, jqXHR) ->
    processSomehow(data)
```

### HTTP Request

`PUT http://users.allforbody.pl/clients/:ID/accept_regulations`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
role | "client" | The role for which the regulations are accepted.

### Response codes

Code | Description
--------- | -----------
200 |  Regulations accepted.
401 | User role does not exist (see errors key in json).