#.http file for Visual Studio Code plugin: Rest Client

```
@host=localhost
@port=8443
@token= ttt

POST https://{{host}}:{{port}}/... HTTP/1.1
content-type: application/json
Authorization: XXX

{
  
}

###
GET https://{{host}}:{{port}}/... HTTP/1.1
Authorization: xxx
X-Auth-Token: {{token}}
content-type: application/json
```