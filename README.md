# Hermes cURL

Hermes cURL is a lightweight wrapper on top of cURL that provides the ability to create reusable configurations for cURL. Configuration files can inherit configurations from other files which allows for common settings such as hostnames and authentication headers to be shared by multiple cURL configs.

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

- `from`: specify a base configuration. This should be a relative path to the current file.
- `headers`: dictionary of headers.
- `path`: path on the server to send the request to.
- `method`: HTTP method to use
- `host`: server host, including protocol and port.
- `body`: request body
- `curl_flags`: a dictionary with any other curl flags to add. ex `"--cacert: certfile"`

## Installation

```
git clone git@github.com:newswangerd/hermes-curl.git
cd hermes-curl
pip install -r requirements.txt
pip install -e .
```
