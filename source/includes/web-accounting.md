# (web) Accounting

This section contains API to negotiate price lists between coach and client.

<aside class="notice">
User (coach) must be authorized (logged in) before running this API queries.
</aside>

## Get default price list

This is used to obtain the default price list when new price list is created. It either returns default prices or the price list last used by coach.

> To obtain the default price list, perform:

```coffee
$.ajax
  dataType: "json"
  type: "get"
  data:
  url: "http://users.allforbody.pl/accounting/default_price_list.json"
  success: (data, status, jqXHR) ->
    processSomehow(data)
```

> The above command returns JSON structured like this:

```ruby
{
    default_prices:
    {
        calendar_task: 5.0
        calendar_note: 2.0
        calendar_comment: 1.0
        client_wall_message: 2.0
        api_sms_message: 2.0
        currency: NOK
    }
    commission: 20
    available_currencies: [PLN, USD, NOK]
    estimated_amounts: {
        knowledge: 20
        motivaiton: 30
    }
}

```

### HTTP Request

`GET http://users.allforbody.pl/accounting/default_price_list.json`

## Get price list for support

This is used to obtain the price list for the given support, ie. for a given coach-client relation.

> To obtain the default price list, perform:

```coffee
$.ajax
  dataType: "json"
  type: "get"
  data:
    support_id: 8
  url: "http://users.allforbody.pl/accounting/support_price_list.json"
  success: (data, status, jqXHR) ->
    processSomehow(data)
```

> The above command returns JSON structured like this:

```ruby
{
    id: 12
    calendar_task: 5.0
    calendar_note: 2.0
    calendar_comment: 1.0
    client_wall_message: 2.0
    api_sms_message: 2.0
    currency: PLN
    commission: 20
    accepted_at: <<timestamp>>
    rejected_at: nil,
    estimated_amounts: {
        knowledge: 20,
        motivation: 30
    }

}

```

### HTTP Request

`GET http://users.allforbody.pl/accounting/support_price_list.json`


## Create price list
It allows for creating price list for support. Custom message can be passed as :message. The welcome (true/false) decides on the email styling.

> To create a new price list, perform:
```coffee
$.ajax
  dataType: "json"
  type: "post"
  data:
    support_id: 2
    prices:
       calendar_task: 2,
       calendar_note: 2,
       calendar_comment: 2,
       client_wall_message: 2,
       api_sms_message: 2
    welcome: true
    message: "Witaj, będzie się nam fajnie trenowało, yno pierwyj kasa"
    estimated_amounts:
       knowledge: 20,
       motivation: 30
  url: "http://users.allforbody.pl/accounting/price_lists"
  success: (data, status, jqXHR) ->
    processSomehow(data)
```



### HTTP Request

`POST http://users.allforbody.pl/accounting/price_lists`

### Response codes

Code | Description
--------- | -----------
201 |  Successfully created.


### Query Parameters
Price lists can be of 2 types: depending on the number of services (i.e. _standard_) or constant amount of money per month (i.e. _fixed_)

Standard price lists

Parameter | Default | Description
--------- | ------- | -----------
support_id | null | Id of the support between coach and client.
currency | null | Currency for prices
prices/calendar_task | null |
prices/calendar_note | null |
prices/calendar_comment | null |
prices/client_wall_message | null |
prices/api_sms_message | null |
welcome | false | Decides if this is first email for client or not (different design)
message | null | Custom message from coach to client
estimated_amount | null | hash of custom key - values to store

Fixed price lists

Parameter | Default | Description
--------- | ------- | -----------
support_id | null | Id of the support between coach and client.
currency | null | Currency for prices
fixed_price | null | The amount in users currency, eg. 125.0
welcome | false | Decides if this is first email for client or not (different design)
message | null | Custom message from coach to client
estimated_amount | null | hash of custom key - values to store

