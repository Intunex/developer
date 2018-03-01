---
layout: apiv2
title: Education
subtitle: Get and update a user's education.
menu: apiv2
sub_menu: education
date: 2018-03-01
---
<div class="pure-menu pure-menu-open pure-menu-horizontal">
    <ul>
        <li><a href="#list">List user's education</a></li>
        <li><a href="#single">Single education items</a></li>
        <li><a href="#create">Add new education</a></li>
    </ul>
</div>

<h2 id="list">List user's education</h2>

*Endpoint: `/api/v2/educations`*

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
            <td>List a user's education</td>
            <td>
              <ul>
                <li><code>user</code>: <code>int</code> the user ID whose education you want to list. <strong>REQUIRED</strong></li>
                <li><code>offset</code>: <code>int</code> fetch education starting from (optional, default: 0)</li>
                <li><code>limit</code>: <code>int</code> how many items to get (optional, default: 20, limit 0-50)</li>
              </ul>
            </td>
        </tr>
    </tbody>
</table>

An example of a return response for a url like `/api/v2/educations?&user=12345678`

    "data": [ // The returned work experience collection
      {
        "type": "education",
        "id": "123456",
        "attributes": {
          "title": "MSc",
          "institution": "University of Tampere",
          "field": "Interactive Technology",
          "description": "Studying computer science and media.",
          "start-year": "2001",
          "end-year": "2007",
          "created-at": "Tue, 16 May 2017 15:08:46 +0300",
          "updated-at": "Tue, 16 May 2017 15:08:46 +0300"
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
      ... // More education itms.
    ],
    "meta": {
      "total-count": 7 // Total number of items for this user
    }



<h2 id="single">Single education items</h2>

*Endpoint: `/api/educations/:education_id`*

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
            <td>Delete education identified by <code>education_id</code></td>
            <td>N/A</td>
        </tr>
    </tbody>
</table>


<h2 id="create">Add new education</h2>

*Endpoint: `/api/v2/educations`*

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
            <td>Add new education.</td>
            <td>
            N/A
            </td>
        </tr>
    </tbody>
</table>

New education is added by issuing a `POST` request to the api endpoint `/api/v2/educations`. 

Here's an example request to post:

	{
      "data": {
        "type": "educations",
        "attributes": {
          "title": "MSc",
          "institution": "University of Tampere",
          "field": "Interactive Technology",
          "description": "Studying computer science and media.",
          "start-year": "2001",
          "end-year": "2007",
          "created-at": "Tue, 16 May 2017 15:08:46 +0300",
          "updated-at": "Tue, 16 May 2017 15:08:46 +0300"
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

