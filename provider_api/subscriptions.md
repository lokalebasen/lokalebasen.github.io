---
layout: provider_api_sub
---
## Subscription Resources

* [Read Subscriptions](#read_subscriptions)
* [Read Subscription](#read_subscription)
* [Create Subscription](#create_subscription)
* [Delete Subscription](#delete_subscription)

## <a id="subscriptions_intro">Subscriptions</a>

Subscriptions allow additional contacts to receive leads on a particular location. The subscribing contacts are not
revealed to the client, but receives e-mails whenever a client requests information on the particular location.

### <a id="read_subscriptions">Read Subscriptions</a>

GET Location \["location"\] \["_links"\] \["subscriptions"\] \["href"\]

Response body example:

{% highlight json %}
{
  "_links":{
    "self":{
      "href":"http://www.lokalebasen.dk/api/provider/locations/7569/subscriptions"
    }
  },
  "subscriptions":[
    {
      "_links":{
        "self":{
          "href": "http://www.lokalebasen.dk/api/provider/subscriptions/13473"
        },
        "contact": {
          "href": "http://www.lokalebasen.dk/api/provider/contacts/15965"
        }
      },
      "contact": "http://www.lokalebasen.dk/api/provider/contacts/15965"
    },
    {
      "_links":{
        "self":{
          "href":"http://www.lokalebasen.dk/api/provider/subscriptions/13472"
        },
        "contact": {
          "href": "http://www.lokalebasen.dk/api/provider/contacts/4595"
        }
      },
      "contact": "http://www.lokalebasen.dk/api/provider/contacts/4595"
    },
    {
      "_links":{
        "self":{
          "href":"http://www.lokalebasen.dk/api/provider/subscriptions/13471"
        },
        "contact": {
          "href": "http://www.lokalebasen.dk/api/provider/contacts/26615"
        }
      },
      "contact": "http://www.lokalebasen.dk/api/provider/contacts/26615"
    }
  ]
}
{% endhighlight %}

The response body consists of a link the resource itself and a list of subscriptions. Each subscription has a link to its subscribing contact.

#### Status codes

* 200 OK

### <a id="read_subscription">Read Subscription</a>

GET Subscriptions \["subscriptions"\] \[index\] \["_links\] \["self"\] \["href"\]

Response body example:

{% highlight json %}
{
  "subscription": {
    "_links": {
      "self": {
          "href": "http://www.lokalebasen.dk/api/provider/subscriptions/13470"
      },
      "contact": {
          "href": "http://www.lokalebasen.dk/api/provider/contacts/80"
      },
      "location": {
          "href": "http://www.lokalebasen.dk/api/provider/locations/7569"
      }
    },
    "contact": "http://www.lokalebasen.dk/api/provider/contacts/80"
  }
}
{% endhighlight %}

#### Status codes

* 200 OK

### <a id="create_subscription">Create Subscription</a>

POST Location \["location"\] \["_links"\] \["subscriptions"\] \["href"\]

Request body example:

{% highlight json %}
{
  "contact": "http://www.lokalebasen.dk/api/provider/contacts/82776"
}
{% endhighlight %}

This action is idempotent. If the contact already subscribes to the location, 201 will be returned.

Response body example:

{% highlight json %}
{
  "subscription": {
    "_links": {
      "self": {
        "href": "http://www.lokalebasen.dk/api/provider/subscriptions/13360"
      },
      "contact": {
        "href": "http://www.lokalebasen.dk/api/provider/contacts/82776"
      },
      "location": {
        "href": "http://www.lokalebasen.dk/api/provider/locations/7569"
      }
    },
    "contact": "http://www.lokalebasen.dk/api/provider/contacts/82776"
  }
}
{% endhighlight %}

#### Status codes

* 201 Created
* 400 Bad Request
* 422 Unprocessable Entity

### <a id="delete_subscription">Delete Subscription</a>

DELETE Subscriptions \["subscriptions"\] \[index\] \["_links\] \["self"\] \["href"]

#### Status codes

* 204 No Content
* 400 Bad Request
* 422 Unprocessable Entity
