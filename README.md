# YOURLS PID service

### Description
Attempts to mimic the this [PID service](https://github.com/SISS/PID) using [YOURLS](https://yourls.org), a more actively maintained platform.
YOURLS performs much better at scale ( > 300,000 entries), and allows for the easy modification of the capacities of the service using YOURLS plugins. 

### Requires
- Docker & docker-compose.

Community YOURLS plugins used & activated:
- [reset-urls](https://gist.github.com/ozh/a0090f46569b50835520d95f9481d9fd#file-plugin-php) 
- [always-302](https://github.com/tinjaw/Always-302) (modified to 303)
- [keep-querystring](https://github.com/rinogo/yourls-keep-query-string)
- [redirect-index](https://github.com/tomslominski/yourls-redirect-index)
- [request-forwarder](https://github.com/webb-ben/plugins/tree/master/request-forward)
- [bulk-import-and-shorten](https://github.com/vaughany/yourls-bulk-import-and-shorten)
- [sleeky-backend](https://sleeky.flynntes.com)
- change-title

YOURLS plugins developed for geoconnex
- [bulk-API-import](https://github.com/webb-ben/plugins/tree/main/bulk-api-import)
- [regex-in-urls](https://github.com/webb-ben/plugins/tree/master/regex-in-urls)

### Installation

1. Clone the repository to your own personal folder. <br>
   `git clone https://github.com/internetofwater/IoW-YOURLS`<br>
   `cd IoW-YOURLS`<br>
   `docker-compose up -d --build`
2. Open yourls admin interface and install yourls.
3. Enable all plugins before adding any entries. 

### Populating database
Under [python](python/README.md) we have built a [Dockerfile](https://github.com/internetofwater/IoW-YOURLS/blob/main/python/Dockerfile-url)
that builds a docker image designed to populate a YOURLS database with csv files formatted similarly to the geoconnex contribution format. The image is available on Dockerhub at [internetofwater/post-geoconnex](https://hub.docker.com/repository/docker/internetofwater/post-geoconnex).

The basic command is
`docker run -i -t --rm internetofwater/post-geoconnex python yourls_client.py --options <path/to/csv>` with the following options

`-s <url>` The stem of the persistent identifiers. In our case, usually `https://geoconnex.us/`

`-a <url>` The url of the PID server management layer. In our case, `https://pids.geoconnex.us`

`-u` The username (same as before)

`-p` The password (same as before)

`<path/to/csv>` can be a local directory with many CSV files, the path of a single CSV file, or the URL of a hosted CSV file.

For example usage:

``` docker run -i -t --rm internetofwater/post-geoconnex python yourls_client.py -s https://geoconnex.us/ -a https://pids.geoconnex.us -u <user> -p <password> https://raw.githubusercontent.com/internetofwater/geoconnex.us/iow/namespaces/iow/test.csv```


### License
This service is licensed under the [MIT License](LICENSE).
