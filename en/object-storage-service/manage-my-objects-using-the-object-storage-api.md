---
title: "Manage my objects using the Object Storage API"
slug: manage-my-objects-using-the-object-storage-api
---


This article will describe how to use the OpenStack SWIFT API to manage your objects. To do all these API calls, you need to have your Object Storage API credentials handy. If you didn't read it yet, see [this article](https://app.elev.io/articles/edit/4982#) to know how to obtain your credentials from our self-service portal.

In the examples, you will notice some highlighted portions. These are important values that you will need for subsequent calls.

### Tokens

First, you have to obtain a token from the authentication authority.

#### POST /v2.0/tokens

##### Authenticate

Authenticates and generates a token.

The Identity API is a ReSTful web service. It is the entry point to all service APIs.

**Normal response codes:** 200, 203
**Error response codes:** identityFault (400, 500, …), userDisabled (403), badRequest (400), unauthorized (401), forbidden (403), badMethod (405), overLimit (413), serviceUnavailable (503), itemNotFound (404)

**JSON Data:**

```
{
    "auth": {
        "tenantName": "warrenton-Medias",
        "passwordCredentials": {
            "username": "warrenton-user",
            "password": "GhJdhw72pc927"
        }
    }
}
```

**CURL Request:**

```
curl -X POST -i \
 -H "Content-Type: application/json" \
 -d @test.json \
 https://auth-east.cloud.ca/v2.0/tokens ; echo
```

**CURL Response:**

```
HTTP/1.1 200 OK
Vary: X-Auth-Token
X-Distribution: Ubuntu
Content-Type: application/json
Content-Length: 1238
Date: Mon, 16 Mar 2015 23:01:50 GMT
{
   "access":{
      "token":{
         "issued_at":"2015-03-16T23:01:50.129423",
         "expires":"2015-03-17T00:01:50Z",
    -->  "id":"c7436b7a2f1a4c1fb58606fa9b4b0816", <--
         "tenant":{
            "description":"",
            "enabled":true,
            "id":"d6429737322249ac9c60bc5bb659fa28",
            "name":“demo"
         },
         "audit_ids":[
            "mIa_TZf-RX6W5jwEPMR2cg"
         ]
      },
      ... (output truncated)
```

### Buckets

This section will show how to interact with Buckets.

#### PUT/v1/{account}/{bucket}

##### Create a Bucket

Creates a Bucket (or a Container).

You do not need to check if a container already exists before issuing a PUT operation because the operation is idempotent: It creates a container or updates an existing container, as appropriate.

**CURL Request:**

```
curl -i https://objects-east.cloud.ca/v1/d6429737322249ac9c60bc5bb629fe32/uploads \
  -X PUT -H "Content-Length: 0" -H "X-Auth-Token: c7436b7a2f1a4c1fb58606fa9b4b0816"
```

**CURL Response:**

```
HTTP/1.1 201 Created
Content-Length: 0
Content-Type: text/html; charset=UTF-8
X-Trans-Id: tx7f6b7fa09bc2443a94df0-0052d58b56
Date: Mon, 16 Mar 2015 23:01:50 GMT
```

#### GET/v1/{account}/{bucket}

##### Show bucket details and list objects

Shows details for a specified bucket and lists objects.

Specify query parameters in the request to filter the list and return a subset of object names. Omit query parameters to return the complete list of object names that are stored in the container, up to 10,000 names. The 10,000 maximum value is configurable. To view the value for the cluster, issue a GET /info request.

**Normal response codes:** 200,204
**Error response codes:** NotFound(404)

**CURL Request:**

```
curl -i https://objects-east.cloud.ca/v1/d6429737322249ac9c60bc5bb629fe32/Pictures \
  -X GET -H "X-Auth-Token: c7436b7a2f1a4c1fb58606fa9b4b0816"
```

**CURL Response:**

```
HTTP/1.1 200 OK
Content-Length: 179
X-Container-Object-Count: 7
Accept-Ranges: bytes
X-Storage-Policy: Policy-0
X-Container-Bytes-Used: 1661152
X-Timestamp: 1424957110.29889
Content-Type: text/plain; charset=utf-8
X-Trans-Id: tx7c235b898f534704a8505-0055084060
Date: Tue, 17 Mar 2015 14:55:28 GMT
Apache CloudStack Logo With Cloud Monkey.ai
cloudops_logo.eps
cloudops_logo_150.png
cloudops_logo_300.png
cloudops_logo_cloud-01.png
cloudops_logo_square.jpg
firefighter-tarp.jpg
```

#### DELETE/v1/{account}/{bucket}

##### Delete a Bucket

