---
layout: apiv2
title: User Relationships
subtitle: Get user relationship data through the Skillhive API
menu: apiv2
sub_menu: relationship
date: 2023-04-27
---
<div class="pure-menu pure-menu-open pure-menu-horizontal">
    <ul>
        <li><a href="#list">List all user relationships</a></li>
        <li><a href="#delete">Delete a user relaitonship</a></li>
        <li><a href="#create">Create a new user relationship</a></li>
    </ul>
</div>

<h2 id="list">List all user relationships in Skillhive</h2>

*Endpoint: `/api/v2/user-relationships`*

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
            <td>List user relationships</td>
            <td>
              <ul>
                <li><code>offset</code>: <code>int</code> fetch profiles starting from (optional, default: 0)</li>
                <li><code>limit</code>: <code>int</code> how many profiles to get (optional, default: 20, limit 0-50)</li>
                <li><code>user</code>: <code>int</code> userId for the user whose relationiships you want to list</li>
                <li><code>target</code>: <code>int</code> userId for the user who is the target of the relationship</li>
                <li><code>relationship</code>: <code>string</code> list only relationships of this type, e.g. <code>subordinate</code></li>
              </ul>
            </td>
        </tr>
    </tbody>
</table>

An example of a return response:

    {
      "data": [ // The returned user relationship collection
        { // A relationship object
          "type": "user-relationships",
          "id": "12345",      // The user relationship id
          "attributes": {
            "relationship": "subordinate",
            "created-at": "Wed, 21 May 2014 10:11:24 +0300",
            "updated-at": "Tue, 03 Jun 2014 12:28:56 +0300"          
          },
          "relationships": {
            "target": {
              "data": {
                "type": "users",
                "id": "9876" // This is the user Id of the "target" of the relationship
              }
            }
          }
        },
        ... // More user relationships
      ],
      "meta": {
        "total-count": 5 // Number of user relationships.
      }
    }



<h2 id="delete">Delete a single user relationship</h2>

*Endpoint: `/api/v2/user-relationships/:user_relationship_id`*

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
            <td>DELETE</td>
            <td>Delete the relationship defined by <code>user_relationship_id</code></td>
            <td>N/A</td>
        </tr>
    </tbody>
</table>


<h2 id="create">Create a new user relationship</h2>

*Endpoint: `/api/v2/user-relationships`*

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
            <td>Create user relationship</td>
            <td></td>
        </tr>
    </tbody>
</table>

You can add new user relationships to Skillhive by doing a `POST` request to the api endpoint. Here's an example, to create a `subordinate` relationship between two users. In this example user `9876` is the supervisor of user `1234`. 

    {
      "data": {
        "type": "user-relationships",
        "attributes": {
          "relationship": "subordinate",
        },
        "relationships": {
          "user": {
            "data": {          // This is the user ID of the "owner" of the
              "type": "users", // relationship. In this example this is the subordinate.
              "id": "1234"     // This is usually the loggedin user whos is creating
            }                  // the relationship.
          },
          "target": {
            "data": {
              "type": "users", // This is the user ID of the "target" of the
              "id": "9876"     // relationship. In this example this is the supervisor.
            }
          }
        }
      }
    }

The API endpoint will return a `201 Created` response with all the data for the newly created relationsip. If a non-admin user tries to create new relationship for someone else, they will get a `403 Forbidden` response instead.

