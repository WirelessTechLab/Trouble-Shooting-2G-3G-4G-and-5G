# Service-Based Architecture (SBA) General Issues

### Troubleshooting Steps: 

- Check HTTP/2 connectivity between NFs 

- Verify TLS security (if enabled) 

- Review OAuth 2.0 token validation 

- Check JSON schema compliance 

- Verify API versioning 

- Review error handling and retry mechanisms 

### PCAP Analysis: 

- HTTP/2 Connection: 

- Verify TLS handshake (if security enabled) 

- Check ALPN: h2 (HTTP/2) 

- Look for SETTINGS frame exchange 

- Verify HPACK header compression 

### SBI HTTP Requests: 

- Check Method: GET, POST, PUT, PATCH, DELETE 

- Verify :authority pseudo-header: Target NF FQDN 

- Check :path: API endpoint URI 

- Look for 3gpp-Sbi- headers*: 

    - 3gpp-Sbi-Target-apiRoot: Target API 

    - 3gpp-Sbi-Discovery-*: Discovery parameters 

    - 3gpp-Sbi-Message-Priority: Message priority 

    - 3gpp-Sbi-Max-Rsp-Time: Response timeout 

- Verify Content-Type: application/json or application/problem+json 

- Check OAuth token in Authorization header (if OAuth used) 

### SBI HTTP Responses: 

- Verify :status code 

- Check Content-Type: application/json 

- Look for Location header (for created resources) 

- Check 3gpp-Sbi- response headers* 

### Error Responses: 

- `4xx Client Errors`: 

    - 400: Bad Request (invalid JSON) 

    - 401: Unauthorized (missing/invalid token) 

    - 403: Forbidden (insufficient permissions) 

    - 404: Not Found (resource doesn't exist) 

    - 405: Method Not Allowed 

    - 409: Conflict (resource already exists) 

    - 415: Unsupported Media Type 

    - 429: Too Many Requests (rate limit) 

- `5xx Server Errors`: 

    - 500: Internal Server Error 

    - 502: Bad Gateway 

    - 503: Service Unavailable (NF overload) 

    - 504: Gateway Timeout 

- `Check ProblemDetails JSON in response body`: 

    - type: Error type URI 

    - title: Error title 

    - status: HTTP status code 

    - detail: Detailed error description 

    - instance: Specific instance of error 

    - cause: 3GPP-specific cause 

    - invalidParams: Invalid parameters 