---
layout: provider_api_sub
---
### Location Resources
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

####<a id="read_locations">Read Locations</a>

GET [Entry \["_links"\] \["locations"\] \["href"\] ](/provider_api.html#entry_locations)

Response body example:

####Locations
<a id="location_list"></a>

{% highlight json %}
{
    "_links": {
        "self": {
            "href": "http://www.lokalebasen.dk/api/provider/locations"
        }
    },
    "locations": [
            {
                "_links": {
                    "self": {
                        "href": "http://www.lokalebasen.dk/api/provider/locations/8250"
                    }
                },
                "id": 8250,
                "address_line1": "Lillegade 3",
                "address_line2": "",
                "postal_code": 1371,
                "area_from": 334,
                "area_to": null,
                "postal_district_name": "København K",
                "state": "closed",
                "kind": "office",
                "external_key": "Location 2"
            },
            {
                "_links": {
                    "self": {
                        "href": "http://www.lokalebasen.dk/api/provider/locations/8289"
                    }
                },
                "id": 8289,
                "address_line1": "Hovedgaden 5, 1. th.",
                "address_line2": "",
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
{% endhighlight %}

The response body consists of a link to this resource and a list of all
providers locations.
The [ Locations \["_links"\] \["self"\] \["href"\] ](#location_list) can
be used to reload the list of locations. It can also be used to POST data
to create a new location ( see [Create Location](#create_location) ).

Each location in the list has a link to its own resource. The URL for the
second location in the list above is found at
[ Locations \["locations"\] \[1\] \["_links"\] \["self"\] \["href"\] ](#location_list).
Use the GET method on these URLs  to see more details about a given location
 ( see [Read Location](#read_location) ).
The external_key value is providers own reference to a location used to find
the desired location.

####Status codes
* 200 ok




####<a id="read_location">Read Location</a>

To find a specific location in the locations list a client application should
run through the list of [locations](#location_list) until it finds a match
for external_key. Then the client application may follow the self link for
that location to view additional data and options for the location.

GET [ Locations \["locations"\] \[index\] \["_links"\] \["self"\] \["href"\] ](#location_list)

Response body:

####Location
<a id="location"></a>

{% highlight json %}
{
    "location": {
        "_links": {
            "self": {
                "href": "http://www.lokalebasen.dk/api/provider/locations/8289"
            },
            "prospectuses": {
                "href": "http://www.lokalebasen.dk/api/provider/locations/8289/prospectuses"
            },
            "photos": {
                "href": "http://www.lokalebasen.dk/api/provider/locations/8289/photos"
            },
            "floor_plans": {
                "href": "http://www.lokalebasen.dk/api/provider/locations/8289/floor_plans"
            },
            "activation": {
                "href": "http://www.lokalebasen.dk/api/provider/locations/8289/activation"
            }
        },
        "title": "Beautiful place by the lake",
        "description": "Old building...\n\nIn the old center",
        "address_line1": "Hovedgaden 5, 1. th.",
        "address_line2": "",
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
                "_links": {
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
                "_links": {
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
            "_links": {
                "self": {
                    "href": "http://www.lokalebasen.dk/api/provider/prospectuses/142973"
                }
            },
            "external_key": "Prospectus 2",
            "url": "http://www.lokalebasen.dk/uploads/0014/2973/sample.pdf"
        }
    }
}
{% endhighlight %}

[The list of links](#location) shows what you can do with a location.

* GET [ Location \["location"\] \["_links"\] \["self"\] \["href"\] ](#location)
to reload location.
* PUT [ Location \["location"\] \["_links"\] \["self"\] \["href"\] ](#location)
to [update location](#update_location).
* POST [ Location \["location"\] \["_links"\] \["activation"\] \["href"\] ](#location)
to [activate location](#activate_location). This link is only available
when `state` is "new" or "closed".
* POST [ Location \["location"\] \["_links"\] \["deactivation"\] \["href"\] ](#location_update)
to [deactivate location](#deactivate_location). This link is only available
when `state` is "active".
* POST [ Location \["location"\] \["_links"\] \["photos"\] \["href"\] ](#location)
to [create photos](#create_photo) for location.
* POST [ Location \["location"\] \["_links"\] \["floor_plans"\] \["href"\] ](#location)
to [create floor_plan](#create_floor_plan) for location.
* POST [ Location \["location"\] \["_links"\] \["prospectuses"\] \["href"\] ](#location)
to [create prospectus](#create_prospectus) for location.

####Status codes
* 200 ok
* 404 record not found

####<a id="create_location">Create Location</a>

POST [ Location \["location"\] \["_links"\] \["self"\] \["href"\] ](#location_list)

Request body example:


####Location Create
<a id="location_create"></a>

{% highlight json %}
{
    "location": {
        "external_key": "Location 3",
        "title": "Beautiful place by the lake",
        "description": "Old building...\n\nIn the old center",
        "address_line1": "Hovedgaden 5, 1. th.",
        "address_line2": "",
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
{% endhighlight %}

Some of the attributes included in the request body example above are optional.
Check the list below to see details for all fields.

#####<a id="location_attributes">Location Attributes</a>

| Field  | Type | Description | Required/Optional |
| ------ | ---- | ----------- | ----------------- |
address_line1|String| |Required
address_line2|String| |Optional
area_from|Integer|Minimum area in m2.|Required
area_to|Integer|Maximum area in m2. Must be more than area_from.|Optional
description|String|A detailed description of the location. Use \n for new line.|Optional
external_key|String|Providers own reference. Must be unique for a given resource. E.g. a provider can only have one photo with an external_key called "1", but he may also have a floor plan with an external_key called "1"|Optional
kind|String|Type ("office", "warehouse" or "store").|Required
latitude|Float|Latitude ( e.g. 55.6012 ). Must be within the area of Denmark ( 54.2000 - 57.9000 ).|Required
longitude|Float|Longitude ( e.g. 11.6121 ). Must be within the area of Denmark ( 7.8000 - 15.4000 ).|Required
postal_code|String|A valid zip-code for the country of the location.|Required
provider_website_link|String|A link to the location representation on providers own website.|Optional
state|String|State ("new", "active", "closed"). Can only be changed by using activation/deactivation link in [location representation](#location)| Neither
title|String|Title.|Required
yearly_operational_cost_per_m2_from|[Money](#money)|Minimum yearly operational cost per m2.|Optional
yearly_operational_cost_per_m2_to|[Money](#money)|Maximum yearly operational cost per m2. Must be more than yearly_operational_cost_per_m2_from.|Optional
yearly_rent_per_m2_from|[Money](#money)|Minimum yearly rent per m2 .|Required
yearly_rent_per_m2_to|[Money](#money)|Maximum yearly rent per m2. Must be more than yearly_rent_per_m2_from.|Optional

All attributes not included in the list above will be ignored. This makes
it possible to GET an existing location ( with links, photos etc ), alter a
few attributes and use it as the request body to create a new location.

#####<a id="money">Money</a>

Some fields expect to receive a money type.

Money example

{% highlight json %}
{
  "cents": 49500,
  "currency": "DKK"
}
{% endhighlight %}

####Money Attributes

| Field | Type | Description | Required/Optional |
| ----- | ---- | ----------- | ----------------- |
cents|Integer|Price in currency times 100|Required
currency|String|Entity currency ("DKK")|Required

After posting the [Location Create](#location_create) for a new location you
will receive
a response with the representation of the new location:

Response body:

{% highlight json %}
{
    "location": {
        "title": "Beautiful place by the lake",
        "description": "Old building...\n\nIn the old center",
        "address_line1": "Hovedgaden 5, 1. th.",
        "address_line2": "",
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
{% endhighlight %}

Response header includes a `Location` key with a value containing a
link for the location resource.

A location does not have any photos, floor_plans or a prospectus just
after it is created.

####Status codes
* 201 created
* 400 bad request




####<a id="update_location">Update Location</a>

PUT [ Location \["location"\] \["_links"\] \["self"\] \["href"\] ](#location)

It is possible to update any of the [location attributes](#location_attributes)
that can be set when [creating a location](#create_location).

Request body example:

####Location Update
<a id="location_update"></a>

{% highlight json %}
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
            "deactivation": {
                "href": "http://localhost:3000/api/provider/locations/8289/deactivation"
            },
        },
        "title": "Beautiful place by the lake",
        "description": "Old building...\n\nIn the old center",
        "address_line1": "Hovedgaden 5, 1. th.",
        "address_line2": "",
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
{% endhighlight %}

A full [location representation](#location) with the desired changes may be
used for the response body, though less data will do the job.
A request body like: `{ "location": { "external_key": "New Key" } } }` would
change the `external_key` value.

If succesful a [location representation](#location) will be returned in the
response body.

####Status codes
* 200 ok
* 404 record not found




####<a id="activate_location">Activate Location</a>

Only locations that are not active ( `state` set to "new" or "closed" ) may
be activated.

POST [ Location \["location"\] \["_links"\] \["activation"\] \["href"\] ](#location)

If succesfull a [location representation](#location) will be returned in the
response body.

Response header includes a `Location` key with a value containing a link for
the location resource.

####Status codes
* 200 ok
* 404 record not found




####<a id="deactivate_location">Deactivate Location</a>

Only locations that are active ( `state` set to "active" ) may be deactivated.

POST [ Location \["location"\] \["_links"\] \["deactivation"\] \["href"\] ](#location_update)

If succesfull a [location representation](#location) will be returned in the
response body.

Response header includes a `Location` key with a value containing a link for
the location resource.

####Status codes
* 200 ok
* 404 record not found




####<a id="create_photo">Create Photo</a>

POST [ Location \["location"\] \["_links"\] \["photos"\] \["href"\] ](#location)

Request body example:

{% highlight json %}
{
  "photo": {
    "external_key": "Photo 5",
    "url": "http://www.skyen.dk/worldpixelsPictures/BigNarrowPictures/tokay.png"
  }
}
{% endhighlight %}

####Photo Attributes

| Field | Type | Description | Required/Optional |
| ----- | ---- | ----------- | ----------------- |
external_key|String|Providers own reference. Must be unique. A provider may only have one photo with the external_key set to e.g. "1", though this provider may also have e.g. a floor plan with the external_key set to "1".|Required
url|String|Photo URL ( jpg or png ).|Required

The photo file must be accesible on the internet.

The photo is uploaded in a background job, and may not be attached to the
location immediately.

Response body example:

{% highlight json %}
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
{% endhighlight %}

Use the link supplied in the response body to find out how the job is doing.

* GET [ Job \["job\] \["_links"\] \["self"\] \["href"\] ](#read_job) to [read job](#read_job).

####Status codes
* 202 accepted
* 400 bad request




####<a id="delete_photo">Delete Photo</a>

DELETE [ Location \["location"\] \["photos"\] \[index\] \["_links"\] \["self"\] \["href"\] ](#location)

####Status codes
* 204 no content
* 404 record not found



####<a id="create_floor_plan">Create Floor Plan</a>

POST [ Location \["location"\] \["_links"\] \["floor_plans"\] \["href"\] ](#location)

Request body example:

{% highlight json %}
{
  "floor_plan": {
    "external_key": "Floor Plan 1",
    "url": "http://www.skyen.dk/worldpixelsPictures/BigNarrowPictures/floor_plan.png"
  }
}
{% endhighlight %}

####Floor Plan Attributes

| Field | Type | Description | Required/Optional |
| ----- | ---- | ----------- | ----------------- |
external_key|String|Providers own reference. Must be unique. A provider may only have one floor plan with the external_key set to e.g. "1", though this provider may also have a photo with the external_key set to "1".|Required
url|String|Floor plan URL ( jpg or png ).|Required

The floor plan file must be accesible on the internet.

The floor plan is uploaded in a background job, and may not be attached to the
location immediately.

Response body example:

{% highlight json %}
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
{% endhighlight %}

Use the link supplied in the response body to find out how the job is doing.

* GET [ Job \["job\] \["_links"\] \["self"\] \["href"\] ](#read_job) to
[read job](#read_job).

####Status codes
* 202 accepted
* 400 bad request




####<a id="delete_floor_plans">Delete Floor Plans</a>

DELETE [ Location \["location"\] \["floor_plans"\] \[index\] \["_links"\] \["self"\] \["href"\] ](#location)

####Status codes
* 204 no content
* 404 record not found




####<a id="create_prospectus">Create Prospectus</a>

POST [ Location \["location"\] \["_links"\] \["prospectuses"\] \["href"\] ](#location)

Request body example:

{% highlight json %}
{
  "prospectus": {
    "external_key": "Prospectus 2",
    "url": "http://www.skyen.dk/worldpixelsPictures/BigNarrowPictures/prospectus2.png"
  }
}
{% endhighlight %}

####Prospectus Attributes

| Field | Type | Description | Required/Optional |
| ----- | ---- | ----------- | ----------------- |
external_key|String|Providers own reference. Must be unique. A provider may only have one prospectus with the external_key set to e.g. "1", though this provider may also have a floor plan with the external_key set to "1".|Required
url|String|Prospectus URL ( pdf, jpg or png )|Required

The prospectus file must be accesible on the internet.

A location can only have one prospectus.
If a location already has a prospectus, but you want to change it - first
[delete](#delete_prospectus) the current prospectus and then add a new one.

The prospectus is uploaded in a background job, and may not be attached to the
location immediately.

Response body example:

{% highlight json %}
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
{% endhighlight %}

Use the link supplied in the response body to find out how the job is doing.

* GET [ Job \["job\] \["_links"\] \["self"\] \["href"\] ](#read_job) to
[read job](#read_job).

####Status codes
* 202 accepted
* 400 bad request




####<a id="delete_prospectus">Delete Prospectus</a>

DELETE [ Location \["location"\] \["prospectus"\] \["_links"\] \["self"\] \["href"\] ](#location)

####Status codes
* 204 no content
* 404 record not found



####<a id="read_job">Read Job</a>

GET [ Job \["job"\] \["_links"\] \["self"\] \["href"\] ](#read_job)

Request body example:

####Read Job
<a id="read_job"></a>

{% highlight json %}
{
    "job": {
        "_links": {
            "self": {
                "href": "http://localhost:3000/api/provider/asset_jobs/25888"
            }
        },
        "state": "enqueued"
    }
}
{% endhighlight %}

The state of the job is revealed in the value of the `state` attribute.
This will initialy be set to `enqueued`. When the job is done it will be set
to either `success` or `error`. When set to `success` the photo, floor plan
or prospectus will appear in the [Location](#location).


####Status codes
* 200 ok
* 404 record not found
