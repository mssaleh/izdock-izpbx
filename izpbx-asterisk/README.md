# izpbx-asterisk

izPBX is a TurnKey Cloud Native Telephony System powered by Asterisk Engine and FreePBX Management GUI

for more info: https://github.com/ugoviti/izdock-izpbx

# Docker Development

## Build

Asterisk 18:  
`docker build --pull --rm --build-arg APP_VER=dev-18 --build-arg APP_DEBUG=1 --build-arg APP_VER_BUILD=1 --build-arg APP_BUILD_COMMIT=fffffff --build-arg APP_BUILD_DATE=$(date +%s) --build-arg ASTERISK_VER=18.5.1 -t izpbx-asterisk:dev-18 .`

Asterisk 16:  
`docker build --pull --rm --build-arg APP_VER=dev-16 --build-arg APP_DEBUG=1 --build-arg APP_VER_BUILD=1 --build-arg APP_BUILD_COMMIT=fffffff --build-arg APP_BUILD_DATE=$(date +%s) --build-arg ASTERISK_VER=16.16.0 -t izpbx-asterisk:dev-16 .`


## Run

### Docker Run:
Start MySQL:  
`docker run --rm -ti -p 3306:3306 -v ${PWD}/data/db:/var/lib/mysql -e MYSQL_DATABASE=asterisk -e MYSQL_USER=asterisk -e MYSQL_ROOT_PASSWORD=CHANGEM3 -e MYSQL_PASSWORD=CHANGEM3 --name izpbx-db mariadb:10.5`

Start izPBX:  
`docker run --rm -ti --network=host --privileged --cap-add=NET_ADMIN -v ${PWD}/data/izpbx:/data -e MYSQL_SERVER=127.0.0.1 -e MYSQL_DATABASE=asterisk -e MYSQL_USER=asterisk -e MYSQL_ROOT_PASSWORD=CHANGEM3 -e MYSQL_PASSWORD=CHANGEM3 -e APP_DATA=/data --name izpbx izpbx-asterisk:dev-18`


### Docker Compose:

Asterisk 16:  
`docker-compose down ; docker-compose -f docker-compose.yml -f docker-compose-dev-16.yml up`

Asterisk 18:  
`docker-compose down ; docker-compose -f docker-compose.yml -f docker-compose-dev-18.yml up`
