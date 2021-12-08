# python-tiny-http-server

A simple ad-hoc HTTP server for serving static pages,
similar to `python -m http.server`.

This supports:
* Basic authentication, for one or more user:password pairs, which can be specified from the command line and/or be read in from a file.
* Support for HTTPS using a cert and key file
* Support to run as CGI server, but without basic auth / HTTPS for now

## Installation

`pip install -U tiny-http-server` 

## Usage

```
usage: tiny-http-server [-h] [--cgi] [--bind ADDRESS] [--directory DIRECTORY]
                        [--port PORT] [--authfile AUTHFILE]
                        [--auth USERNAME:PASSWORD] [--cert CERT] [--key KEY]

Tiny HTTP server with optional basic authentication and https support.

optional arguments:
  -h, --help            show this help message and exit
  --cgi                 Run as CGI Server
  --bind ADDRESS, -b ADDRESS
                        Specify alternate bind address [default: 127.0.0.1]
  --directory DIRECTORY, -d DIRECTORY
                        Specify alternative directory [default: current
                        directory]
  --port PORT           Specify alternate port [default: 8000]
  --authfile AUTHFILE, -f AUTHFILE
                        If specified, a file with lines username:password
  --auth USERNAME:PASSWORD, -a USERNAME:PASSWORD
                        Add username:password to accepted authentication
  --cert CERT, -c CERT  If specified, the cert-file to use, enables https
  --key KEY, -k KEY     Key file, needed if --cert is specified
```

## Using HTTPS

This is experimental. It requires a cert and key file.

For testing this can be created for `localhost` using the command:
```bash
openssl req -x509 -out localhost.crt -keyout localhost.key -newkey rsa:2048 -nodes -sha256 -subj '/CN=localhost' -extensions EXT -config <( printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")
```

