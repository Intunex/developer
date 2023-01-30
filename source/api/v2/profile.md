---
layout: apiv2
title: Users
subtitle: Get user data through the Skillhive API
menu: apiv2
sub_menu: profile
date: 2023-01-30
---
<div class="pure-menu pure-menu-open pure-menu-horizontal">
    <ul>
        <li><a href="#list">List all users</a></li>
        <li><a href="#single">Get or update a single user</a></li>
        <li><a href="#create">Add a new user</a></li>
    </ul>
</div>

<h2 id="list">List all users in Skillhive</h2>

This is also the main endpoint for searching for users.

*Endpoint: `/api/v2/users`*

<table class="pure-table">
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
            <td>List users</td>
            <td>
              <ul>
                <li><code>offset</code>: <code>int</code> fetch profiles starting from (optional, default: 0)</li>
                <li><code>limit</code>: <code>int</code> how many profiles to get (optional, default: 20, limit 0-50)</li>
                <li>Optional search options:
                  <ul>
                    <li><code>query</code> A generic search term to search for</li>
                    <li><code>skills[]</code> Match users by these skills.</li>
                  </ul>
                </li>
                <li>Optional sort parameters:
                  <ul>
                    <li><code>name</code> Sort in alphabetical order (default)</li>
                    <li><code>competence</code> Sort by matched competence (only available when searching users by skills)</li>
                    <li><code>interest</code> Sort by matched interest (only available when searching users by skills)</li>
                    <li><code>recommendations</code> Sort by the number of recommendations the users have got (only available when searching users by skills)</li>
                    <li><code>price</code> Sort by user defined price (only available in select sites)</li>
                  </ul>
                </li>
              </ul>
            </td>
        </tr>
    </tbody>
</table>

An example of a return response:

    {
      "data": [ // The returned user collection
        { // A user object
          "type": "users",
          "id": "12345",      // The user id
          "attributes": {     // User attributes
            "first-name": "Jaakko",
            "last-name": "Naakka",
            "email": "jaakko.naakka@intunex.fi",
            "description": "",
            "location": [
              "Finland",
              "Akaa"
            ],
            "unit": [
              "Development"
            ],
            "phone": [
              "123455"
            ],
            "mobile": [
              "123466"
            ],
            "is-enabled": true,
            "access-level": "admin",
            "img-url": {
              "small": "<Absolute URL to small version of user icon>",
              "medium": "Absolute <URL to medium version of user icon>",
              "large": "Absolute <URL to large version of user icon>"
              "xlarge": "Absolute <URL to extra large version of user icon>"
              "master": "Absolute <URL to the original version of user icon>"
            },
            "competence": 0,      // Competence, interest and...
            "interest": 0,        // ... recommendations are only available
            "recommendations": 0, // ... when you're searching users by skills.
            "created-at": "Thu, 07 Jun 2012 15:25:42 +0300",
            "updated-at": "Thu, 14 Sep 2017 11:36:17 +0300",
            "price": 145, // Prices are only used in some sites
            "price2": 8.45,
            "price3": 780,
            "alt-id": "cds7csd9423423" // An alternate id used only to identify user accounts in other services
          },
          "links": {
            "self": "/api/v2/users/2972"  // API link to the user profile itself
          }
        },
        ... // More user accounts.
      ],
      "meta": {
        "total-count": 145 // Number of user account.
      }
    }



<h2 id="single">Get or update a single user</h2>

*Endpoint: `/api/v2/users/:user_id`*

<table class="pure-table">
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
            <td>Get user profile defined by <code>user_id</code></td>
            <td>N/A</td>
        </tr>
        <tr>
            <td>PATCH</td>
            <td>Update a user profile identified by <code>user_id</code></td>
            <td>N/A</td>
        </tr>
    </tbody>
</table>

