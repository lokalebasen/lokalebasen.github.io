---
layout: provider_api
---
The purpose of this document is to help developers build client applications
that integrate with Lokalebasen.dk through Lokalebasen.dk Provider API.
Thereby allowing providers to automatically and continuously update data
on Lokalebasen.dk.

* [Contact](#contact_)
* [Architecture](#architecture_)
* [Getting Access](#getting_access)
* [Headers](#headers_)
* [Media Types](#media_types)
* [Error Handling](#error_handling)
* [API resource documentation](#api_resource_documentation)



###<a id="contact_">Contact</a>

Any questions, suggestions or other may be send to api@lokalebasen.dk .



###<a id="architecture_">Architecture</a>

As a part of the Lokalebasen.dk B2B strategy, a RESTful API is being used.
REST libraries are available for the most common programming languages such
as Java, C#, Javascript, PHP, Python and Ruby.

Lokalebasen.dk Provider API is a hypermedia API, meaning that it allows
client applications to browse through information much like a human user
browses through the internet.
The client should begin any operation at the entry of the API at
http://www.lokalebasen.dk/api/provider and then follow link after link until
a link to the desired resource is found.
The link keys will remain unchanged. Some URLs will definately change over
time.
Client applications should not store any URLs apart from the entry URL
mentioned above.

Instead of using the absolute paths, this document explains where in a
reponse body an URL is found.
This is done to stress that URLs should not be hardcoded.

A successful GET request on the location resource will produce a json
response body. The top of which may appear as shown below:

####Example
<a id="syntax_example"></a>

{% highlight json %}
{
    "location": {
        "_links": {
            "self": {
                "href": "http://www.lokalebasen.dk/api/provider/locations/8289"
            }
        }
    }
}
{% endhighlight %}

When explaining how to reload the location ( which the link in the json above
may be used for ) the documentation will use the following syntax:
GET [ Example \["location\] \["_links"\] \["self"\] \["href"\] ](#syntax_example) .
Meaning, in this example, that the client needs to
`GET http://www.lokalebasen.dk/api/provider/locations/8289`.
Whenever this syntax is used it will link to the json response where the link
can be found.


###<a id="getting_access">Getting Access</a>

Getting access to Lokalebasen.dk Provider API is easy. Just follow the few
steps below and you are ready to go.

* Create a provider profile on Lokalebasen.dk.
* Call us at (+45) 70 20 08 14 and request access to the API.
* You will then receive an email with your `Api-Key`.

The `Api-Key` goes into the header of all requests to the API
( see [Headers](#headers_) ).



###<a id="headers_">Headers</a>

Every request sent to the API must include `Api-Key` and `Content-Type` in
header.

#####Header Requirements

| Header | Value |
| --- | ----- |
Api-Key| < providers 40 hex characters key >
Content-Type|application/json



###<a id="media_types">Media Types</a>

The API uses `application/json` media type. `application/xml` is not supported.




###<a id="error_handling">Error Handling</a>

Possible status codes and error messages are listed under each resource chapter.

Except for 5xx errors, all error messages are returned in json as the value to
the key: `message` ( see example below ).

{% highlight json %}
{
    "message": "Record not found!"
}
{% endhighlight %}

If Lokalebasen.dk Provider API is having trouble, you may see a 5xx error.
`500` can mean that the server is down, but you may also see
`502 Bad Gateway`, `503 Service Unavailable`, or `504 Gateway Timeout`.
It's the clients responsibility in all of these cases to retry your request
later.




###<a id="api_resource_documentation">API Resource Documentation</a>

* [Entry Point](#entry_point)
* [Location Resources](/provider_api/locations.html)

####<a id="entry_point">Entry Point</a>

The only URL in the API that is certain not to change is the API entry
point.
This URL should be hard coded into the client application. The entry point exposes
the URLs for accessing the [location resources](/provider_api/locations.html).

GET http://www.lokalebasen.dk/api/provider

Response body example:

####Entry:
<a id="entry_locations"></a>

{% highlight json %}
{
    "_links": {
        "clients": {
            "href": "http://www.lokalebasen.dk/api/provider/clients.json"
        },
        "locations": {
            "href": "http://www.lokalebasen.dk/api/provider/locations.json"
        },
        "orders": {
            "index": {
                "href": "http://www.lokalebasen.dk/api/provider/orders.json"
            },
            "index_for": {
                "href": "http://www.lokalebasen.dk/api/provider/orders/index_for.json"
            }
        }
    }
}
{% endhighlight %}

####Status codes
* 200 ok