Deletes an empty Bucket.

This operation fails unless the bucket is empty. An empty bucket has no objects.

**Normal response codes:** 204
**Error response codes:** NotFound(404), Conflict(209)

**CURL Request:**

```
curl -i https://objects-east.cloud.ca/v1/d6429737322249ac9c60bc5bb629fe32/uploads \
  -X DELETE -H "X-Auth-Token: c7436b7a2f1a4c1fb58606fa9b4b0816"
```

**CURL Response:**

```
HTTP/1.1 204 No Content
Content-Length: 0
Content-Type: text/html; charset=UTF-8
X-Trans-Id: tx7f6b7fa09bc2443a94df0-0052d58b56
Date: Mon, 16 Mar 2015 23:01:50 GMT
```

### Objects

This section will show how to interact with Objects.

#### PUT/v1/{account}/{bucket}/{object}

##### Create or replace object

Creates a new object with specified data content and metadata.

The PUT operation always creates a new object. If you use this operation on an existing object, you replace the existing object and metadata rather than modifying the object. Consequently, this operation returns a 201 Created status code. If you use this operation to copy a manifest object, the new object is a normal object and not a copy of the manifest. Instead it is a concatenation of all the segment objects. This means that you cannot copy objects larger than 5 GB.

**Normal response codes:** 201
**Error response codes:** timeout (408), lengthRequired (411), unprocessableEntity (422)

**CURL Request:**

```
curl -i https://objects-east.cloud.ca/v1/d6429737322249ac9c60bc5bb629fe32/uploads/ \
  -T myobject.txt \
  -X PUT \
  -H "Content-Type: text/html"\
  -H "X-Auth-Token: c7436b7a2f1a4c1fb58606fa9b4b0816"
```

**CURL Response:**

```
HTTP/1.1 100 Continue
HTTP/1.1 201 Created
Last-Modified: Tue, 17 Mar 2015 15:08:21 GMT
Content-Length: 0
Etag: d95679752134a2d9eb61dbd7b91c4bcc
Content-Type: text/html
X-Trans-Id: tx02828f7e1367494488e6e-0055084364
Date: Tue, 17 Mar 2015 15:08:20 GMT
```

#### GET/v1/{account}/{bucket}/{object}

##### Get object content and metadata

Downloads the object content and gets the object metadata.

This operation returns the object metadata in the response headers and the object content in the response body. If this is a large object, the response body contains the concatenated content of the segment objects. To get the manifest instead of concatenated segment objects for a static large object, use the multipart-manifest query parameter.

**Normal response codes:** 200
**Error response codes:** NotFound (404)

**CURL Request:**

```
curl -i https://objects-east.cloud.ca/v1/d6429737322249ac9c60bc5bb629fe32/uploads/myobject.txt \
  -X GET \
  -H "X-Auth-Token: c7436b7a2f1a4c1fb58606fa9b4b0816"
```

**CURL Response:**

```
HTTP/1.1 200 OK
Content-Length: 12
Accept-Ranges: bytes
Last-Modified: Tue, 17 Mar 2015 15:16:39 GMT
Etag: 9e8bde8ad2d571a03e1c95d0c2ead964
X-Timestamp: 1426605398.84480
Content-Type: text/html
X-Trans-Id: tx2197e9ed2bfd4e458d239-0055084567
Date: Tue, 17 Mar 2015 15:16:55 GMT
Hello Dear!
```

#### DELETE/v1/{account}/{bucket}/{object}

##### Delete an object

Permanently deletes an object from the object store.

You can use the COPY method to copy the object to a new location. Then, use the DELETE method to delete the original object. Object deletion occurs immediately at request time. Any subsequent GET, HEAD, POST, or DELETE operations return a 404 Not Found error code. For static large object manifests, you can add the ?multipart-manifest=delete query parameter. This operation deletes the segment objects and if all deletions succeed, this operation deletes the manifest object.

**Normal response codes:** 204
**Error response codes:** 400, 500, ...

**CURL Request:**

```
curl -i https://objects-east.cloud.ca/v1/d6429737322249ac9c60bc5bb629fe32/uploads/myobject.txt \
  -X DELETE \
  -H "X-Auth-Token: c7436b7a2f1a4c1fb58606fa9b4b0816"
```

**CURL Response:**

```
HTTP/1.1 204 No Content
Content-Length: 0
Content-Type: text/html; charset=UTF-8
X-Trans-Id: tx6fdb2d8ca1334f63b95f9-0055084c04
Date: Tue, 17 Mar 2015 15:45:08 GMT
```

### More Information?

Some other call exists. Please visit the OpenStack Swift API reference guide available on this link.
