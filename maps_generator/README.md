# Dockerfile for [maps_generator](https://github.com/mapsme/omim/tree/master/tools/python/maps_generator)

## Setup
You must have [docker](https://docs.docker.com/install/) and complete the following steps:

0. Create and change directory:
```sh
$ mkdir ~/Projects && cd ~/Projects
```
1. Clone this repo:
```sh
Projects$ git clone https://github.com/mapsme/dockerfiles.git
Projects$ cd dockerfiles/maps_generator 
```
2. Build docker container
```sh
maps_generator$ docker build --build-arg [TAG=release-91] -t maps_generator . 
```
The default TAG is master.

## Usage
A. For example you want to generate 'Russia_Samara Oblast' map. 

0. Make directory for maps generation:
```sh
$ cd ~/Projects && mkdir generation
```

1. Make settings file:
```sh
Projects$ vim generation/config.ini
```
```ini
[Main]
DEBUG: 0

[External]
PLANET_URL: https://download.geofabrik.de/russia/volga-fed-district-latest.osm.pbf
PLANET_MD5_URL: https://download.geofabrik.de/russia/volga-fed-district-latest.osm.pbf.md5
SUBWAY_URL: http://osm-subway.maps.me/mapsme/latest.json
```

2. Run docker cantainer:
```sh
Projects$ docker run -v ~/Projects/generation:/mapsme/generation: --rm -t maps_generator --config=/mapsme/generation/config.ini --countries="Russia_Samara Oblast" --skip="coastline"
```

3. Check maps:
```sh
Projects$ ls generation/
```
The output will look like this
```
2019_06_27__16_36_15  config.ini  generation.log  planet.o5m  planet.o5m.lock  planet.o5m.md5
```

B. For example you want to generate 'Russia_Samara Oblast' map. 

0. Make directory for maps generation:
```sh
$ cd ~/Projects && mkdir generation
```

1. Make settings file:
```sh
maps_generator$ vim generation/maps_generator_config.ini
```
```ini
[Main]
DEBUG: 0

[External]
PLANET_URL: http://download.geofabrik.de/asia/uzbekistan-latest.osm.pbf
PLANET_MD5_URL: http://download.geofabrik.de/asia/uzbekistan-latest.osm.pbf.md5
SUBWAY_URL: http://osm-subway.maps.me/mapsme/latest.json
```

2. Run docker cantainer:
```sh
Projects$ docker run -v ~/Projects/generation:/mapsme/generation: --rm -t maps_generator --config=/mapsme/generation/config.ini --countries="Uzbekistan" --skip="coastline"
```

3. Check maps:
```sh
Projects$ ls generation/
```

