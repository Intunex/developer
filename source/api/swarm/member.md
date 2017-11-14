---
layout: api
title: Swarm Members
subtitle: Get swarm members through the Skillhive API
menu: api
sub_menu: member
date: 2015-01-23
---
<div class="pure-menu pure-menu-open pure-menu-horizontal">
    <ul>
        <li><a href="#list">List members</a></li>
        <li><a href="#create">Add a member</a></li>
        <li><a href="#single">Get a single member</a></li>
        <li><a href="#update">Update membership</a></li>
        <li><a href="#delete">Remove a member</a></li>
    </ul>
</div>

<h2 id="list">List Swarm Members</h2>

*Endpoint: `/api/swarm/:swarm_id/member/`*

Fetch all members in a swarm.

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
            <td>Get swarm members</td>
            <td>
              <ul>
                <li>Offset: <code>int</code> fetch members starting from (optional, default: 0)</li>
                <li>Limit: <code>int</code> how many members to get (optional, default: 20, limit 0-50)</li>
              </ul>            
            </td>
        </tr>
    </tbody>
</table>

An example of a return response:    

    {
      "limit":20,
      "offset":0,
      "previous":null,
      "next":"/api/swarm/67521/member/?offset=20&limit=20",
      "total_count":28,
      "collection": [
        {
          "id": 4535,
          "relationship": "member",
          "role": "",
          "start_at": {
            "friendly_time": "yesterday",
            "date_local": "22.1.2015",
            "date": "Thu, 22 Jan 2015 14:17:43 +0200"
          },
          "end_at": null,
          "created_at": {
            "friendly_time": "two weeks ago",
            "date_local": "22.1.2015",
            "date": "Thu, 22 Jan 2015 14:17:43 +0200"
          },
          "updated_at": {
            "friendly_time": "yesterday",
            "date_local": "22.1.2015",
            "date": "Thu, 22 Jan 2015 14:17:43 +0200"
          },
          "user": {
            "id": 4535,
            "name": "Skillhive Tester",
            "uri": "\/api\/user\/4535",
            "icon_url": ""https://skillhive.com/public/user/4535/icon/small/"",
            "email": "testuser@skillhive.com",
          }
        },
        ...
      ]
    }


<h2 id="create">Add a Member</h2>

*Endpoint: `/api/swarm/:swarm_id/member/`*

Add a new member to swarm.

<table class="pure-table">
    <thead>
        <tr>
            <th>Method</th>
            <th>Action</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>POST</td>
            <td>Add a new member to swarm.</td>
        </tr>
    </tbody>
</table>

Possible post parameters:

<table class="pure-table">
    <thead>
        <tr>
            <th>Parameter</th>
            <th>Type</th>
            <th>Default</th>
            <th>Optional</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>user_id</td>
            <td>integer</td>
            <td>Current user's id</td>
            <td>true</td>
        </tr><tr>
            <td>start_at</td>
            <td>string</td>
            <td><code>now()</code></td>
            <td>true</td>
        </tr><tr>
            <td>end_at</td>
            <td>string</td>
            <td></td>
            <td>true</td>
        </tr>
    </tbody>
</table>

If `user_id` parameter is not sent the user making the request will be added as a member.
Optionally, you can also define start and end dates for the membership. Notice, that the
dates are not used in all swarm types.

If the membership is succesfully created, the returned response will be similar to the
result when viewing [a single membership](#single).         


<h2 id="single">Get a single Member</h2>

*Endpoint: `/api/swarm/:swarm_id/member/:user_id`*

Get a membership identified by `user_id`,

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
            <td>Get a membership</td>
            <td>
            N/A
            </td>
        </tr>
    </tbody>
</table>

Return the membership, for instance:

    {
      "id": 4535,
      "relationship": "member",
      "role": "",
      "start_at": {
        "friendly_time": "yesterday",
        "date_local": "22.1.2015",
        "date": "Thu, 22 Jan 2015 14:17:43 +0200"
      },
      "end_at": null,
      "created_at": {
        "friendly_time": "two weeks ago",
        "date_local": "22.1.2015",
        "date": "Thu, 22 Jan 2015 14:17:43 +0200"
      },
      "updated_at": {
        "friendly_time": "yesterday",
        "date_local": "22.1.2015",
        "date": "Thu, 22 Jan 2015 14:17:43 +0200"
      },
      "user": {
        "id": 4535,
        "name": "Skillhive Tester",
        "uri": "\/api\/user\/4535",
        "icon_url": ""https://skillhive.com/public/user/4535/icon/small/"",
        "email": "testuser@skillhive.com",
      }
    }

Some swarm types can have special user roles in the swarm. For instance, course swarms may
have teachers and onboarding swarms might have onboardess.


<h2 id="update">Update a Membership</h2>

*Endpoint: `/api/swarm/:swarm_id/member/:user_id`*

Update an existing membership identified by `user_id`.

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
            <td>PUT</td>
            <td>Update a membership</td>
            <td>
              <ul>
                <li>start_at <code>string</code> The start date.</li>
                <li>end_at <code>string</code> The end date.</li>
              </ul>            
            </td>
        </tr>
    </tbody>
</table>

If the membership is succesfully updated, the returned response will be similar to the
result when viewing [a single membership](#single).         


<h2 id="delete">Remove a Member</h2>

*Endpoint: `/api/swarm/:swarm_id/member/:user_id`*

Remove a user from swarm identified by `user_id`.

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
            <td>Remove a member.</td>
            <td>
            N/A
            </td>
        </tr>
    </tbody>
</table>

If the member is succesfully removed, the server will return a HTTP Response with status code 200.
