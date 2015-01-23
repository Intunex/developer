---
layout: api
title: Swarm Checklists
subtitle: Get checklists through the Skillhive API
sub_menu: checklist
date: 2015-01-23
---
<div class="pure-menu pure-menu-open pure-menu-horizontal">
    <ul>
        <li><a href="#list">List checklists</a></li>
        <li><a href="#create">Create a checklist</a></li>
        <li><a href="#single">Get a single checklist</a></li>
        <li><a href="#update">Update a checklist</a></li>
        <li><a href="#delete">Delete a checklist</a></li>
        <li><a href="#itemlist">List items</a></li>
        <li><a href="#itemcreate">Create an item</a></li>
        <li><a href="#itemsingle">Get a single item</a></li>
        <li><a href="#itemupdate">Update an item</a></li>
        <li><a href="#itemdelete">Delete an item</a></li>
    </ul>
</div>

<h2 id="list">List Swarm Checklists</h2>

*Endpoint: `/api/swarm/:swarm_id/checklist/`*

Fetch checklists in a swarm

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
            <td>Get swarm checklists</td>
            <td>
              <ul>
                <li>Offset: <code>int</code> fetch checklists starting from (optional, default: 0)</li>
                <li>Limit: <code>int</code> how many checklists to get (optional, default: 20, limit 0-50)</li>
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
      "next":"/api/swarm/67521/checklist/?offset=20&limit=20",
      "total_count":3,
      "collection": [
        {
          "id":8989,
          "uri":"/api/swarm/67521/checklist/8989/"
          "title":"My ToDos",
          "user":{                 // The user who created the Checklist
            "id":765,
            "uri":"/api/user/765/",
            "name":"User Name",
            "icon_url":"https://company.skillhive.com/user/765/icon"
          },
          "assigned_to":{          // This is an optional value. It can be
            "id":765,              // null or point to an existing user.
            "uri":"/api/user/765/",
            "name":"User Name",
            "icon_url":"https://company.skillhive.com/user/765/icon"
          },
          "resources": {
            "items": "/api/swarm/67521/checklist/8989/item/"
          }
          "created_at":
          "updated_at":
        },
        {
          "id":8998,
          "uri":"/api/swarm/67521/checklist/8998/"
          "title":"Check these out",
          "user":{                 // The user who created the Checklist
            "id":168,
            "uri":"/api/user/168/",
            "name":"User Name",
            "icon_url":"https://company.skillhive.com/user/168/icon"
          },
          "assigned_to":null,      // This is an optional value. Null if not set.
          "resources": {
            "items": "/api/swarm/67521/checklist/8989/item/"
          },
          "created_at":
          "updated_at":
        },
        ...
      ]
    }


<h2 id="create">Create a Checklist</h2>

*Endpoint: `/api/swarm/:swarm_id/checklist/`*

Create a new checklist in swarm.

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
            <td>Create a new Checklist</td>
            <td>
              <ul>
                <li>title: <code>string</code> The title of the Checklist (required)</li>
                <li>assigned_to: <code>int | hash</code> The user id, or a hash including user id for the user this checklist is assigned to (optional)</li> 
                <li>copy_from: <code>int</code> Checklist id for copying the items (optional)</li>
              </ul>            
            </td>
        </tr>
    </tbody>
</table>

If the checklist is succesfully created, the created checklist will be returned. For instance:

    {
      "id":8989,
      "uri":"/api/swarm/67521/checklist/8989/"
      "title":"My ToDos",
      "user":{                 // The user who created the Checklist
        "id":765,
        "uri":"/api/user/765/",
        "name":"User Name",
        "icon_url":"https://company.skillhive.com/user/765/icon"
      },
      "assigned_to":{          // This is an optional value. It can be
        "id":765,              // null or point to an existing user.
        "uri":"/api/user/765/",
        "name":"User Name",
        "icon_url":"https://company.skillhive.com/user/765/icon"
      },
      "resources": {
        "items": "/api/swarm/67521/checklist/8989/item/"
      }
      "created_at":
      "updated_at":
    }


<h2 id="single">Get a single Checklist</h2>

*Endpoint: `/api/swarm/:swarm_id/checklist/:checklist_id`*

Get a single checklist identified by `checklist_id`.

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
            <td>Get a Checklist</td>
            <td>
            N/A
            </td>
        </tr>
    </tbody>
</table>

