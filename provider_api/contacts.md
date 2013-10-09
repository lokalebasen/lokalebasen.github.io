---
layout: provider_api_sub
---
### Contact Resources

* [Read Contacts](#read_contacts)
* [Read Contact](#read_contact)
* [Create Contact](#create_contact)

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


####<a id="create_contact">Create Contact</a>

POST [ Contact \["contacts"\] \["_links"\] \["self"\] \["href"\] ](#contact_list)

Request body example:

#####Contact Create
<a id="contact_create_request"></a>

{% highlight json %}
{
    "contact": {
        "email": "anders@andersen.dk",
        "password": "secret123",
        "name": "Anders Andersen",
        "phone_number": "12345678",
        "external_key": "Contact 1"
    }
}

{% endhighlight %}

Some of the attributes included in the request body example above are optional.
Check the list below to see details for all fields.

#####<a id="contact_attributes">Contact Attributes</a>
| Field      | Type   | Description | Request/Optional |
| ---------- | ------ | ----------- | ---------------- |
email        | String |             | Required
password     | String | The password used to login to [Lokalebasen Provider Application](http://www.lokalebasen.dk/login). Must be between 6 and 40 characters.| Required
name         | String |             | Required
phone_number | String |             | Required
external_key | String | Providers own reference. Must be unique for all contacts. | Optional

After the request, the api will send a representation of the new contact as the response body.

Response body example:

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
* 201 created
* 400 bad request