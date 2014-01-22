---
layout: api
title: List users
subtitle: List users through the xTune API
sub_menu: profile
date: 2014-01-22
---
<div class="pure-menu pure-menu-open pure-menu-horizontal">
    <ul>
        <li><a href="#list">List all users</a></li>
        <li><a href="#single">Get a single user</a></li>
    </ul>
</div>

<h2 id="list">List all users in xTune</h2>

*Endpoint: `/api/user/`*

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
                    <li><code>skill[]</code> Match users by these skills.</li>
                  </ul>
                </li>
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
      "next":"/api/user/?offset=20&limit=20",
      "collection": [
        {
          "id":12345,
          "name":"Test User",
          "uri":"/api/user/12345/", 
          "description":"I'm just a PHP programmer.",
          "job_title":"PHP Coder.",
          "location": ["Helsinki", "Finland"],
          "department":["Research and Development"],
          "job_rotation":true,
          "profile_url":"https://xtune.fi/pg/profile/testuser@xtune.fi/",
          "icon_url":"https://xtune.fi/public/user/12345/icon/small/",
          "email":"testuser@xtune.fi",
          "phone":"412 4214 421421412",
          "mobile":"+358 40 123 4567",
          "twitter":"intunex",
          "linkedin_url":"http://linkedin.com/",
          "website":"http://intunex.fi",
          "competence":45,  // Competence and interest are only available
          "interest":52,    // if you are searching by skills.
          "resources":{
            "skills":"/api/user/12345/skill/"
          },
          "created_at" :
          "updated_at" : 
        },
        ...
      ]
    }

    

<h2 id="single">Fetch a single user profile</h2>

*Endpoint: `/api/user/:user_id/`*

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
    </tbody>
</table>

An example of a return response:

    {
      "id":12345,
      "uri":"/api/user/12345/", 
      "name":"Test User",
      "description":"I'm just a PHP programmer.",
      "job_title":"PHP Coder.",
      "location":["Helsinki, Finland"],
      "department":["Research and Development", "Intunex HQ"],
      "job_rotation":true,
      "profile_url":"https://xtune.fi/pg/profile/testuser@xtune.fi/",
      "icon_url":"https://xtune.fi/public/user/12345/icon/small/",
      "email":"testuser@xtune.fi",
      "phone":"412 4214 421421412",
      "mobile":"+358 40 123 4567",
      "twitter":"intunex",
      "linkedin_url":"http://linkedin.com/",
      "website":"http://intunex.fi",
      "resources":{
        "skills":"/api/user/12345/skill/"
      },
      "created_at" :
      "updated_at" : 
    }
