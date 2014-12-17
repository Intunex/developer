---
layout: api
title: Swarms
subtitle: Get swarm data through the Skillhive API
sub_menu: swarm
date: 2014-07-03
---
<div class="pure-menu pure-menu-open pure-menu-horizontal">
    <ul>
        <li><a href="#all">List swarms</a></li>
        <li><a href="#single">Get a single swarm</a></li>
        <li><a href="#skills">Swarm skills</a></li>
        <li><a href="#checklists">Checklists</a></li>
        <li><a href="#stats">Statistics</a></li>
    </ul>
</div>


<h2 id="all">List All Swarms</h2>

*Endpoint: `/api/swarm/`*

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
            <td>List swarms</td>
            <td>
              <ul>
                <li>Offset: <code>int</code> fetch skills starting from (optional, default: 0)</li>
                <li>Limit: <code>int</code> how many skills to get (optional, default: 20, limit 0-50)</li>
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
      "next":"/api/swarm/?offset=20&limit=20",
      "total_count":124,
      "collection": [
        {
          "id":67521,
          "uri":"/api/swarm/67521/",
          "title":"Testing Project",
          "type":"project",
          "description":"This is a testing project.",
          "is_official":false,
          "is_draft":false,
          "location":"Helsinki, Finland",
          "competence": 78,     // The current user's competence...
          "interest": 90,       // ...and interest for this swarm.
          "resources":{
            "users":"/api/swarm/67521/user/",
            "skills":"/api/swarm/67521/skill/"
          },
          "start_at"::
          "end_at":
          "duration":6,
          "created_at" :
          "updated_at" :
        },
        ...
      ]
    }


<h2 id="single">Fetch a Single Swarm</h2>

*Endpoint: `/api/swarm/:swarm_id/`*

Fetch a single swarm based on swarm id.

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
            <td>Get swarm details</td>
            <td>N/A</td>
        </tr>
    </tbody>
</table>

An example of a return response:

    {
      "id":67521,
      "uri":"/api/swarm/67521/",
      "title":"Testing Project",
      "type":"project",
      "description":"This is a testing project.",
      "is_official":false,
      "is_draft":false,
      "location":"Helsinki, Finland",
      "resources":{
        "users":"/api/swarm/67521/user/",
        "skills":"/api/swarm/67521/skill/"
      },
      "start_at":
      "end_at":
      "duration":8,
      "created_at" :
      "updated_at" :
    }


<h2 id="skills">Fetch Skills in Swarm</h2>

*Endpoint: `/api/swarm/:swarm_id/skill/`*

Fetch skills used in swarm.

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
            <td>Get swarm skills</td>
            <td>
              <ul>
                <li>Offset: <code>int</code> fetch skills starting from (optional, default: 0)</li>
                <li>Limit: <code>int</code> how many skills to get (optional, default: 20, limit 0-50)</li>
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
      "next":"/api/swarm/67521/skill/?offset=20&limit=20",
      "total_count":8,
      "collection": [
        {
          "id":8989,
          "uri":"/api/swarm/67521/skill/8989/"
          "name":"PHP",
          "competence":75,
          "is_mandatory":true,
          "created_at":
          "updated_at":
        },
        {
          "id":8990,
          "uri":"/api/swarm/67521/skill/8990/"
          "name":"Unit testing",
          "competence":65,
          "is_mandatory":false,
          "created_at":
          "updated_at":
        },
        ...
      ]
    }

    
*Endpoint: `/api/swarm/:swarm_id/skill/:skill_id/`*

Get a single swarm skill by `skill_id`.

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
            <td>Get a single swarm skill</td>
            <td>N/A</td>
        </tr>
    </tbody>
</table>

An example of a return response:

    {
      "id":8989,
      "uri":"/api/swarm/67521/skill/8989/"
      "name":"PHP",
      "competence":75,
      "is_mandatory":true,
      "created_at":
      "updated_at":
    }


<h2 id="checklists">Swarm Checklists</h2>

### List Checklists

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

### Create a Checklist

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

### Get a single Checklist

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


### Update a Checklist

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

### Delete a Checklist

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


### List Checklist Items

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


### Create a new Checklist Item

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

### Get a single Checklist Item

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
    


### Update a Checklist Item

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

### Delete a Checklist Item

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


<h2 id="stats">Swarm Statistics</h2>

Endpoints to get swarm statistics.

### Swarm Statistics

Get a list of swarms ready for displaying swarms in statistics. This has a few minor differences
compared to the standard swarm list. This list includes `category` and `completeness` attributes
for each swarm. 

Category is based on the business unit of the user who created the swarm. A list of all available
categories is listed as well.

An example of a return response:

    {
      "limit":20,
      "offset":0,
      "previous":null,
      "next":"/api/swarm/?offset=20&limit=20",
      "total_count":124, // Total number of swarms
      "categories": [
        "Research and Development",
        "Intunex HQ",
        "Sales"
      ],
      "collection": [
        {
          "id":67521,
          "uri":"/api/swarm/67521/",
          "title":"Testing Project",
          "type":"project",
          "category":"HR Development",
          "description":"This is a testing project.",
          "completeness":7,
          "is_official":false,
          "is_draft":false,
          "location":"Helsinki, Finland",
          "resources":{
            "users":"/api/swarm/67521/user/",
            "skills":"/api/swarm/67521/skill/"
          },
          "start_at"::
          "end_at":
          "duration":6,
          "created_at" :
          "updated_at" :
        },
        ...
      ]
    }



### Swarm Skill Statistics

*Endpoint: `/api/swarm/:swarm_id/statistics/skills/user`*

Get statistics about swarm members' skills in the skills that are tagged in the swarm.

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
            <td>Get skill statistics</td>
            <td>N/A</td>
        </tr>
    </tbody>
</table>

An example of a return response:    

    {
      "total_count":3, // Total number of skills in this swarm
      "collection": [
        {
          "name":"Scrum",
          "uri":"/api/skill/?skill=Scrum",
          "competence_avg": 65,
          "interest_avg": 78,
          "expert_count": 8, // How many users in this swarm has this skill
          "users":[
            {
              "id":765,             
              "uri":"/api/user/765/",
              "name":"User Name",
              "icon_url":"https://company.skillhive.com/user/765/icon",
              "competence": 97,
              "interest": 78
            },
            {
              "id":768,             
              "uri":"/api/user/768/",
              "name":"Jane Doe",
              "icon_url":"https://company.skillhive.com/user/768/icon",
              "competence": 88,
              "interest": 95
            }
          ]
        },
        {
          "name":"Node.js",
          "uri":"/api/skill/?skill=node.js",
          "competence_avg": 45,
          "interest_avg": 89,
          "expert_count": 4, // How many users in this swarm has this skill
          "users":{
            {
              "id":768,             
              "uri":"/api/user/768/",
              "name":"Jane Doe",
              "icon_url":"https://company.skillhive.com/user/768/icon",
              "competence": 72,
              "interest": 81
            },
            {
              "id":765,             
              "uri":"/api/user/765/",
              "name":"User Name",
              "icon_url":"https://company.skillhive.com/user/765/icon",
              "competence": 56,
              "interest": 43
            }
          }        
        },
        ...
      ]
    }

