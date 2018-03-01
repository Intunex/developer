---
layout: apiv2
title: Work Experience
subtitle: Get and update a user's work experience.
menu: apiv2
sub_menu: work-experience
date: 2018-03-01
---
<div class="pure-menu pure-menu-open pure-menu-horizontal">
    <ul>
        <li><a href="#list">List user's work experience</a></li>
        <li><a href="#single">Single work experience items</a></li>
        <li><a href="#create">Add new work experience</a></li>
    </ul>
</div>

<h2 id="list">List user's work experience</h2>

*Endpoint: `/api/v2/work-experiences`*

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
            <td>List a user's work experience</td>
            <td>
              <ul>
                <li><code>user</code>: <code>int</code> the user ID whose work experience you want to list. <strong>REQUIRED</strong></li>
                <li><code>offset</code>: <code>int</code> fetch work experience starting from (optional, default: 0)</li>
                <li><code>limit</code>: <code>int</code> how many items to get (optional, default: 20, limit 0-50)</li>
              </ul>
            </td>
        </tr>
    </tbody>
</table>

An example of a return response for a url like `/api/v2/work-experiences?&user=12345678`

    "data": [ // The returned work experience collection
      {
        "type": "work-experience",
        "id": "123456",
        "attributes": {
          "title": "CTO",
          "institution": "Intunex Oy",
          "description": "Develop Skillhive.",
          "start-year": "2010",
          "end-year": null,
          "is-current": true,
          "linkedin-id": null,
          "created-at": "Thu, 10 Aug 2017 11:15:31 +0300",
          "updated-at": "Thu, 10 Aug 2017 11:15:31 +0300"
        },
        "relationships": {
          "user": {
            "data": {
              "type": "users",
              "id": "12345678"
            }
          }
        }
      },
      ... // More work experience itms.
    ],
    "meta": {
      "total-count": 7 // Total number of items for this user
    }



<h2 id="single">Single work experience items</h2>

*Endpoint: `/api/work-experiences/:workexperience_id`*

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
            <td>Delete work experience identified by <code>workexperience_id</code></td>
            <td>N/A</td>
        </tr>
    </tbody>
</table>


<h2 id="create">Add new work experience</h2>

*Endpoint: `/api/v2/work-experiences`*

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
            <td>Add new work experience</td>
            <td>
            N/A
            </td>
        </tr>
    </tbody>
</table>

New work experience is added by issuing a `POST` request to the api endpoint `/api/v2/work-experiences`. 

Here's an example request to post:

	{
      "data": {
        "type": "work-experience",
        "attributes": {
          "title": "CTO",
          "institution": "Intunex Oy",
          "description": "Develop Skillhive.",
          "start-year": "2010",
          "end-year": null,
          "is-current": true,
          "linkedin-id": null,
          "created-at": "Thu, 10 Aug 2017 11:15:31 +0300",
          "updated-at": "Thu, 10 Aug 2017 11:15:31 +0300"
        },
        "relationships": {
          "user": { // This defines the user whose work experience this is.
            "data": {
              "type": "users",
              "id": "12345678"
            }
          }
        }
      }
    }

The API endpoint will return a `201 Created` response with all the data for the newly created item.

