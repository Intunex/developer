---
layout: api
title: xTune API
subtitle: xTune API Documentation
sub_menu: basics
date: 2014-01-22
---

<div class="pure-menu pure-menu-open pure-menu-horizontal">
    <ul>
        <li><a href="#about">About</a></li>
        <li><a href="#versioning">Versioning</a></li>
        <li><a href="#browsing">Browsing the API</a></li>
        <li><a href="#format">Format</a></li>
        <li><a href="#responses">Responses</a></li>
    </ul>
</div>

<h2 id="about">About xTune API</h2>

xTune API is designed to be flexible and developer friendly. It's designed around
RESTful principles.

<h2 id="versioning">Versioning</h2>

We do our best not to brake backwards compatibility, but this can happen in some
unforeseen circumstances. Therefore, we provide the possibility to define which
version of the API you are accessing and get the contents in the format you want.

You can define the version using `Content-Type` HTTP header as
follows:


    application/vnd.xtune.YYYYMMDD+json

Where `YYYYMMDD` is the version (based on date, obviously) you requested.
You don't have to define the content-type, then you will just get the latest version.

<h2 id="browsing">Browsing the API</h2>

xTune API URI endpoints are designed to be as permanent as possible. But things change
and we don't know what our API will evolve into. Keep this in mind and don't hardcode API 
endpoints into your application. Instead, ask the initial endpoints through the API.

For exapmle, calling the root of the api at `/api` will return the current user, and the user object 
includes the URI for the user. Almost all objects include a `resources` object,
which includes URI endpoints for resources belonging to that object.

For instance, the user object includes

    "resources":{
      "skills":"/api/user/12345/skill",
      "colleagues":"/api/user/12345/colleague"
    }

Use the URI endpoints defined in the `resources` object and don't harcode
the endpoints. If you want to get the user's skills, for instance, don't hardcode 
the uri as `/api/user/:user_id/skill` but use the URI defined in resources 
instead.

Of course, hopefully we will never have the need to change our URI format, but you 
never know. It's good to get this right from the start.

<h2 id="format">Format</h2>

All responses from xTune are returned in `JSON` format.

<h2 id="responses">Responses</h2>

We embrace the HTTP specification and set the status codes, content types
and other HTTP headers accordingly. Almost all responses have some common 
elements in them. These are described below.

### Listings

All listing responses through the API will be in the following format. Here's
an example of what a call to `/api/user?limit=20&amp;offset=0` could look like.

    {
      "limit":20,                             // Current limit, defaults to 20
      "offset":0,                             // Current offset, defaults to 0
      "total_count":312,                      // Total number of objects
      "previous":null,                        // Pagination, previous set
      "next":"/api//user?offset=20&limit=20", // Pagination, next set
      "collection": [                         // The user collection
        ....
      ]
    }

### Objects

Almost all objects will include some common elements. Here's an example of
a user object:

    {
      "id":12345,              // All objects have an `id`
      "uri":"/api/user/12345", // Object URI is always included as `uri`
      "created_at" :           // Timestamps telling when the object was created... 
      "updated_at" :           // ... and when it was modified.
    }

Most objects include a `resources` object which includes
URIs to other resources belonging to this object. For example, the user
object include skills and colleagues in the following format

    {
      "id":12345,          
      "uri":"/api/user/12345", 
      "resources":{
        "skills":"/api/user/12345/skill",
        "colleagues":"/api/user/12345/colleague"
      }
    }

Using these API endpoints it's easy to get extra resources related to the
object.

## Fetch URI endpoints and current user

*Endpoint: `/api`*

This is the perfect starting points for using the API. Calling `/api` 
will return the current user object and the URI endpoints for our API.

<table class="pure-table ">
	<thead>
		<tr>
			<th>Method</th>
			<th>Action</th>
			<th>Parameters</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>GET</td>
			<td>Fetch URI endpoints</td>
			<td>N/A</td>
		</tr>
	</tbody>
</table>

An example of a return response:

    {
      "current_user":{
        "id":12345,
        "uri":"/api/user/12345",
        "resources":{
          "skills":"/api/user/12345/skill",
          "colleagues":"/api/user/12345/colleague"
        },
        "name":"Test User",
        "description":"I'm just a PHP programmer.",
        "job_title":"PHP Coder.",
        "location":"Helsinki, Finland",
        "department":"Research and Development, Intunex HQ",
        "job_rotation":true,
         "profile_url":"https://xtune.fi/pg/profile/testuser@xtune.fi/",
        "icon_url":"https://xtune.fi/public/user/12345/icon/small/",
        "email":"testuser@xtune.fi",
        "phone":"412 4214 421421412",
        "mobile":"+358 40 123 4567",
        "twitter":"intunex",
        "linkedin_url":"http://linkedin.com/",
        "website":"http://intunex.fi",
        "created_at" :
        "updated_at" : 
      },
      "resources":{
        "users":"/api/user",
        "skills":"/api/skill",
        "swarms":"/api/swarm"
      }
    }
