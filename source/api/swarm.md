---
layout: api
title: Swarms
subtitle: Get swarm data through the Skillhive API
menu: api
sub_menu: swarm
date: 2015-01-22
---
<div class="pure-menu pure-menu-open pure-menu-horizontal">
    <ul>
        <li><a href="#all">List swarms</a></li>
        <li><a href="#single">Get a single swarm</a></li>
        <li><a href="#create">Create a swarm</a></li>
        <li><a href="#skills">Swarm skills</a></li>
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


<h2 id="create">Create a Swarm</h2>

*Endpoint: `/api/swarm/`*

Create a new swarm.

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
            <td>Create a new swarm</td>
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
            <th>Values</th>
            <th>Optional</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>type</td>
            <td>string</td>
            <td>idea</td>
            <td>idea, problem, project, message, survey, announcement, objective,
            onboarding, course, certificate, role, expert</td>
            <td>true</td>
        </tr><tr>
            <td>title</td>
            <td>string</td>
            <td></td>
            <td>Max length 255 characters</td>
            <td>false</td>
        </tr><tr>
            <td>description</td>
            <td>string</td>
            <td></td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td>status</td>
            <td>string</td>
            <td>in_progress</td>
            <td>in_progress, completed</td>
            <td>true</td>
        </tr><tr>
            <td>is_draft</td>
            <td>boolean</td>
            <td>false</td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td>is_official</td>
            <td>boolean</td>
            <td>false</td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td>access</td>
            <td>string</td>
            <td>public</td>
            <td>public, members</td>
            <td>true</td>
        </tr><tr>
            <td>start_at</td>
            <td>string</td>
            <td><code>now()</code></td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td>end_at</td>
            <td>string</td>
            <td><code>now()</code></td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td>location</td>
            <td>string</td>
            <td></td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td>show_map</td>
            <td>boolean</td>
            <td>false</td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td>duration</td>
            <td>string</td>
            <td></td>
            <td>Max length 32 characters</td>
            <td>true</td>
        </tr><tr>
            <td>price</td>
            <td>string</td>
            <td></td>
            <td>Max length 32 characters</td>
            <td>true</td>
        </tr><tr>
            <td>participants_min</td>
            <td>integer</td>
            <td></td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td>participants_max</td>
            <td>integer</td>
            <td></td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td>skills</td>
            <td>string</td>
            <td></td>
            <td>A comma separated list of skill names: JavaScript, C++, Node.js</td>
            <td>true</td>
        </tr>
    </tbody>
</table>

Notice that almost all values have some sensible defaults and actually the swarm title is the only
required parameter you need to send. Notice also, that not all of the swarm attributes are actually
used in all swarm types. For instance, the number of allowed participants defined by `participants_min`
and `participants_max` parameters are only used for course swarms. The values are saved but they
won't be shown to users in the Skillhive UI.

If the swarm is created succesfully, the return response will be similar to the
[single swarm listing](#single) you get through the api.


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


<h2 id="stats">Swarm Statistics</h2>

Endpoints to get swarm statistics.

### Swarm Skill Statistics

*Endpoint: `/api/swarm/:swarm_id/statistics/skills/`*

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
