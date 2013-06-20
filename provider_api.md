--
layout: default
--
Lokalebasen.dk Provider API Documentation
======================================

The purpose of this document is to help developers build client applications that integrate with Lokalebasen.dk through Lokalebasen.dk Provider API. Thereby allowing providers to automatically and continuously update data on Lokalebasen.dk.

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

As a part of the Lokalebasen.dk B2B strategy, a RESTful API is being used. REST libraries are available for the most common programming languages such as Java, C#, Javascript, PHP, Python and Ruby.  

Lokalebasen.dk Provider API is a hypermedia API, meaning that it allows client applications to browse through information much like a human user browses through the internet.  
The client should begin any operation at the entry of the API at http://www.lokalebasen.dk/api/provider and then follow link after link until a link to the desired resource is found.  
The link keys will remain unchanged. Some URLs will definately change over time.  
Client applications should not store any URLs apart from the entry URL mentioned above.  

Instead of using the absolute paths, this document explains where in a reponse body an URL is found.
This is done to stress that URLs should not be hardcoded.

A successful GET request on the location resource will produce a json response body. The top of which may appear as shown below:

######Example
<pre>
{
    "location": {
        "_links": {
            "self": {<a id="syntax_example"></a>
                "href": "http://www.lokalebasen.dk/api/provider/locations/8289"
            },
            ...
}
</pre>

When explaining how to reload the location ( which the link in the json above may be used for ) the documentation will use the following syntax:  
GET [ Example \["location\] \["_links"\] \["self"\] \["href"\] ](#syntax_example)  
Meaning, in this example, that the client needs to GET http://www.lokalebasen.dk/api/provider/locations/8289.  
Whenever this syntax is used it will link to the line it refers to in a json example.



###<a id="getting_access">Getting Access</a>

Getting access to Lokalebasen.dk Provider API is easy. Just follow the few steps below and you are ready to go.

* Create a provider profile on Lokalebasen.dk.
* Call us at (+45) 70 20 08 14 and request access to the API.
* You will then receive an email with your `Api-Key`.

The `Api-Key` goes into the header of all requests to the API ( see [Headers](#headers_) ).



###<a id="headers_">Headers</a>

Every request sent to the API must include `Api-Key` and `Content-Type` in header.

#####Header Requirements

| Header | Value |
| --- | ----- |
Api-Key| < providers 40 hex characters key >
Content-Type|application/json



###<a id="media_types">Media Types</a>

The API uses `application/json` media type. `application/xml` is not supported.




###<a id="error_handling">Error Handling</a>

Possible status codes and error messages are listed under each resource chapter.

Except for 5xx errors, all error messages are returned in json as the value to the key: `message` ( see example below ).

<pre>
{
    "message": "Record not found!"
}
</pre>
If Lokalebasen.dk Provider API is having trouble, you might see a 5xx error. `500` might mean that the app is entirely down, but you may also see `502 Bad Gateway`, `503 Service Unavailable`, or `504 Gateway Timeout`. It's your responsibility in all of these cases to retry your request later.




###<a id="api_resource_documentation">API Resource Documentation</a>

* [Locations Entry Point](#locations_entry_point)
* [Read Locations](#read_locations)
* [Read Location](#read_location)
* [Create Location](#create_location)
* [Update Location](#update_location)
* [Activate Location](#activate_location)
* [Deactivate Location](#deactivate_location)
* [Create Photo](#create_photo)
* [Delete Photo](#delete_photo)
* [Create Floor Plan](#create_floor_plan)
* [Delete Floor Plan](#delete_floor_plan)
* [Create Prospectus](#create_prospectus)
* [Delete Prospectus](#delete_prospectus)
* [Read job](#read_job)




####<a id="locations_entry_point">Locations Entry Point</a>

The only URL in the API that is certain not to change is the API entry point - e.g. http://www.lokalebasen.dk/api/providers.  
This URL should be hard coded into the client application.  

GET http://www.lokalebasen.dk/api/provider  

Response body example:

######Entry:
<pre>
{
    "_links": {
        "clients": {
            "href": "http://www.lokalebasen.dk/api/provider/clients.json"
        },
        "locations": {<a id="entry_locations"></a>
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
</pre>

######Status codes
* 200 ok




####<a id="read_locations">Read Locations</a>

GET [Entry \["_links"\] \["locations"\] \["href"\] ](#entry_locations)  

Response body example:

######Locations
<pre>
{
    "_links": {
        "self": {<a id="locations_resource"></a>
            "href": "http://www.lokalebasen.dk/api/provider/locations"
        }
    },
    "locations": [ <a id="location_list"></a>
            {
                "_links": {
                    "self": {
                        "href": "http://www.lokalebasen.dk/api/provider/locations/8250"
                    }
                },
                "id": 8250,
                "street_name": "Somewhere",
                "house_number": "5",
                "floor": "1",
                "side": "th",
                "postal_code": 1371,
                "area_from": 334,
                "area_to": null,
                "postal_district_name": "København K",
                "state": "closed",
                "kind": "office",
                "external_key": "Location 2"
            },
            {
                "_links": {<a id="location_8289_in_list"></a>
                    "self": {
                        "href": "http://www.lokalebasen.dk/api/provider/locations/8289"
                    }
                },
                "id": 8289,
                "street_name": "Main Street",
                "house_number": "5",
                "floor": "1",
                "side": "th",
                "postal_code": 1371,
                "area_from": 334,
                "area_to": 370,
                "postal_district_name": "København K",
                "state": "new",
                "kind": "office",
                "external_key": "Location 45"
            }
        ]
}
</pre>

The response body consists of a link to this resource and a list of all providers locations.  
The [ Locations \["_links"\] \["self"\] \["href"\] ](#locations_resource) can be used to reload the list of locations. It can also be used to POST data to create a new location ( see [Create Location](#create_location) ).  

Each location in the list has a link to its own resource. The URL for the second location in the list above is found at [Locations \["locations"\] \[1\] \["_links"\] \["self"\] \["href"\]  ](#location_8289_in_list). Use the GET method on these URLs  to see more details about a given location ( see [Read Location](#read_location) ).  
The external_key value is providers own reference to a location used to find the desired location.  

######Status codes
* 200 ok




####<a id="read_location">Read Location</a>

To find a specific location in the locations list a client application should run through the list of [locations](#location_list) until it finds a match for external_key. Then the client application may follow the self link for that location to view additional data and options for the location.

GET [ Locations \["locations"\] \[index\] \["_links"\] \["self"\] \["href"\] ](#location_8289_in_list)  

Response body:

######Location
<pre>
{<a id="location"></a>
    "location": {<a id="location_key"></a>
        "_links": {<a id="links"></a>
            "self": {<a id="location_8289"></a>
                "href": "http://www.lokalebasen.dk/api/provider/locations/8289"
            },
            "prospectuses": {<a id="location_8289_prospectuses"></a>
                "href": "http://www.lokalebasen.dk/api/provider/locations/8289/prospectuses"
            },
            "photos": {<a id="location_8289_photos"></a>
                "href": "http://www.lokalebasen.dk/api/provider/locations/8289/photos"
            },
            "floor_plans": {<a id="location_8289_floor_plans"></a>
                "href": "http://www.lokalebasen.dk/api/provider/locations/8289/floor_plans"
            },
            "activation": {<a id="location_8289_activation"></a>
                "href": "http://www.lokalebasen.dk/api/provider/locations/8289/activation"
            }
        },
        "title": "Beautiful place by the lake",
        "description": "Old building...\n\nIn the old center",
        "street_name": "Main Street",
        "house_number": "5",
        "floor": "1",
        "side": "th",
        "postal_code": 1371,
        "latitude": 52.145,
        "longitude": 12.813,
        "state": "new",
        "kind": "office",
        "area_from": 334,
        "area_to": 370,
        "external_key": "Location 45",
        "provider_website_link": "http://www.provider.com/location1",
        "yearly_rent_per_m2_from": {
            "cents": 117300,
            "currency": "DKK"
        },
        "photos": [
            {
                "_links": {<a id="photo_5"></a>
                    "self": {
                        "href": "http://www.lokalebasen.dk/api/provider/photos/142968"
                    }
                },
                "external_key": "Photo 5",
                "url": "http://www.lokalebasen.dk/uploads/0014/2968/tokay.png"
            },
            {
                "_links": {
                    "self": {
                        "href": "http://www.lokalebasen.dk/api/provider/photos/142969"
                    }
                },
                "external_key": "Photo 7",
                "url": "http://www.lokalebasen.dk/uploads/0014/2969/tokay.png"
            }
        ],
        "floor_plans": [
            {
                "_links": {<a id="floor_plan_1"></a>
                    "self": {
                        "href": "http://www.lokalebasen.dk/api/provider/floor_plans/142971"
                    }
                },
                "external_key": "Floor Plan 1",
                "url": "http://www.lokalebasen.dk/uploads/0014/2971/1_full.jpg"
            }
        ],
        "yearly_rent_per_m2_to": {
            "cents": 137300,
            "currency": "DKK"
        },
        "yearly_operational_cost_per_m2_from": {
            "cents": 39500,
            "currency": "DKK"
        },
        "yearly_operational_cost_per_m2_to": {
            "cents": 49500,
            "currency": "DKK"
        },
        "prospectus": {
            "_links": {<a id="prospectus_1"></a>
                "self": {
                    "href": "http://www.lokalebasen.dk/api/provider/prospectuses/142973"
                }
            },
            "external_key": "Prospectus 2",
            "url": "http://www.lokalebasen.dk/uploads/0014/2973/sample.pdf"
        }
    }
}
</pre>



The list of [links](#links) shows what you can do with a location.

* GET [ Location \["location\] \["_links"\] \["self"\] \["href"\] ](#location_8289) to reload location.
* PUT [ Location \["location\] \["_links"\] \["self"\] \["href"\] ](#location_8289) to [update location](#update_location).
* PUT [ Location \["location\] \["_links"\] \["activation"\] \["href"\] ](#location_8289_activation) to [activate location](#activate_location). This link is only available when `state` is "new" or "closed".
* PUT [ Location \["location\] \["_links"\] \["deactivation"\] \["href"\] ](#location_8289_deactivation) to [deactivate location](#deactivate_location). This link is only available when `state` is "active".
* POST [ Location \["location\] \["_links"\] \["photos"\] \["href"\] ](#location_8289_photos) to [create photos](#create_photo) for location.
* POST [ Location \["location\] \["_links"\] \["floor_plans"\] \["href"\] ](#location_8289_floor_plans) to [create floor_plan](#create_floor_plan) for location.
* POST [ Location \["location\] \["_links"\] \["prospectuses"\] \["href"\] ](#location_8289_prospectuses) to [create prospectus](#create_prospectus) for location.

######Status codes
* 200 ok
* 404 record not found

####<a id="create_location">Create Location</a>

POST [ Location \["location"\] \["_links"\] \["self"\] \["href"\] ](#locations_resource)  

Request body example:


######Location Create
<a id="location_create"></a>

<pre>
{
    "location": {
        "external_key": "Location 3",
        "title": "Beautiful place by the lake",
        "description": "Old building...\n\nIn the old center",
        "street_name": "Main Street",
        "house_number": "5",
        "postal_code": "1371",
        "floor": "1",
        "side": "th",
        "area_from": 334,
        "area_to": 370,
        "kind": "office",
        "latitude": 52.145,
        "longitude": 12.813,
        "provider_website_link": "http://www.provider.com/location1",
        "yearly_rent_per_m2_from": {
            "cents": 117300,
            "currency": "DKK"
        },
        "yearly_rent_per_m2_to": {
            "cents": 137300,
            "currency": "DKK"
        },
        "yearly_operational_cost_per_m2_from": {
            "cents": 39500,
            "currency": "DKK"
        },
        "yearly_operational_cost_per_m2_to": {
            "cents": 49500,
            "currency": "DKK"
        }
    }
}
</pre>

Some of the attributes included in the request body example above are optional. Check the list below to see details for all fields.

#####<a id="location_attributes">Location Attributes</a>

| Field  | Type | Description | Required/Optional |
| ------ | ---- | ----------- | ----------------- |
area_from|Integer|Minimum area in m2.|Required
area_to|Integer|Maximum area in m2. Must be more than area_from.|Optional
description|String|A detailed description of the location. Use \n for new line.|Optional
external_key|String|Providers own reference. Must be unique for a given resource. E.g. a provider can only have one photo with an external_key called "1", but he may also have a floor plan with an external_key called "1"|Optional
floor|String|Floor.|Optional
house_number|String|House number.|Required
kind|String|Type ("office", "warehouse" or "store").|Required
latitude|Float|Latitude ( e.g. 55.6012 ). Must be within the area of Denmark ( 54.2000 - 57.9000 ).|Required
longitude|Float|Longitude ( e.g. 11.6121 ). Must be within the area of Denmark ( 7.8000 - 15.4000 ).|Required
postal_code|String|A valid zip-code for the country of the location.|Required
provider_website_link|String|A link to the location representation on providers own website.|Optional
side|String|Side of staircase.|Optional
state|String|State ("new", "active", "closed"). Can only be changed by using activation/deactivation link in [location representation](#location)| Neither
street_name|String|Street name|Required
title|String|Title.|Required
yearly_operational_cost_per_m2_from|[Money](#money)|Minimum yearly operational cost per m2.|Optional
yearly_operational_cost_per_m2_to|[Money](#money)|Maximum yearly operational cost per m2. Must be more than yearly_operational_cost_per_m2_from.|Optional
yearly_rent_per_m2_from|[Money](#money)|Minimum yearly rent per m2 .|Required
yearly_rent_per_m2_to|[Money](#money)|Maximum yearly rent per m2. Must be more than yearly_rent_per_m2_from.|Optional

All attributes not included in the list above will just be ignored. This makes it possible to GET an existing location ( with links, photos etc ), alter a few attributes and use it as the request body to create a new location.

#####<a id="money">Money</a>

Some fields expect to receive a money type.

Money example

<pre>
{
  "cents": 49500,
  "currency": "DKK"
}
</pre>

####Money Attributes

| Field | Type | Description | Required/Optional |
| ----- | ---- | ----------- | ----------------- |
cents|Integer|Price in currency times 100|Required
currency|String|Entity currency ("DKK")|Required

After posting the [Location Create](#location_create) for a new location you will receive
a response with the representation of the new location:  

Response body:

<pre>
{
    "location": {
        "title": "Beautiful place by the lake",
        "description": "Old building...\n\nIn the old center",
        "street_name": "Main Street",
        "house_number": "5",
        "floor": "1",
        "side": "th",
        "postal_code": 1371,
        "latitude": 52.145,
        "longitude": 12.813,
        "state": "new",
        "kind": "office",
        "area_from": 334,
        "area_to": 370,
        "external_key": "Location 3",
        "provider_website_link": "http://www.provider.com/location1",
        "yearly_rent_per_m2_from": {
            "cents": 117300,
            "currency": "DKK"
        },
        "yearly_rent_per_m2_to": {
            "cents": 137300,
            "currency": "DKK"
        },
        "yearly_operational_cost_per_m2_from": {
            "cents": 39500,
            "currency": "DKK"
        },
        "yearly_operational_cost_per_m2_to": {
            "cents": 49500,
            "currency": "DKK"
        }
    }
}
</pre>

Response header includes a `Location` key with a value containing a link for the location resource.  

A location does not have any photos, floor_plans or a prospectus when just created.

######Status codes
* 201 created
* 400 bad request




####<a id="update_location">Update Location</a>

PUT [ Location \["location"\] \["_links"\] \["self"\] \["href"\] ](#location_8289)

It is possible to update any of the [location attributes](#location_attributes) that can be set when [creating a location](#create_location).

Request body example:

######Location Update

<pre>
{
    "location": {
        "_links": {
            "self": {
                "href": "http://localhost:3000/api/provider/locations/8289"
            },
            "prospectuses": {
                "href": "http://localhost:3000/api/provider/locations/8289/prospectuses"
            },
            "photos": {
                "href": "http://localhost:3000/api/provider/locations/8289/photos"
            },
            "floor_plans": {
                "href": "http://localhost:3000/api/provider/locations/8289/floor_plans"
            },
            "deactivation": {<a id="location_8289_deactivation"></a>
                "href": "http://localhost:3000/api/provider/locations/8289/deactivation"
            },
        },
        "title": "Beautiful place by the lake",
        "description": "Old building...\n\nIn the old center",
        "street_name": "Main Street",
        "house_number": "5",
        "floor": "1",
        "side": "th",
        "postal_code": 2900,
        "latitude": 52.145,
        "longitude": 12.813,
        "state": "active",
        "kind": "office",
        "area_from": 334,
        "area_to": 370,
        "external_key": "Location 4",
        "provider_website_link": "http://www.provider.com/location1",
        "yearly_rent_per_m2_from": {
            "cents": 117300,
            "currency": "DKK"
        },
        "photos": [
            {
                "_links": {
                    "self": {
                        "href": "http://localhost:3000/api/provider/photos/142968"
                    }
                },
                "external_key": "Photo 5",
                "url": "/uploads/0014/2968/tokay.png"
            },
            {
                "_links": {
                    "self": {
                        "href": "http://localhost:3000/api/provider/photos/142969"
                    }
                },
                "external_key": "Photo 7",
                "url": "/uploads/0014/2969/tokay.png"
            },
            {
                "_links": {
                    "self": {
                        "href": "http://localhost:3000/api/provider/photos/142994"
                    }
                },
                "external_key": "Photo 512",
                "url": "/uploads/0014/2994/tokay.png"
            }
        ],
        "floor_plans": [
            {
                "_links": {
                    "self": {
                        "href": "http://localhost:3000/api/provider/floor_plans/142971"
                    }
                },
                "external_key": null,
                "url": "/uploads/0014/2971/1_full.jpg"
            },
            {
                "_links": {
                    "self": {
                        "href": "http://localhost:3000/api/provider/floor_plans/142977"
                    }
                },
                "external_key": "Floor Plan 1",
                "url": "/uploads/0014/2977/tokay.png"
            }
        ],
        "yearly_rent_per_m2_to": {
            "cents": 137300,
            "currency": "DKK"
        },
        "yearly_operational_cost_per_m2_from": {
            "cents": 39500,
            "currency": "DKK"
        },
        "yearly_operational_cost_per_m2_to": {
            "cents": 49500,
            "currency": "DKK"
        },
        "prospectus": {
            "_links": {
                "self": {
                    "href": "http://localhost:3000/api/provider/prospectuses/142973"
                }
            },
            "external_key": "Prospectus 2",
            "url": "/Users/kennjacobsen/lokalebasen/uploads/0014/2973/sample.pdf"
        }
    }
}
</pre>

Far from all the data in the request body example above is necessary.  
A request body like: `{ "location": { "external_key": "New Key" } } }` would change the `external_key` value.  

If succesful a [location representation](#location) will be returned in the response body.

######Status codes
* 200 ok
* 404 record not found




####<a id="activate_location">Activate Location</a>

Only locations that are not active ( `state` set to "new" or "closed" ) may be activated.

PUT [ Location \["location"\] \["_links"\] \["activation"\] \["href"\] ](#location_8289_activation)  

If succesfull a [location representation](#location) will be returned in the response body.

Response header includes a `Location` key with a value containing a link for the location resource.

######Status codes
* 200 ok
* 404 record not found




####<a id="deactivate_location">Deactivate Location</a>

Only locations that are active ( `state` set to "active" ) may be deactivated.

PUT [ Location \["location"\] \["_links"\] \["deactivation"\] \["href"\] ](#location_8289_deactivation)  

If succesfull a [location representation](#location) will be returned in the response body.  

Response header includes a `Location` key with a value containing a link for the location resource.

######Status codes
* 200 ok
* 404 record not found




####<a id="create_photo">Create Photo</a>

POST [ Location \["location"\] \["_links"\] \["photos"\] \["href"\] ](#location_8289_photos)  

Request body example:

<pre>
{
  "photo": {
    "external_key": "Photo 5",
    "url": "http://www.skyen.dk/worldpixelsPictures/BigNarrowPictures/tokay.png"
  }
}
</pre>

####Photo Attributes

| Field | Type | Description | Required/Optional |
| ----- | ---- | ----------- | ----------------- |
external_key|String|Providers own reference. Must be unique. A provider may only have one photo with the external_key set to e.g. "1", though this provider may also have e.g. a floor plan with the external_key set to "1".|Required
url|String|Photo URL ( jpg or png ).|Required

The photo file must be accesible on the internet.

The photo is uploaded in a background job, and may not be attached to the location immediately.

Response body example:

<pre>
{
    "job": {
        "_links": {
            "self": {
                "href": "http://localhost:3000/api/provider/asset_jobs/25951"
            }
        },
        "state": "enqueued"
    }
}
</pre>

Use the link supplied in the response body to find out how the job is doing.

* GET [ Job \["job\] \["_links"\] \["self"\] \["href"\] ](#job_25888) to [read job](#read_job).

######Status codes
* 202 accepted
* 400 bad request




####<a id="delete_photo">Delete Photo</a>

DELETE [ Location \["location"\] \["photos"\] \[index\] \["_links"\] \["self"\] \["href"\] ](#photo_5)

######Status codes
* 204 no content
* 404 record not found



####<a id="create_floor_plan">Create Floor Plan</a>

POST [ Location \["location"\] \["_links"\] \["floor_plans"\] \["href"\] ](#location_8289_floor_plans)  

Request body example:

<pre>
{
  "floor_plan": {
    "external_key": "Floor Plan 1",
    "url": "http://www.skyen.dk/worldpixelsPictures/BigNarrowPictures/floor_plan.png"
  }
}
</pre>

####Floor Plan Attributes

| Field | Type | Description | Required/Optional |
| ----- | ---- | ----------- | ----------------- |
external_key|String|Providers own reference. Must be unique. A provider may only have one floor plan with the external_key set to e.g. "1", though this provider may also have a photo with the external_key set to "1".|Required
url|String|Floor plan URL ( jpg or png ).|Required

The floor plan file must be accesible on the internet.  

The floor plan is uploaded in a background job, and may not be attached to the location immediately.  

Response body example:

<pre>
{
    "job": {
        "_links": {
            "self": {
                "href": "http://localhost:3000/api/provider/asset_jobs/25952"
            }
        },
        "state": "enqueued"
    }
}
</pre>

Use the link supplied in the response body to find out how the job is doing.

* GET [ Job \["job\] \["_links"\] \["self"\] \["href"\] ](#job_25888) to [read job](#read_job).

######Status codes
* 202 accepted
* 400 bad request




####<a id="delete_floor_plans">Delete Floor Plans</a>

DELETE [ Location \["location"\] \["floor_plans"\] \[index\] \["_links"\] \["self"\] \["href"\] ](#floor_plan_1)

######Status codes
* 204 no content
* 404 record not found




####<a id="create_prospectus">Create Prospectus</a>

POST [ Location \["location"\] \["_links"\] \["prospectuses"\] \["href"\] ](#location_8289_prospectuses)  

Request body example:

<pre>
{
  "prospectus": {
    "external_key": "Prospectus 2",
    "url": "http://www.skyen.dk/worldpixelsPictures/BigNarrowPictures/prospectus2.png"
  }
}
</pre>

####Prospectus Attributes

| Field | Type | Description | Required/Optional |
| ----- | ---- | ----------- | ----------------- |
external_key|String|Providers own reference. Must be unique. A provider may only have one prospectus with the external_key set to e.g. "1", though this provider may also have a floor plan with the external_key set to "1".|Required
url|String|Prospectus URL ( pdf, jpg or png )|Required

The prospectus file must be accesible on the internet.  

A location can only have one prospectus.  
If a location already has a prospectus, but you want to change it - first [delete](#delete_prospectus) the current prospectus and then add a new one.  

The prospectus is uploaded in a background job, and may not be attached to the location immediately.  

Response body example:

<pre>
{
    "job": {
        "_links": {
            "self": {
                "href": "http://localhost:3000/api/provider/asset_jobs/25953"
            }
        },
        "state": "enqueued"
    }
}
</pre>

Use the link supplied in the response body to find out how the job is doing.  

* GET [ Job \["job\] \["_links"\] \["self"\] \["href"\] ](#job_25888) to [read job](#read_job).

######Status codes
* 202 accepted
* 400 bad request




####<a id="delete_prospectus">Delete Prospectus</a>

DELETE [ Location \["location"\] \["prospectus"\] \["_links"\] \["self"\] \["href"\] ](#prospectus_1)  

######Status codes
* 204 no content
* 404 record not found



####<a id="read_job">Read Job</a>

GET [ Job \["job"\] \["_links"\] \["self"\] \["href"\] ](#job_25888)  

Request body example:

######Read Job
<pre>
{
    "job": {
        "_links": {<a id="job_25888"></a>
            "self": {
                "href": "http://localhost:3000/api/provider/asset_jobs/25888"
            }
        },
        "state": "enqueued"
    }
}
</pre>

The state of the job is revealed in the value of the `state` attribute. This will initialy be set to `enqueued`. When the job is done it will be set to either `success` or `error`. When set to `success` the photo, floor plan or prospectus will appear in the [Location](#location).


######Status codes
* 200 ok
* 404 record not found
