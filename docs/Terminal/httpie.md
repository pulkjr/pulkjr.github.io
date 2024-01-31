# HTTPIE

HTTPIE is "A simple yet powerful command-line HTTP and API testing client for the API era.". I'm using it specifically for the output highlighting.

## Install

```bash
# Install httpie
brew update
brew install httpie
```

## Brocade FOS Switch

### Login to Switch

```bash
http POST https://10.10.10.10/rest/login -a 'user:password' -A basic

HTTP/1.1 200 OK
Authorization: Custom_Basic dG1hZG1pbjp4eHg6NWQxNzE0MGFkMTUzNjg5MTk3ZWQ0NjBjOTU3YWM5NTdkYjhmMzkyYWM5ZDMwZTZlMmRiOGEwODExZjQwOTAxNA==
Cache-Control: no-cache, no-store                                                                           
Connection: close
Content-Security-Policy: default-src 'self'; object-src 'none'; referrer 'none'; base-uri 'self'; form-action 'none'; frame-ancestors 'none'; sandbox allow-scripts; report-uri 'none'; plugin-types 'none'
Content-Type: application/yang-data+json;version=1.30.0                                                     
Date: Thu, 04 Jan 2024 16:14:45 GMT
Server: Apache                                                                                              
Strict-Transport-Security: max-age=31536000; includeSubDomains                                              
Transfer-Encoding: chunked                                                                                  
X-Content-Type-Options: nosniff      
X-Frame-Options: DENY
X-XSS-Protection: 1; mode=block
```

### Collection Switch information

```bash
http GET https://10.10.10.10/rest/running/brocade-fibrechannel-switch/fibrechannel-switch/ Authorization:'Custom_Basic dG1hZG1pbjp4eHg6NWQxNzE0MGFkMTUzNjg5MTk3ZWQ0NjBjOTU3YWM5NTdkYjhmMzkyYWM5ZDMwZTZlMmRiOGEwODExZjQwOTAxNA=='
```

response

```xml
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Connection: close
Content-Security-Policy: default-src 'self'; object-src 'none'; referrer 'none'; base-uri 'self'; form-action 'none'; frame-ancestors 'none'; sandbox allow-scripts; report-uri 'none'; plugin-types 'none'
Content-Type: application/yang-data+xml;version=1.30.0
Date: Thu, 04 Jan 2024 14:08:52 GMT
Server: Apache
Strict-Transport-Security: max-age=31536000; includeSubDomains
Transfer-Encoding: chunked
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
X-XSS-Protection: 1; mode=block

<?xml version="1.0"?>
<Response>
  <fibrechannel-switch>
    <name>10:00:d8:1f:cc:18:ac:81</name>
    <domain-id>1</domain-id>
    <fcid>16776195</fcid>
    <fcid-hex>0xfffc03</fcid-hex>
    <user-friendly-name>switch01</user-friendly-name>
    <enabled-state>2</enabled-state>
    <is-enabled-state>true</is-enabled-state>
    <operational-status>2</operational-status>
    <banner>login banner</banner>
    <up-time>38319662</up-time>
    <domain-name>domain.local</domain-name>
    <dns-servers>
      <dns-server>8.8.8.8</dns-server>
      <dns-server>8.8.4.4</dns-server>
    </dns-servers>
    <principal>0</principal>
    <ip-address>
      <ip-address>10.10.10.10</ip-address>
    </ip-address>
    <subnet-mask>255.255.255.0</subnet-mask>
    <model>173.3</model>
    <firmware-version>v8.2.3c</firmware-version>
    <ip-static-gateway-list>
      <ip-static-gateway>10.10.10.1</ip-static-gateway>
    </ip-static-gateway-list>
    <vf-id>128</vf-id>
    <fabric-user-friendly-name/>
    <ag-mode>0</ag-mode>
  </fibrechannel-switch>
</Response>
```