Return the checklist, for instance:

    {
      "id":8989,
      "uri":"/api/swarm/67521/checklist/8989/"
      "title":"My ToDos",
      "user":{                 // The user who created the Checklist
        "id":765,
        "uri":"/api/user/765/",
        "name":"User Name",
        "icon_url":"https://company.skillhive.com/user/765/icon"
      },
      "assigned_to":{          // This is an optional value. It can be
        "id":765,              // null or point to an existing user.
        "uri":"/api/user/765/",
        "name":"User Name",
        "icon_url":"https://company.skillhive.com/user/765/icon"
      },
      "resources": {
        "items": "/api/swarm/67521/checklist/8989/item/"
      }
      "created_at":
      "updated_at":
    }


<h2 id="update">Update a Checklist</h2>

*Endpoint: `/api/swarm/:swarm_id/checklist/:checklist_id`*

Update an existing checklist identified by `checklist_id`.

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
            <td>Update a Checklist</td>
            <td>
              <ul>
                <li>title: <code>string</code> The title of the Checklist (required)</li>
                <li>assigned_to: <code>int | hash</code> The user id, or a hash including user id for the user this checklist is assigned to (optional)</li> 
              </ul>            
            </td>
        </tr>
    </tbody>
</table>

If the checklist is succesfully updated, the updated checklist will be returned. For instance:

    {
      "id":8989,
      "uri":"/api/swarm/67521/checklist/8989/"
      "title":"My ToDos",
      "user":{                 // The user who created the Checklist
        "id":765,
        "uri":"/api/user/765/",
        "name":"User Name",
        "icon_url":"https://company.skillhive.com/user/765/icon"
      },
      "assigned_to":{          // This is an optional value. It can be
        "id":765,              // null or point to an existing user.
        "uri":"/api/user/765/",
        "name":"User Name",
        "icon_url":"https://company.skillhive.com/user/765/icon"
      },
      "resources": {
        "items": "/api/swarm/67521/checklist/8989/item/"
      }
      "created_at":
      "updated_at":
    }


<h2 id="delete">Delete a Checklist</h2>

*Endpoint: `/api/swarm/:swarm_id/checklist/:checklist_id`*

Delete an existing checklist identified by `checklist_id`. *This will delete all items in this checklist as well.*

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
            <td>Delete a Checklist</td>
            <td>
            N/A
            </td>
        </tr>
    </tbody>
</table>

If the checklist is succesfully deleted, the server will return a HTTP Response with status code 200.


<h2 id="itemlist">List Checklist Items</h2>

*Endpoint: `/api/swarm/:swarm_id/checklist/:checklist_id/item/`*

Fetch items in a checklist.

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
            <td>Get items in a checklist</td>
            <td>
              <ul>
                <li>Offset: <code>int</code> fetch checklists starting from (optional, default: 0)</li>
                <li>Limit: <code>int</code> how many checklists to get (optional, default: 20, limit 0-50)</li>
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
      "next":"/api/swarm/67521/checklist/24/item/?offset=20&limit=20",
      "total_count":26,
      "collection": [
        {
          "id": 22,
          "title": "First task",
          "uri": "/api/swarm/14548/checklist/24/item/22",
          "user": {                        // The user who created the item
            "id": "123",
            "name": "Jaakko Naakka",
            "uri": "/api/user/123",
            "icon_url": "https://company.skillhive.com//user/123/icon/"
          },
          "checklist": {   // The checklist this item belongs to
            "id": "24",
            "uri": "/api/swarm/14548/checklist/24"
          },
          "completed_by": {   // Either null or user who marked this item completed
            "id": "123",
            "name": "Jaakko Naakka",
            "uri": "/api/user/123",
            "icon_url": "https://company.skillhive.com//user/123/icon/"
          },
          "completed_at": {   // Either null or timestamp when the item was completed
            "date": "Thu, 3 Mar 2014 10:45:29 +0200",
            "friendly_time": "yesterday",
            "date_local": "2014-3-3"
          },
          "created_at": {
            "date": "Wed, 30 Jan 2014 12:37:47 +0200",
            "friendly_time": "33 days ago",
            "date_local": "2014-1-30"
          },
          "updated_at": {
            "date": "Thu, 3 Mar 2014 10:45:29 +0200",
            "friendly_time": "yesterday",
            "date_local": "2014-3-3"
          },
        ...
      ]
    }


<h2 id="itemcreate">Create a new Checklist Item</h2>

*Endpoint: `/api/swarm/:swarm_id/checklist/:checklist_id/item/`*

Fetch items in a checklist.

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
            <td>Create a new checklist item</td>
            <td>
              <ul>
                <li>title: <code>string</code> The title of the checklist item (required)</li>
              </ul>            
            </td>
        </tr>
    </tbody>
</table>

