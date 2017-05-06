# A FastCGI MapServer instance

[![](https://images.microbadger.com/badges/version/carletes/mapserver.svg)](https://microbadger.com/images/carletes/mapserver "Get your own image badge on microbadger.com")
[![](https://images.microbadger.com/badges/image/carletes/mapserver.svg)](https://microbadger.com/images/carletes/mapserver "Get your own image badge on microbadger.com")
[![](https://images.microbadger.com/badges/commit/carletes/mapserver.svg)](https://microbadger.com/images/carletes/mapserver "Get your own commit badge on microbadger.com")

This image implements a [MapServer](http://mapserver.org/) instance accepting [FastCGI](https://en.wikipedia.org/wiki/FastCGI) connections.

It listens by default on port 9001, and expects MapServer map files and related data to be available in a volume mounted on `/data`.


## Usage

The following will start a MapServer instance listening on port 9001 for FastCGI connections, and serving MapServer data from the directory `/some/mapserver/data`:

    $ docker run \
	    --volume=/some/mapserver/data:/data:ro \
		carletes/mapserver

If you want to listen on a different port, use the `FCGI_LISTEN_PORT` environment variable:

    $ docker run \
	    --volume=/some/mapserver/data:/data:ro \
		--env=FCGI_LISTEN_PORT=9022 \
		carletes/mapserver

You will need a web server to expose MapServer to your clients via HTTP. The GitHub repository [carletes/docker-mapserver-example](https://github.com/carletes/docker-mapserver-example) shows a way of doing it.


## Configurable parameters

The following environment variables can set in order to tweak the behaviour of MapServer:

| Variable              | Description                                 | Default value |
|-----------------------|---------------------------------------------|---------------|
| `FCGI_LISTEN_ADDRESS` | Listening address for FastCGI requests      | 0.0.0.0       |
| `FCGI_LISTEN_PORT`    | Listening port for FastCGI requests         | 9001          |
| `FCGI_NPROC`          | Nimber of FastCGI child processes to spawn  | 1             |
| `FCGI_BACKLOG`        | TCP connection backlog for FastCGI requests | 1024          |
| `FCGI_UID`            | Unix UID of FastCGI process                 | `mapserver`   |
| `FCGI_GID`            | Unix GID of FastCGI process                 | `mapserver`   |

All [MapServer environment variables](http://mapserver.org/environment_variables.html) may be specified as well. This images runs with the following non-default MapServer environment variables:

| MapServer variable | Value used in this image         |
|--------------------|----------------------------------|
| `MS_ERRORFILE`     | `stderr`                         |
