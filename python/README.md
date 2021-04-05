# Python YOURLS PID service

### Description
Extension of [Pyourls3](https://pypi.org/project/pyourls3/) for api based PID support and bulk uploading.
Includes example dockerfiles to show the functionality of the api from inside docker environment.
See usage to explore optional arguments.

### Requires
- If running via Docker: Docker & docker-compose.
- If running via python script: [pyourls3](https://pypi.org/project/pyourls3/).

### Installation

1. Clone the repository to your own personal folder and start YOURLS service. <br>
   ```
   git clone https://github.com/webb-ben/geoconnex.us
   cd geoconnex.us/simple-yourls<br>
   docker-compose up -d --build
   ```
2. Open yourls admin interface at `http://[HOSTNAME]/admin` and install yourls.
3. Enable plugins before adding any entries. 
4. To populate database (with Docker):
 - From namespaces & namespaces is located in `.` :
   ```
   docker build -t namespaces -f Dockerfile-namespaces .
   docker run -i -t \
    --mount type=bind,source="$(pwd)"/namespaces/,dst=/data/ \
    --network simple-yourls_default \
    namespaces
   ``` 
 - From BACKUP & backup_current is located in `.` :
   ```
   docker build -t backup -f Dockerfile-backup .
   docker run -i -t \
    --mount type=bind,source="$(pwd)"/backup_current/,dst=/data/ \
    --network simple-yourls_default \
    backup
   ```
  - From URL & urls are declared in the CMD list of the Dockerfile:
   ```
   docker build -t url -f Dockerfile-url .
   docker run -i -t \
    --network simple-yourls_default \
    url
   ``` 

#### Usage
The python files can also be run locally on To see argparser defaults & options run:
- `python yourls_client.py -h`
- `python populate_db.py -h`

### License
This service is licensed under the [MIT License](LICENSE).