If the checklist item is succesfully created, the created item will be returned. For instance:

    {
      "id": 22,
      "title": "First task",
      "uri": "/api/swarm/14548/checklist/24/item/22",
      "user": {                        // The user who created the item
        "id": "123",
        "name": "Jaakko Naakka",
        "uri": "/api/user/123",
        "icon_url": "https://company.skillhive.com//user/123/icon/"
      },
      "checklist": {   // The checklist this item belongs to
        "id": "24",
        "uri": "/api/swarm/14548/checklist/24"
      },
      "completed_by":null,
      "completed_at":null,
      "created_at": {
        "date": "Fri, 30 Jan 2014 12:37:47 +0200",
        "friendly_time": "just now",
        "date_local": "2014-1-30"
      },
      "updated_at": {
        "date": "Fri, 30 Jan 2014 12:37:47 +0200",
        "friendly_time": "just now",
        "date_local": "2014-1-30"
    }


<h2 id="itemsingle">Get a single Checklist Item</h2>

*Endpoint: `/api/swarm/:swarm_id/checklist/:checklist_id/item/:item_id`*

Get a single checklist item identified by `item_id`.

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
            <td>Get a single checklist item</td>
            <td>
            N/A
            </td>
        </tr>
    </tbody>
</table>

Get a single checklist item, for instance:

    {
      "id": 22,
      "title": "First task",
      "uri": "/api/swarm/14548/checklist/24/item/22",
      "user": {                        // The user who created the item
        "id": "123",
        "name": "Jaakko Naakka",
        "uri": "/api/user/123",
        "icon_url": "https://company.skillhive.com//user/123/icon/"
      },
      "checklist": {   // The checklist this item belongs to
        "id": "24",
        "uri": "/api/swarm/14548/checklist/24"
      },
      "completed_by": {   // Either null or user who marked this item completed
        "id": "123",
        "name": "Jaakko Naakka",
        "uri": "/api/user/123",
        "icon_url": "https://company.skillhive.com//user/123/icon/"
      },
      "completed_at": {   // Current server time
        "date": "Fri, 30 Jan 2014 12:37:47 +0200",
        "friendly_time": "just now",
        "date_local": "2014-1-30"
      },
      "created_at": {
        "date": "Fri, 30 Jan 2014 12:37:47 +0200",
        "friendly_time": "just now",
        "date_local": "2014-1-30"
      },
      "updated_at": {
        "date": "Fri, 30 Jan 2014 12:37:47 +0200",
        "friendly_time": "just now",
        "date_local": "2014-1-30"
    }
    


<h2 id="itemupdate">Update a Checklist Item</h2>

*Endpoint: `/api/swarm/:swarm_id/checklist/:checklist_id/item/:item_id`*

Update a checklist item identified by `item_id`.

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
            <td>Update a checklist item</td>
            <td>
              <ul>
                <li>title: <code>string</code> The title of the checklist item (required)</li>
                <li>completed_at: <code>string</code> This can be a <code>boolean</code> or a timestamp or
                a date string. The <code>completed_at</code> timestamp will always be saved as the current
                time of the server (optional).
                </li>
              </ul>            
            </td>
        </tr>
    </tbody>
</table>

If the checklist item is succesfully update, the updated item will be returned. The user who set
the item completed is always the currently loggedin user. An example of the returned item:

    {
      "id": 22,
      "title": "First task",
      "uri": "/api/swarm/14548/checklist/24/item/22",
      "user": {                        // The user who created the item
        "id": "123",
        "name": "Jaakko Naakka",
        "uri": "/api/user/123",
        "icon_url": "https://company.skillhive.com//user/123/icon/"
      },
      "checklist": {   // The checklist this item belongs to
        "id": "24",
        "uri": "/api/swarm/14548/checklist/24"
      },
      "completed_by": {   // Either null or user who marked this item completed
        "id": "123",
        "name": "Jaakko Naakka",
        "uri": "/api/user/123",
        "icon_url": "https://company.skillhive.com//user/123/icon/"
      },
      "completed_at": {   // Current server time
        "date": "Fri, 30 Jan 2014 12:37:47 +0200",
        "friendly_time": "just now",
        "date_local": "2014-1-30"
      },
      "created_at": {
        "date": "Fri, 30 Jan 2014 12:37:47 +0200",
        "friendly_time": "just now",
        "date_local": "2014-1-30"
      },
      "updated_at": {
        "date": "Fri, 30 Jan 2014 12:37:47 +0200",
        "friendly_time": "just now",
        "date_local": "2014-1-30"
    }


<h2 id="itemdelete">Delete a Checklist Item</h2>

*Endpoint: `/api/swarm/:swarm_id/checklist/:checklist_id/item/:item_id`*

Delete a checklist item identified by `item_id`.

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
            <td>Delete a Checklist Item</td>
            <td>
            N/A
            </td>
        </tr>
    </tbody>
</table>

If the item is succesfully deleted, the server will return a HTTP Response with status code 200.
