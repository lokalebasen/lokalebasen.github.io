---
layout: provider_api_sub
---
## Location Resources

* [Read Locations](#read_locations)
* [Read Location](#read_location)
* [Create Location](#create_location)
* [Update Location](#update_location)
* [Activate Location](#activate_location)
* [Deactivate Location](#deactivate_location)
* [Create Photo](#create_photo)
* [Update Photo](#update_photo)
* [Delete Photo](#delete_photo)
* [Create Floor Plan](#create_floor_plan)
* [Update Floor Plan](#update_floor_plan)
* [Delete Floor Plan](#delete_floor_plan)
* [Create Prospectus](#create_prospectus)
* [Update Prospectus](#update_prospectus)
* [Delete Prospectus](#delete_prospectus)
* [Read Job](#read_job)

### <a id="read_locations">Read Locations</a>

GET [Entry \["_links"\] \["locations"\] \["href"\] ](/provider_api.html#entry_locations)

Response body example:

### <a id="location_list">Locations</a>

{% highlight json %}
{
  "_links": {
    "self": {
      "href": "https://www.lokalebasen.dk/api/provider/locations"
    }
  },
  "locations": [
    {
      "_links": {
        "self": {
          "href": "https://www.lokalebasen.dk/api/provider/locations/8250"
        }
      },
      "id": 8250,
      "address_line1": "Lillegade 3",
      "address_line2": "",
      "postal_code": "1371",
      "postal_name": "København K",
      "area_from": 334,
      "area_to": null,
      "postal_district_name": "København K",
      "state": "closed",
      "kind": "office",
      "internal_identifier": "123456",
      "external_key": "Location 2"
    },
    {
      "_links": {
        "self": {
          "href": "https://www.lokalebasen.dk/api/provider/locations/8289"
        }
      },
      "id": 8289,
      "address_line1": "Hovedgaden 5, 1. th.",
      "address_line2": "",
      "postal_code": "1371",
      "postal_name": "København K",
      "area_from": 334,
      "area_to": 370,
      "postal_district_name": "København K",
      "state": "new",
      "kind": "office",
      "internal_identifier": "123457",
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

### Status codes
* 200 OK

### <a id="read_location">Read Location</a>

To find a specific location in the locations list a client application should
run through the list of [locations](#location_list) until it finds a match
for external_key. Then the client application may follow the self link for
that location to view additional data and options for the location.

GET [ Locations \["locations"\] \[index\] \["_links"\] \["self"\] \["href"\] ](#location_list)

Response body:

### <a id="location">Location</a>

{% highlight json %}
{
  "location": {
    "_links": {
      "self": {
        "href": "https://www.lokalebasen.dk/api/provider/locations/8289"
      },
      "prospectuses": {
        "href": "https://www.lokalebasen.dk/api/provider/locations/8289/prospectuses"
      },
      "photos": {
        "href": "https://www.lokalebasen.dk/api/provider/locations/8289/photos"
      },
      "floor_plans": {
        "href": "https://www.lokalebasen.dk/api/provider/locations/8289/floor_plans"
      },
      "subscriptions": {
        "href": "https://www.lokalebasen.dk/api/provider/locations/8289/subscriptions"
      },
      "activation": {
        "href": "https://www.lokalebasen.dk/api/provider/locations/8289/activation"
      }
    },
    "title": "Beautiful place by the lake",
    "description": "Old building...\n\nIn the old center",
    "contact": "https://www.lokalebasen.dk/api/provider/contacts/82776",
    "address_line1": "Hovedgaden 5, 1. th.",
    "address_line2": "",
    "postal_code": "1371",
    "postal_name": "København K",
    "latitude": 55.145,
    "longitude": 12.813,
    "state": "new",
    "kind": "office",
    "area_from": 334,
    "area_to": 370,
    "energy_rating": "A",
    "exempted_from_energy_rating": false,
    "internal_identifier": "123457",
    "external_key": "Location 45",
    "provider_website_link": "http://www.provider.com/location1",
    "facility_keys": ["alarm_system", "shower", "elevator"],
    "suitable_for_kinds": ["showroom", "clinic", "education"],
    "yearly_rent_per_m2_from": {
      "cents": 117300,
      "currency": "DKK"
    },
    "photos": [
      {
        "_links": {
          "self": {
            "href": "https://www.lokalebasen.dk/api/provider/photos/142968"
          }
        },
        "external_key": "Photo 5",
        "url": "https://www.lokalebasen.dk/uploads/0014/2968/tokay.png",
        "position": 0
      },
      {
        "_links": {
          "self": {
            "href": "https://www.lokalebasen.dk/api/provider/photos/142969"
          }
        },
        "external_key": "Photo 7",
        "url": "https://www.lokalebasen.dk/uploads/0014/2969/tokay.png",
        "position": 1
      }
    ],
    "floor_plans": [
      {
        "_links": {
          "self": {
            "href": "https://www.lokalebasen.dk/api/provider/floor_plans/142971"
          }
        },
        "external_key": "Floor Plan 1",
        "url": "https://www.lokalebasen.dk/uploads/0014/2971/1_full.jpg",
        "position": 0
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
    "yearly_heating_cost_per_m2_from": {
      "cents": 5500,
      "currency": "DKK"
    },
    "yearly_heating_cost_per_m2_to": {
      "cents": 7000,
      "currency": "DKK"
    },
    "yearly_water_cost_per_m2_from": {
      "cents": 5500,
      "currency": "DKK"
    },
    "yearly_water_cost_per_m2_to": {
      "cents": 7000,
      "currency": "DKK"
    },
    "yearly_electricity_cost_per_m2_from": {
      "cents": 5500,
      "currency": "DKK"
    },
    "yearly_electricity_cost_per_m2_to": {
      "cents": 7000,
      "currency": "DKK"
    },
    "prospectus": {
      "_links": {
        "self": {
          "href": "https://www.lokalebasen.dk/api/provider/prospectuses/142973"
        }
      },
      "external_key": "Prospectus 2",
      "url": "https://www.lokalebasen.dk/uploads/0014/2973/sample.pdf"
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
* GET [ Location \["location"\] \["_links"\] \["subscriptions"\] \["href"\] ](#location)
to [read list of subscriptions](/provider_api/subscriptions.html#read_subscriptions) for location.
* POST [ Location \["location"\] \["_links"\] \["subscriptions"\] \["href"\] ](#location)
to [create a subscription](/provider_api/subscriptions.html#read_subscriptions) for the location.

#### Status codes

* 200 OK
* 404 Record Not Found

### <a id="create_location">Create Location</a>

POST [ Locations \["locations"\] \["_links"\] \["self"\] \["href"\] ](#location_list)

Request body example:

#### <a id="location_create">Location Create</a>

{% highlight json %}
{
  "location": {
    "external_key": "Location 3",
    "title": "Beautiful place by the lake",
    "contact": "https://www.lokalebasen.dk/api/provider/contacts/82776",
    "description": "Old building...\n\nIn the old center",
    "address_line1": "Hovedgaden 5, 1. th.",
    "address_line2": "",
    "postal_code": "1371",
    "postal_name": "København K",
    "area_from": 334,
    "area_to": 370,
    "workstation_count_from": 4,
    "workstation_count_to": 10,
    "workstation_cost_per_month_from": 40,
    "workstation_cost_per_month_to": 100,
    "employees_count_from": 5,
    "employees_count_to": 9,
    "employees_count_visible": true,
    "kind": "office",
    "latitude": 55.145,
    "energy_rating": "A",
    "exempted_from_energy_rating": false,
    "has_energy_certificate_levels": false,
    "internal_identifier": "123458",
    "longitude": 12.813,
    "provider_website_link": "http://www.provider.com/location1",
    "is_rent_include_operational_cost": false,
    "yearly_rent_per_m2_amount_flexible": true,
    "annual_rent_amount_flexible": true,
    "fixed_annual_operational_cost": 43,
    "deposit_and_prepaid_rent": 0,
    "yearly_rental_income": 0,
    "amount_of_available_spaces": 4,
    "amount_of_spaces_from": 2,
    "amount_of_spaces_to": 5,
    "virtual_tour": "https://my.matterport.com/show/?m=tN8pmWWtDzc",
    "vimeo_id": "1098180204"
    "parking_type": "garage"
    "facility_keys": ["alarm_system", "shower", "elevator"],
    "suitable_for_kinds": ["showroom", "clinic", "education"],
    "secondary_kinds": ["office"],
    "energy_certificate_levels": ["Platin", "Excellent"],
    "hourly_rent_from": {
      "cents": 113,
      "currency": "DKK"
    },
    "monthly_rent_per_space_from": {
      "cents": 1100,
      "currency": "DKK"
    },
    "monthly_rent_per_space_to": {
      "cents": 1170,
      "currency": "DKK"
    },
    "annual_operational_cost_amount_from": {
      "cents": 1170,
      "currency": "DKK"
    },
    "annual_operational_cost_amount_to": {
      "cents": 1170,
      "currency": "DKK"
    },
    "annual_rent_from": {
      "cents": 900,
      "currency": "DKK"
    },
    "annual_rent_to": {
      "cents": 1000,
      "currency": "DKK"
    },
    "hourly_rent_to": {
      "cents": 117,
      "currency": "DKK"
    },
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
    },
    "yearly_heating_cost_per_m2_from": {
      "cents": 5500,
      "currency": "DKK"
    },
    "yearly_heating_cost_per_m2_to": {
      "cents": 7000,
      "currency": "DKK"
    },
    "yearly_water_cost_per_m2_from": {
      "cents": 5500,
      "currency": "DKK"
    },
    "yearly_water_cost_per_m2_to": {
      "cents": 7000,
      "currency": "DKK"
    },
    "yearly_electricity_cost_per_m2_from": {
      "cents": 5500,
      "currency": "DKK"
    },
    "yearly_electricity_cost_per_m2_to": {
      "cents": 7000,
      "currency": "DKK"
    },
    "annual_total_cost_amount_from": {
      "cents": 137300000000,
      "currency": "DKK"
    },
    "annual_total_cost_amount_to": {
      "cents": 234600000000,
      "currency": "DKK"
    }
  }
}
{% endhighlight %}

Some of the attributes included in the request body example above are optional.
Check the list below to see details for all fields.

####<a id="location_attributes">Location Attributes</a>

| Field                                 | Type                                  | Description | Required/Optional |
| ------------------------------------- | ------------------------------------- | ----------- | ----------------- |
| `address_line1`                       | String                                | | Required
| `address_line2`                       | String                                | | Optional
| `area_from`                           | Integer                               | Minimum area in m2.| Required (for all location `kind`s except "virtual_office" and "parking")
| `area_to`                             | Integer                               | Maximum area in m2. Must be more than area_from. | Optional
| `workstation_count_from`              | Integer                               | Minimum workstations count. | Optional
| `workstation_count_to`                | Integer                               | Maximum workstations count. Must be more than workstation_count_from. | Optional
| `workstation_cost_per_month_from`     | Integer                               | Minimum workstation cost per month. | Optional
| `workstation_cost_per_month_to`       | Integer                               | Maximum workstation cost per month. Must be more than workstation_cost_per_month_from. | Optional
| `employees_count_from`                | Integer                               | Minimum employees count. | Optional
| `employees_count_to`                  | Integer                               | Maximum employees count. Must be more than employees_count_from. | Optional
| `employees_count_visible`             | Boolean                               | Indicate the employees count visibility. Default is false.   | Optional
| `has_energy_certificate_levels`       | Boolean                               | Indicate the energy certificate levels visibility. Default is false.   | Optional
| `description`                         | String                                | A detailed description of the location. Use \n for new line. | Optional
| `energy_rating`                       | String                                | "A","B","C","D","E","F" or "G". null to remove. | Optional
| `exempted_from_energy_rating`         | Boolean                               | Indicate the location is exempted from having energy rating. The energy rating is null, when the location is exempted. Default is false.  | Optional
| `external_key`                        | String                                | Providers own reference. Must be unique for a given resource. E.g. a provider can only have one photo with an external_key called "1", but he may also have a floor plan with an external_key called "1" | Required
| `kind`                                | String                                | “Type of Lease” `section`: ("office", "business_center", "warehouse", "store", "coworking", "meeting_room", "virtual_office", "parking"). “Type of Sale” `section` ("housing", "office", "warehouse", "store", "lot"). | Required
| `secondary_kinds`                     | String array                          | `secondary kind` of location ("office", "business_center", "warehouse", "store", "coworking", "meeting_room", "cafe"). "cafe" allowed only if main `kind` is "store" | Optional
| `energy_certificate_levels`           | String array                          | `energy certificate levels` of location (`DGNB`: "Platin", "Guld", "Sølv", "Bronze", `Tillæg til DGNB`: "Diamant", "Hjerte", "Planet", `BREEAM`: "Outstanding", "Excellent", "Very good", "Good", "Pass", "Acceptable", `LEED`: "Platinum", "Gold", "Silver", "Certified"]). Can be selected just one from each energy certificate | Optional
| `suitable_for_kinds`                  | String array                          | `suitable for kind` of location (available "suitable for kinds" by location's kind: `store`: "cafe", "showroom", "clinic", "education", "popup_store", `office`: "showroom", "clinic", "education", `business_center`: "clinic", "education", `warehouse`: "high_ceiling_storage", "storage_hotel", "production", "workshop"). | Optional
| `internal_identifier`                 | String                                | Providers own internal reference. | Optional
| `latitude`                            | Float                                 | Latitude ( e.g. 55.6012 ). Should contain at least 4 decimal points. Must be within the area of Denmark ( 54.2000 - 57.9000 ). | Required
| `longitude`                           | Float                                 | Longitude ( e.g. 11.6121 ). Should contain at least 4 decimal points. Must be within the area of Denmark ( 7.8000 - 15.4000 ). | Required
| `postal_code`                         | String                                | A valid zip-code for the country of the location. | Required
| `postal_name`                         | String                                | The city/area for the postal code - will be autodetected from postal_code, if not set | Optional
| `provider_website_link`               | String                                | A link to the location representation on providers own website. | Optional
| `state`                               | String                                | State ("new", "active", "closed"). Can only be changed by using activation/deactivation link in [location representation](#location)| Neither
| `title`                               | String                                | Title. | Required
| `facility_keys`                       | String array                          | An array of facility keys as human readable strings. There are no technical constraints on the number. You can retrieve a list of approved values here: https://www.lokalebasen.dk/lease/api/facilities. The list may be subject to change. | Optional
| `contact`                             | [Contact Resource](#location_contact) | A resource representation of the contact. | Required
| `hourly_rent_from`                    | [Money](#money)                       | Minimum hourly rent. | Optional
| `hourly_rent_to`                      | [Money](#money)                       | Maximum hourly rent. | Optional
| `monthly_rent_per_space_from`         | [Money](#money)                       | Minimum monthly rent per space. | Optional
| `monthly_rent_per_space_to`           | [Money](#money)                       | Maximum monthly rent per space. | Optional
| `annual_operational_cost_amount_from` | [Money](#money)                       | Minimum annual operational cost amount. | Optional
| `annual_operational_cost_amount_to`   | [Money](#money)                       | Maximum annual operational cost amount. | Optional
| `annual_rent_from`                    | [Money](#money)                       | Minimum annual rent cost. | Optional
| `annual_rent_to`                      | [Money](#money)                       | Maximum annual rent cost. | Optional
| `yearly_operational_cost_per_m2_from` | [Money](#money)                       | Minimum yearly operational cost per m2. | Optional
| `yearly_operational_cost_per_m2_to`   | [Money](#money)                       | Maximum yearly operational cost per m2. Must be more than yearly_operational_cost_per_m2_from. | Optional
| `yearly_heating_cost_per_m2_from`     | [Money](#money)                       | Minimum yearly heating cost per m2. | Optional
| `yearly_heating_cost_per_m2_to`       | [Money](#money)                       | Maximum yearly heating cost per m2. Must be more than yearly_heating_cost_per_m2_from. | Optional
| `yearly_water_cost_per_m2_from`       | [Money](#money)                       | Minimum yearly water cost per m2. | Optional
| `yearly_water_cost_per_m2_to`         | [Money](#money)                       | Maximum yearly water cost per m2. Must be more than yearly_water_cost_per_m2_from. | Optional
| `yearly_electricity_cost_per_m2_from` | [Money](#money)                       | Minimum yearly electricity cost per m2. | Optional
| `yearly_electricity_cost_per_m2_to`   | [Money](#money)                       | Maximum yearly electricity cost per m2. Must be more than yearly_electricity_cost_per_m2_from. | Optional
| `yearly_rent_per_m2_from`             | [Money](#money)                       | Minimum yearly rent per m2. | Required
| `yearly_rent_per_m2_to`               | [Money](#money)                       | Maximum yearly rent per m2. Must be more than yearly_rent_per_m2_from. | Optional
| `annual_total_cost_amount_from`       | [Money](#money)                       | Minimum yearly total cost (yearly rent with yearly operational cost) | Optional
| `annual_total_cost_amount_to`         | [Money](#money)                       | Maximum yearly total cost (yearly rent with yearly operational cost). Must be more than annual_total_cost_amount_from. | Optional
| `monthly_rent_per_space_to`           | [Money](#money)                       | Maximum monthly rent per space. Must be more than monthly_rent_per_space_from. | Optional
| `monthly_rent_per_space_from`         | [Money](#money)                       | Minimum monthly rent per space. | Required for “virtual_office” location `kind` and shows on “parking” location `kind`
| `parking_type`                        | String                                | Type of parking ("underground_parking", "outdoor_parking", "parking_house", "garage"). | Requried for location with "parking" `kind`
| `amount_of_spaces_from`               | Integer                               | Maximum number of parking lots at parking. | Required for location with "parking" `kind`
| `amount_of_spaces_to`                 | Integer                               | Maximum number of parking lots at parking. | Optional
| `section`                             | String                                | For lease locations ("lease"), for sale locations ("own_use", "foreclosure", "investment"). | Optional (if not set then "lease")

All attributes not included in the list above will be ignored. This makes
it possible to GET an existing location ( with links, photos etc ), alter a
few attributes and use it as the request body to create a new location.

#### <a id="location_contact">Contact</a>

The contact information of the contact is the contact information displayed to the clients. The contact will also receive emails about leads for the location.

The value for the contact is the URL for the resource of the given contact.

{% highlight json %}
{
  "contact": "https://www.lokalebasen.dk/api/provider/contacts/82776"
}
{% endhighlight %}


#### <a id="money">Money</a>

Some fields expect to receive a money type.

Money example

{% highlight json %}
{
  "cents": 49500,
  "currency": "DKK"
}
{% endhighlight %}

#### Money Attributes

| Field      | Type    | Description                 | Required/Optional |
| ---------- | ------- | --------------------------- | ----------------- |
| `cents`    | Integer | Price in currency times 100 | Required
| `currency` | String  | Entity currency ("DKK")     | Required

After posting the [Location Create](#location_create) for a new location, the API will send a response with a full [location representation](#location).

Response header includes a `Location` key with a value containing a
link for the location resource.

A location does not have any photos, floor_plans or a prospectus just
after it is created.

#### Status codes

* 201 Created
* 400 Bad Request

### <a id="update_location">Update Location</a>

PUT [ Location \["location"\] \["_links"\] \["self"\] \["href"\] ](#location)

It is possible to update any of the [location attributes](#location_attributes)
that can be set when [creating a location](#create_location).

Request body example:

#### <a id="location_update">Location Update</a>

{% highlight json %}
{
  "location": {
    "title": "Beautiful place by the lake",
    "description": "Old building...\n\nIn the old center",
    "contact": "https://www.lokalebasen.dk/api/provider/contacts/82776",
    "address_line1": "Hovedgaden 5, 1. th.",
    "address_line2": "",
    "postal_code": "2900",
    "latitude": 55.145,
    "longitude": 12.813,
    "state": "active",
    "kind": "office",
    "area_from": 334,
    "energy_rating": null,
    "area_to": 370,
    "internal_identifier": "123456",
    "external_key": "Location 4",
    "provider_website_link": "http://www.provider.com/location1",
    "suitable_for_kinds": ["showroom", "clinic", "education"],
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
    },
    "yearly_heating_cost_per_m2_from": {
      "cents": 5500,
      "currency": "DKK"
    },
    "yearly_heating_cost_per_m2_to": {
      "cents": 7000,
      "currency": "DKK"
    },
    "yearly_water_cost_per_m2_from": {
      "cents": 5500,
      "currency": "DKK"
    },
    "yearly_water_cost_per_m2_to": {
      "cents": 7000,
      "currency": "DKK"
    },
    "yearly_electricity_cost_per_m2_from": {
      "cents": 5500,
      "currency": "DKK"
    },
    "yearly_electricity_cost_per_m2_to": {
      "cents": 7000,
      "currency": "DKK"
    },
    "annual_total_cost_amount_from": {
      "cents": 137300000000,
      "currency": "DKK"
    },
    "annual_total_cost_amount_to": {
      "cents": 234600000000,
      "currency": "DKK"
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

#### Status codes

* 200 OK
* 404 Record Not Found

### <a id="activate_location">Activate Location</a>

Only locations that are not active ( `state` set to "new" or "closed" ) may
be activated.

POST [ Location \["location"\] \["_links"\] \["activation"\] \["href"\] ](#location)

If succesfull a [location representation](#location) will be returned in the
response body.

Response header includes a `Location` key with a value containing a link for
the location resource.

#### Status codes

* 200 OK
* 404 Record Not Found

### <a id="deactivate_location">Deactivate Location</a>

Only locations that are active ( `state` set to "active" ) may be deactivated.

POST [ Location \["location"\] \["_links"\] \["deactivation"\] \["href"\] ](#location_update)

If succesfull a [location representation](#location) will be returned in the
response body.

Response header includes a `Location` key with a value containing a link for
the location resource.

#### Status codes

* 200 OK
* 404 Record Not Found

### <a id="create_photo">Create Photo</a>

POST [ Location \["location"\] \["_links"\] \["photos"\] \["href"\] ](#location)

Request body example:

{% highlight json %}
{
  "photo": {
    "external_key": "Photo 5",
    "url": "http://www.skyen.dk/worldpixelsPictures/BigNarrowPictures/tokay.png",
    "position": 2
  }
}
{% endhighlight %}

#### Photo Attributes

| Field          | Type    | Description | Required/Optional |
| -------------- | ------- | ----------- | ----------------- |
| `external_key` | String  | Providers own reference. Must be unique. A provider may only have one photo with the external_key set to e.g. "1", though this provider may also have e.g. a floor plan with the external_key set to "1". | Required
| `url`          | String  | Photo URL ( jpg, jpeg, png, tif, tiff, bmp or gif ). | Required
| `position`     | Integer | Photo position relative to other photos for location. Photo with the lowest position will be shown first. | Optional

The photo file must be accesible on the internet.

The photo is uploaded in a background job, and may not be attached to the
location immediately.

Response body example:

{% highlight json %}
{
    "job": {
        "_links": {
            "self": {
                "href": "https://www.lokalebasen.dk/api/provider/asset_jobs/25951"
            }
        },
        "state": "enqueued"
    }
}
{% endhighlight %}

Use the link supplied in the response body to find out how the job is doing.

* GET [ Job \["job\] \["_links"\] \["self"\] \["href"\] ](#read_job) to [read job](#read_job).

#### Status codes

* 202 Accepted
* 400 Bad Request

### <a id="update_photo">Update Photo</a>

PUT [ Location \["location"\] \["photos"\] \[index\] \["_links"\] \["self"\] \["href"\] ](#location)

Only the `position` and `url` attribute may be updated on a photo.

Request body example:

{% highlight json %}
{
  "photo": {
    "position": 4,
    "url": "http://www.skyen.dk/worldpixelsPictures/BigNarrowPictures/tokay.png"
  }
}
{% endhighlight %}

#### Status codes

* 200 OK
* 404 Record Not Found

### <a id="delete_photo">Delete Photo</a>

DELETE [ Location \["location"\] \["photos"\] \[index\] \["_links"\] \["self"\] \["href"\] ](#location)

#### Status codes

* 204 No Content
* 404 Record Not Found

### <a id="create_floor_plan">Create Floor Plan</a>

POST [ Location \["location"\] \["_links"\] \["floor_plans"\] \["href"\] ](#location)

Request body example:

{% highlight json %}
{
  "floor_plan": {
    "external_key": "Floor Plan 1",
    "url": "http://www.skyen.dk/worldpixelsPictures/BigNarrowPictures/floor_plan.png",
    "position": 4
  }
}
{% endhighlight %}

#### Floor Plan Attributes

| Field          | Type    | Description | Required/Optional |
| -------------- | ------- | ----------- | ----------------- |
| `external_key` | String  | Providers own reference. Must be unique. A provider may only have one floor plan with the external_key set to e.g. "1", though this provider may also have a photo with the external_key set to "1". | Required
| `url`          | String  | Floor plan URL ( jpg, jpeg, png, tif, tiff, bmp, gif or pdf ). | Required
| `position`     | Integer | Floor plan position relative to other floor plans for location. Floor plan with the lowest position will be shown first. | Optional

The floor plan file must be accesible on the internet.

The floor plan is uploaded in a background job, and may not be attached to the
location immediately.

Response body example:

{% highlight json %}
{
  "job": {
    "_links": {
      "self": {
        "href": "https://www.lokalebasen.dk/api/provider/asset_jobs/25952"
      }
    },
    "state": "enqueued"
  }
}
{% endhighlight %}

Use the link supplied in the response body to find out how the job is doing.

* GET [ Job \["job\] \["_links"\] \["self"\] \["href"\] ](#read_job) to
[read job](#read_job).

#### Status codes

* 202 Accepted
* 400 Bad Request

### <a id="update_floor_plan">Update Floor Plan</a>

PUT [ Location \["location"\] \["floor_plans"\] \[index\] \["_links"\] \["self"\] \["href"\] ](#location)

Only the `position` and `url` attribute may be updated on a floor plan.

Request body example:

{% highlight json %}
{
  "floor_plan": {
    "position": 4,
    "url": "http://www.skyen.dk/worldpixelsPictures/BigNarrowPictures/floor_plan.png"
  }
}
{% endhighlight %}

#### Status codes

* 200 OK
* 404 Record Not Found

### <a id="delete_floor_plan">Delete Floor Plans</a>

DELETE [ Location \["location"\] \["floor_plans"\] \[index\] \["_links"\] \["self"\] \["href"\] ](#location)

#### Status codes

* 204 No Content
* 404 Record Not Found

### <a id="create_prospectus">Create Prospectus</a>

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

#### Prospectus Attributes

| Field          | Type   | Description | Required/Optional |
| -------------- | ------ | ----------- | ----------------- |
| `external_key` | String | Providers own reference. Must be unique. A provider may only have one prospectus with the external_key set to e.g. "1", though this provider may also have a floor plan with the external_key set to "1". | Required
| `url`          | String | Prospectus URL ( pdf, jpg or png ) | Required

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
        "href": "https://www.lokalebasen.dk/api/provider/asset_jobs/25953"
      }
    },
    "state": "enqueued"
  }
}
{% endhighlight %}

Use the link supplied in the response body to find out how the job is doing.

* GET [ Job \["job\] \["_links"\] \["self"\] \["href"\] ](#read_job) to
[read job](#read_job).

#### Status codes

* 202 Accepted
* 400 Bad Request

### <a id="update_prospectus">Update Prospectus</a>

PUT [ Location \["location"\] \["prospectus"\] \[index\] \["_links"\] \["self"\] \["href"\] ](#location)

Only the `url` attribute may be updated on a prospectus.

Request body example:

{% highlight json %}
{
  "prospectus": {
    "url": "http://www.skyen.dk/worldpixelsPictures/BigNarrowPictures/prospectus2.png"
  }
}
{% endhighlight %}

#### Status codes

* 200 OK
* 404 Record Not Found

### <a id="delete_prospectus">Delete Prospectus</a>

DELETE [ Location \["location"\] \["prospectus"\] \["_links"\] \["self"\] \["href"\] ](#location)

#### Status codes

* 204 No Content
* 404 Record Not Found

### <a id="read_job">Read Job</a>

GET [ Job \["job"\] \["_links"\] \["self"\] \["href"\] ](#read_job)

Request body example:

#### <a id="read_job">Read Job</a>

{% highlight json %}
{
  "job": {
    "_links": {
      "self": {
        "href": "https://www.lokalebasen.dk/api/provider/asset_jobs/25888"
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

#### Status codes

* 200 OK
* 404 Record Not Found