<h3>Get a Single User</h3>
An example of a return response to a `GET` request:

    {
      "data": {
        "type": "users",
        "id": "12345",      // The user id
        "attributes": {     // User attributes
          "first-name": "Jaakko",
          "last-name": "Naakka",
          "email": "jaakko.naakka@intunex.fi",
          "description": "",
          "location": [
            "Finland",
            "Akaa"
          ],
          "unit": [
            "Development"
          ],
          "phone": [
            "123455"
          ],
          "mobile": [
            "123466"
          ],
          "is-enabled": true,
          "access-level": "admin",
          "img-url": {
            "small": "<Absolute URL to small version of user icon>",
            "medium": "Absolute <URL to medium version of user icon>",
            "large": "Absolute <URL to large version of user icon>"
            "xlarge": "Absolute <URL to extra large version of user icon>"
            "master": "Absolute <URL to the original version of user icon>"
          },
          "is-supervisor": true,
          "competence": 0,      // Competence, interest and...
          "interest": 0,        // ... recommendations are only available
          "recommendations": 0, // ... when you're searching users by skills.
      "terms-accepted-at": "Wed, 21 Feb 2018 20:50:26 +0200",
          "created-at": "Thu, 07 Jun 2012 15:25:42 +0300",
          "updated-at": "Thu, 14 Sep 2017 11:36:17 +0300",
          "price": 145, // Prices are only used in some sites
          "price2": 8.45,
          "price3": 780,
          "alt-id": "cds7csd9423423" // An alternate id used only to identify user accounts in other services
        }
      },
      relationships": {
        "roles": {
          "data": [
            {
              "type": "userroles",
              "id": "47244"
            },
            {
              "type": "userroles",
              "id": "14251"
            }
          ]
        }    
      },
      "included": [
        {
          "type": "userroles",
          "id": "47244",
          "attributes": {
            "title": "Software Developers"
          }
        },
        {
          "type": "userroles",
          "id": "14251",
          "attributes": {
            "title": "Design Team"
          }
        },
      ]
    }

<h3>Update a single user</h3>
Here's an example `PATCH` request to update a user's first and last name. When
updating a user profile, it's only necessary to send the values for the updated
fields. 

Here's en example json data for a `PATCH` request to `/api/v2/users/12345`

    {
        "data": {
        "attributes": {
          "first-name": "Jane",
          "last-name": "Doe"
        }
      }
    }

The return response will include the full, updated user profile.

<h3>The Return Response</h3>
As you can see, when you fetch a single user profile, the response includes a lot
more information about the user than the generic list endpoint does.

The  `relationships` key includes some details about the relationships the user has
to some other types of models. In this case, it describes all the roles the user has.
This is very convenient, as you can get a lot more information about the user in
a single GET request.

The `included` key holds a list of some objects (or partial objects) that are
included in the response. In this case it includes partial details about the
roles the user has. This includes just the title and the id of the user role. This
information is enough to show what roles the user has and create links to the
user roles themselves.

Here is a more detailed description of all the user attributes and how to update them:

