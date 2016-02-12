# Todo Backend Couch

This project implements the Todo Backend spec using Express, CouchDB, and Nano.

## Installation (local)

1. Install and start [CouchDB](http://couchdb.apache.org/)
1. Add a new admin user to Couch through the web UI (`todoService` / `password` are the default settings)
1. Clone this repo
1. Make sure you have Node >= 5.5 installed.
1. `npm install`
1. `node index.js`

## Installation (Vagrant)

Currently, we do not have an image for couch, so the app will always return a `500 Internal Server Error`. We will be adding a CouchDB instance with the correct networking settings to the Vagrant config in the near future.

1. Install [Packer](https://www.packer.io/intro/getting-started/setup.html)
2. Install [Vagrant](https://www.vagrantup.com/docs/installation/)
3. Clone this repo
4. Build the image:
```shell
./create-image.sh
```
5. Start Vagrant:
```shell
vagrant up
```

## Startup Options
This app uses the environment variables for runtime configuration:

##### `TODOS_COUCH_URL`
URL for connecting to CouchDB. This must include the authentication parameters and port if it is non-80 (or 443 for SSL), e.g. `http://username:password@host:port`

##### `TODOS_APP_PORT`
The port the app is configured to listen for HTTP requests on.

##### `SERVICE_URL_BASE`
The base URL for retrieving todos, e.g. `http://mypublicip.com`. This is meant to allow serviced requests to provide a URL that will hit a load balancer instead of the currently running instance.

#### Example 

```bash
TODOS_COUCH_URL="https://todos:pswd@couch-instance-01" \
TODOS_APP_PORT=9849 \
SERVICE_URL_BASE="https://myservice.com/api/todos" \
node index.js
```
