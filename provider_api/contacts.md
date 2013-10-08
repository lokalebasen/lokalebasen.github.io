---
layout: provider_api_sub
---
### Contact Resources

* [Read Contacts](#read_contacts)
* [Read Contact](#read_contact)

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

The response body consists of a link to itself and the list of contacts. Each contact has a link to its own resource and an external key. To get more details about a given contact, the a GET request must be send to the URL of the given contact in the list (see [Read Contact](#read_contact))

As an example, the URL for the second contact in the list is [ Contacts \["contacts"\] \[1\] \["_links"\] \["self"\] \["href"\] ](#read_contacts).

####Status codes
* 200 OK




####<a id="read_contact">Read Contact</a>

To find a specific contact in the contacts list, a client application should
run through the list of [contacts](#contact_list) until it finds a match
for external_key. Then the client application may follow the self link for
that location to view additional data and options for the location.

GET [ Contacts \["contacts"\] \[index\] \["_links"\] \["self"\] \["href"\] ](#contact_list)

Response body:

{% highlight json %}

{
    "contact": {
        "_links": {
            "self": {
                "href": "http://lokalebasen.dev/api/provider/contacts/82776"
            }
        },
        "name": "Anders Andersen",
        "email": "anders@andersen.dk",
        "phone_number": "12345678",
        "external_key": "Contact 1"
    }
}
{% endhighlight %}

####Status codes
* 200 OK
* 404 Record Not Found