<table class="pure-table pure-table-striped">
    <thead>
        <tr>
            <th>Attribute</th>
            <th>Type</th>
            <th>Required</th>
            <th>Notes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>id</td>
            <td>string</td>
            <td>true</td>
            <td>ID is always provided by Skillhive and it cannot be changed. At the moment, all ids are of type <code>int</code> but this will change into strings in the future.</td>
        </tr>
        <tr>
            <td>first-name</td>
            <td>string</td>
            <td>true</td>
            <td>First name of the user.</td>
        </tr>
        <tr>
            <td>last-name</td>
            <td>string</td>
            <td>true</td>
            <td>Last name of the user.</td>
        </tr>
        <tr>
            <td>email</td>
            <td>string</td>
            <td>true</td>
            <td></td>
        </tr>
        <tr>
            <td>description</td>
            <td>string</td>
            <td>false</td>
            <td>The description summary of the user.</td>
        </tr>
        <tr>
            <td>location</td>
            <td>array</td>
            <td>false</td>
            <td>An array of strings.</td>
        </tr>
        <tr>
            <td>unit</td>
            <td>array</td>
            <td>false</td>
            <td>An array of strings.</td>
        </tr>
        <tr>
            <td>phone</td>
            <td>array</td>
            <td>false</td>
            <td>Array of phone numbers as strings.</td>
        </tr>
        <tr>
            <td>mobile</td>
            <td>array</td>
            <td>false</td>
            <td>Array of mobile numbers as strings.</td>
        </tr>
        <tr>
            <td>jobtitle</td>
            <td>array</td>
            <td>false</td>
            <td>Array of strings.</td>
        </tr>
        <tr>
            <td>website</td>
            <td>array</td>
            <td>false</td>
            <td>Array of strings.</td>
        </tr>
        <tr>
            <td>skype</td>
            <td>array</td>
            <td>false</td>
            <td>Array of strings.</td>
        </tr>
        <tr>
            <td>linkedin</td>
            <td>array</td>
            <td>false</td>
            <td>Array of strings. The absolute URL to LinkedIn profile. <strong>Notice</strong>, this is updated automatically when user authorizes Skillhive to fetch their LinkedIn profile data. This value cannot be changed in Skillhive.</td>
        </tr>
        <tr>
            <td>twitter</td>
            <td>array</td>
            <td>false</td>
            <td>Array of strings.</td>
        </tr>
        <tr>
            <td>is-enabled</td>
            <td>boolean</td>
            <td>true</td>
            <td>A simple boolean stating if the user account is enabled or not. Disabled users cannot log in and will not show up in user listings or searches. <strong>NOTICE!</strong> This value can only be changed by administrators and not the users themselves.</td>
        </tr>
        <tr>
            <td>is-supervisor</td>
            <td>boolean</td>
            <td>true</td>
            <td>Is the user a supervisor of any other users. This value cannot be updated through the API, it's calculated based on user relationships.</td>
        </tr>
        <tr>
            <td>access-level</td>
            <td>string</td>
            <td>true</td>
            <td>User's access level. Allowed values are <code>user</code>, <code>admin</code>, <code>ext</code> and <code>excluded</code>. <strong>NOTICE!</strong> This value can only be changed by administrators and not he users themselves.</td>
        </tr>
        <tr>
            <td>price</td>
            <td>double</td>
            <td>false</td>
            <td>Price is only used in some sites. <strong>Notice</strong>, sorting user accounts in search results is only possible based on <code>price</code> atteibute, not <code>price2</code> or <code>price3</code>.</td>
        </tr>
        <tr>
            <td>price2</td>
            <td>double</td>
            <td>false</td>
            <td>Price is only used in some sites. <strong>Notice</strong>, sorting user accounts in search results is only possible based on <code>price</code> atteibute, not <code>price2</code> or <code>price3</code>.</td>
        </tr>
        <tr>
            <td>price3</td>
            <td>double</td>
            <td>false</td>
            <td>Price is only used in some sites. <strong>Notice</strong>, sorting user accounts in search results is only possible based on <code>price</code> atteibute, not <code>price2</code> or <code>price3</code>.</td>
        </tr>
        <tr>
            <td>alt-id</td>
            <td>string</td>
            <td>false</td>
            <td>An alternate id that's only used in integrations to other service.</td>
        </tr>
        <tr>
            <td>terms-accepted-at</td>
            <td>string</td>
            <td>false</td>
            <td>A timestamp when the user accepted the terms of service. <code>null</code> if terms are not accepted yet.</td>
        </tr>
    </tbody>
</table>


<h2 id="create">Create a new user</h2>

*Endpoint: `/api/v2/users`*

<table class="pure-table">
    <thead>
        <tr>
            <th>Method</th>
            <th>Action</th>
            <th>Parameters</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>POST</td>
            <td>Create user</td>
            <td></td>
        </tr>
    </tbody>
</table>

You can add new user accounts to Skillhive by doing a `POST` request to the api endpoint. Here's an example request to post:

    {
      "data": {
        "type": "users",
        "attributes": {     // User attributes
          "first-name": "Jaakko",
          "last-name": "Naakka",
          "email": "jaakko.naakka@intunex.fi",
        }
      }
    }

The API endpoint will return a `201 Created` response with all the data for the newly created user. The data includes
all the same data you get when you're [fetching a single user by id](#single). If a non-admin user tries to create new 
user accounts, they will get a `403 Forbidden` response instead.

Creating new user accounts is actually pretty simple. The only really required value is `email`. Notice, that
email has to be unique across all users in Skillhive.




