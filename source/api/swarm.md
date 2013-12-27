---
layout: api
title: List Swarm
subtitle: Get swarms through the xTune API
sub_menu: swarm
date: 2013-12-27
---
<div class="pure-menu pure-menu-open pure-menu-horizontal">
    <ul>
        <li><a href="#all">List all swarms</a></li>
        <li><a href="#single">Get a single swarm</a></li>
        <li><a href="#skills">Get swarm skills</a></li>
    </ul>
</div>


<h2 id="all">List All Swarms</h2>

*Endpoint: `/api/swarm`*

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
      "next":"/api/swarm?offset=20&limit=20",
      "total_count":124,
      "collection": [
        {
          "id":67521,
          "uri":"/api/swarm/67521",
          "title":"Testing Project",
          "type":"project",
          "description":"This is a testing project.",
          "is_official":false,
          "is_draft":false,
          "location":"Helsinki, Finland",
          "competence": 78,     // The current user's competence...
          "interest": 90,       // ...and interest for this swarm.
          "resources":{
            "users":"/api/swarm/67521/user",
            "skills":"/api/swarm/67521/skill"
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

*Endpoint: `/api/swarm/:swarm_id`*

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
      "uri":"/api/swarm/67521",
      "title":"Testing Project",
      "type":"project",
      "description":"This is a testing project.",
      "is_official":false,
      "is_draft":false,
      "location":"Helsinki, Finland",
      "resources":{
        "users":"/api/swarm/67521/user/",
        "skills":"/api/swarm/67521/skill"
      },
      "start_at":
      "end_at":
      "duration":8,
      "created_at" :
      "updated_at" :
    }


<h2 id="skills">Fetch Skills in Swarm</h2>

*Endpoint: `/api/swarm/:swarm_id/skill`*

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
            <td>N/A</td>
        </tr>
    </tbody>
</table>

An example of a return response:

    {
      "limit":20,
      "offset":0,
      "previous":null,
      "next":"/api/swarm/67521/skill?offset=20&limit=20",
      "total_count":8,
      "collection": [
        {
          "id":8989,
          "uri":"/api/swarm/67521/skill/8989"
          "name":"PHP",
          "competence":75 
        },
        {
          "id":8990,
          "uri":"/api/swarm/67521/skill/8990"
          "name":"Unit testing",
          "competence":65
        },
        ...
      ]
    }
