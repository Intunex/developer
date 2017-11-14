---
layout: api
title: Skills
subtitle: Get skills through the Skillhive API
menu: api
sub_menu: skill
date: 2014-07-03
---
<div class="pure-menu pure-menu-open pure-menu-horizontal">
    <ul>
        <li><a href="#all">List all skill</a></li>
        <li><a href="#details">Get skill details</a></li>
        <li><a href="#user">Get user skills</a></li>
    </ul>
</div>


<h2 id="all">Fetch All Skills</h2>

*Endpoint: `/api/skill/`*

List all skills in Skillhive.

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
            <td>Get all skills</td>
            <td>
              <ul>
                <li><code>offset</code>: <code>int</code> fetch skills from (optional, default: 0)</li>
                <li><code>limit</code>: <code>int</code> how many skills to get (optional, default: 20, limit 0-50)</li>
              </ul>
            </td>
        </tr>
    </tbody>
</table>

An example of a return response:

    {
      "limit":20,
      "offset":0,
      "total_count":214,
      "previous":null,
      "next":"/api/skill/?offset=20&limit=20",
      "collection": [
        {
          "id":67521,
          "uri":"/api/skill/?skill=Scrum",
          "name":"Scrum",
          "description":"Scrum is an agile method.",
          "competence_avg": 65,
          "interest_avg": 78,
          "expert_count": 250,
          "resources":{
            "users":"/api/user/?skill[]=Scrum",
            "swarms":"/api/swarm/?skill[]=Scrum"
          }
        },
        {
          "id":67521,
          "uri":"/api/skill/?skill=PHP",
          "name":"PHP",
          "description":"PHP is a programming language...",
          "competence_avg": 89,
          "interest_avg": 65,
          "expert_count": 120,
          "resources":{
            "users":"/api/user/?skill[]=PHP",
            "swarms":"/api/swarm/?skill[]=PHP"
          }
        },
        ...
      ]
    }

<h2 id="details">Fetch Skill Details</h2>

*Endpoint: `/api/skill/?skill=:skillname`*

This is the "skill page" which shows a summary of experts and swarms who have this skills.

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
            <td>Get skill details</td>
            <td>N/A</td>
        </tr>
    </tbody>
</table>

An example of a return response:

    {
      "id":67521,
      "uri":"/api/skill/?skill=Scrum",
      "name":"Scrum",
      "description":"Scrum is an agile method.",
      "competence_avg": 89,
      "interest_avg": 65,
      "expert_count": 120,
      "resources":{
        "users":"/api/user/?skill[]=Scrum",
        "swarms":"/api/swarm/?skill[]=Scrum"
      }
    }    



<h2 id="user">Fetching User Skills</h2>

*Endpoint: `/api/user/:user_id/skill/`*

Fetch a user's personal skills and competences. The skills are ordered by
highlight, competence and interest.

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
            <td>List a user's skills</td>
            <td>
              <ul>
                <li>Offset: <code>int</code> fetch skills starting from (optional, default: 0)</li>
                <li>Limit: <code>int</code> how many skills to get (optional, default: 20, limit 0-200)</li>
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
      "total_count": 92
      "next":"/api/user/123456/skill/?offset=20&limit=20",
      "collection": [
        {
          "id":67521,
          "uri":"/api/user/123456/skill/67521/",
          "name":"Scrum",
          "is_highlight":false,
          "competence":72,
          "interest":65,
          "recommendations":3
          "created_at":
          "updated_at":
        },
        {
          "id":67523,
          "uri":"/api/user/123456/skill/67523/",
          "name":"PHP",
          "is_highlight":true,
          "competence":91,
          "interest":89,
          "recommendations":4
          "created_at":
          "updated_at":
        }
        ...
      ]
    }


*Endpoint: `/api/user/:user_id/skill/:skill_id`*

Fetch a single user skill.

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
            <td>Get a single skill by user.</td>
            <td>
            N/A
            </td>
        </tr>
    </tbody>
</table>

An example of a return response:

    {
      "id":67521,
      "uri":"/api/user/123456/skill/67521/",
      "name":"Scrum",
      "is_highlight":false,
      "competence":72,
      "interest":65,
      "recommendations":3
      "created_at":
      "updated_at":
    }
