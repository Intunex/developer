---
layout: apiv2
title: Skillhive API
subtitle: Skillhive API Documentation
menu: apiv2
sub_menu: basics
date: 2017-11-14
---

<div class="pure-menu pure-menu-open pure-menu-horizontal">
    <ul>
        <li><a href="#responses">Responses</a></li>
        <li><a href="#endpoints">Endpoints</a></li>
        <li><a href="#about">About</a></li>
    </ul>
</div>

<h2 id="about">About Skillhive API v2</h2>

Skillhive API v2 is built on [JsonAPI](http://jsonapi.org/) standard and it's designed
to be flexible and developer friendly. JsonAPI is widely supported in almost any programming language you can think of.

This is the v2 of the API. You should use this version for all new applications as the older v1 specification is being deprecated.


<h2 id="endpoints">API Endpoints</h2>

> Main endpoint for the API is `https://<customerid>.skillhive.com/api/v2/`

Skillhive API v2 has a very flat structure. For instance, listing all user accounts
is handled by the endpoint

    GET /api/v2/users

A single user account, whose id is 12345 can be fetched from

    GET /api/v2/users/12345

The flatness of the API is more evident in fetching resources that belong to another entity.
For instance, if you want to get the users skills, they can be accessed from the endpoint

    GET /api/v2/user-skills?user=12345

and *not* at /users/12345/skills as you might have expected.


<h2 id="responses">Responses</h2>

We embrace the HTTP specification and set the status codes, content types
and other HTTP headers accordingly. Almost all responses have some common
elements in them. These are described below.

### Listings

All listing responses through the API will be in the following format. Here's
an example of what a call to `/users` could look like.

    {
      "data": [               // The user collection
        {
          type": "users",
          "id": "15992",
          "attributes": {
            "name": "Jaakko Naakka",
            "email": "jaakko@naakka.net",
            "created-at": "Mon, 26 May 2014 13:59:07 +0300",
            "updated-at": "Fri, 03 Nov 2017 15:28:46 +0200",
          }
        },
        ... // More user accounts
      ],
      "meta": {               // Metadata about the request
        "total-count": "145"  // Total count of user models          
      }
    }

### Objects

Almost all objects will include some common elements. Here's an example of
a user object:

    {
      "id":12345,               // All objects have an `id`
      "created-at" :            // Timestamps telling when the object was created...
      "updated-at" :            // ... and when it was modified.
    }

### Timestamps

Almost all objects returned by the API will include timestamps `created-at` and `updated-at`
describing the the time the object was created and when it was last updated.

All timestamps returned by the api are in [RFC 2822](https://tools.ietf.org/html/rfc2822#page-14) format.

Some objects may include other timestamps as well.
