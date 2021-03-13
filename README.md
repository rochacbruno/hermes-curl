# Hermes cURL

Hermes cURL is a lightweight wrapper on top of cURL that provides reusable HTTP request configurations in YAML. Configuration files can import attributes from other files which allows for common settings such as hostnames and authentication headers to be shared by multiple cURL calls.

## Usage

Base configuration for an entire API:

```yaml
# api_base.yml
headers:
  Authorization: Token MySecretAPIToken
  Content-Type: application/json
host: localhost:5000
curl_flags:
   "--location":
```

Configuration for a specific endpoint:

```yaml
# api.yml
from: api_base.yml
method: PUT
path: /my/api
body: >
  {"hello": "world"}
```

Run the `hermes` command:

```
$ hermes api.yml
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   128  100   112  100    16   3960    565 --:--:-- --:--:-- --:--:--  4000
{
   "msg": "hello Mr world"
}
```

## Configuration file reference

- `from` (optional): specify a path to another configuration file to inherit configurations from. This path is relative to the current file.
- `path` (requires): path on the server to send the request to, including any query params.
- `method` (required): HTTP method to use.
- `host` (required): server host, including protocol and port.
- `headers` (optional): dictionary of headers in the form. Ex`Header: value`.
- `body` (optional): request body.
- `curl_flags` (optional): a dictionary with any other curl flags to add. Ex `"--cacert: certfile"`.

## Installation

```
python3 -m pip install hermes-curl
```
