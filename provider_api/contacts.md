---
layout: provider_api_sub
---
### Contact Resources

* [Read Contacts](#read_contacts)

####<a id="read_contacts">Read Contacts</a>

GET [Entry \["_links"\] \["contacts"\] \["href"\] ](/provider_api.html#entry_locations)

Response body example:

{% highlight json %}

{
    "_links": {
        "self": {
            "href": "http://www.lokalebasen.dk/api/provider/contacts"
        }
    },
    "contacts": [
        {
            "_links": {
                "self": {
                    "href": "http://www.lokalebasen.dk/api/provider/contacts/82776"
                }
            },
            "external_key": "Contact 1"
        },
        {
            "_links": {
                "self": {
                    "href": "http://www.lokalebasen.dk/api/provider/contacts/97440"
                }
            },
            "external_key": "Contact 2"
        }
    ]
}

{% endhighlight %}

The response body consists of a link to itself and the list of contacts. Each contact has a link to its own resource and an external key. To get more details about a given contact, the a GET request must be send to the URL of the given contact in the list.

As an example, the URL for the second contact in the list is [ Contacts \["contacts"\] \[1\] \["_links"\] \["self"\] \["href"\] ](#read_contacts).

####Status codes
* 200 ok
