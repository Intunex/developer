---
layout: api
title: Skillhive API Authentication
subtitle: Authentication
sub_menu: authentication
date: 2014-07-03
---

<div class="pure-menu pure-menu-open pure-menu-horizontal">
    <ul>
        <li><a href="#authentication">Authenticating Requests</a></li>
        <li><a href="#keys">Generate Keys</a></li>
        <li><a href="#request">Forming a Request</a></li>
        <li><a href="#examples">Examples</a></li>
    </ul>
</div>

<h2 id="authentication">Authenticating Requests</h2>

Authentication is handled by some additional HTTP headers and signing the request
using RSA keys. In a nutshell, here's what you need to do:

1. Generate a private RSA key
1. Generate a public RSA key based on the private key
1. Login to Skillhive and setup the api, upload the contents of the *public* key to Skillhive
1. Use the private key to sign requests to Skillhive API

Here are the details.

<h2 id="keys">Generate the RSA Keys</h2>

The keys cannot be created in Skillhive and you need to create them yourself. It's pretty 
straightforward at least in *NIX based systems.

### Step 1. Generate a private key

First step is to generate a private key. 

    $ openssl genrsa 2048 > private_key.pem
    
This will create a file called ``private_key.pem`` which includes the private key. The
private key is used to create the signature for each request you make to Skillhive.

**NOTICE!** Keep the private key to yourself and never ever upload it to Skillhive!

### Step 2. Generate a Public Key

The public key is created based on the private key you created in step 1.

    $ openssl rsa -in private_key.pem -pubout -out public_key.pem

This will create a file called ``public_key.pem`` which includes the public that Skillhive
needs to verify the signature for each request.

<h2 id="request">Forming a Request</h2>

Some additional HTTP headers are required for each request you make to Skillhive API. The headers are

- ``Api-Id`` This is the ID you get when you setup your api connection in Skillhive. Skillhive uses to this to
check where the connection is coming from.
- ``Api-User`` The email address of the user who is connecting to Skillhive (the "loggedin user"). Remember,
that different users have different access rights in Skillhive and the data they are able to view through
the api can be different for different users.
- ``Api-Signature`` The signature created using the private key.

For each request Skillhive will check that 

1. Api keys matching ``Api-Id`` have been setup and are enabled,
1. The signature from ``Api-Signature`` matches the request,
1. A user account is found with the email address defined in ``Api-User``.

If any of these steps fails, Skillhive will return a response with error code ``403``. 

### Creating the Signature

The signature is created from the Api-Id, user email address, the content of the request and the
requested url. 

The signature is made from a string like this:

    {"url":"https://demo.skillhive.com/api/","content":"","api_id":"xasx7as87xash7978","user":"demouser@skillhive.com"}

**NOTICE!** The header ``Api-Signature`` field contains the signature in ``base64`` encoded format.


<h2 id="examples">Examples</h2>

Here is an example how to create the signature PHP. Let's assume we're trying to list all users in Skillhive
throught the api.

    // The data that we need for signing the request
    $url     = "https://demo.skillhive.com/api/user/"; // List all users
    $content = "";                                // Empty for GET requests
    $api_id  = "c7ds89c7shc7ds98h98";             // A random Api-Id recieved from Skillhive
    $user    = "testuser@demoskillhive.com";           // Email of "loggedin" user
    
    $data = array(
        'url'     => $url,
        'content' => $content,
        'api_id'  => $api_id,
        'user'    => $user,
    );        
    
    // The data to sign is a json encoded string    
    $data = json_encode($data);

    // Create signature using the private key
    $private_key = "-----BEGIN RSA PRIVATE KEY-----MIIEpAIBAAKCAQEAyUSQ3Jky...."; 
    $signature   = "";
    
    // Do the actual signing
    openssl_sign($data, $signature, $private_key);

    // Base64 encode signature
    $signature = base64_encode($signature);
    
    // Now $signature is ready to pass in the http headers


