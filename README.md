[![Go Report Card](https://goreportcard.com/badge/github.com/wroge/wms)](https://goreportcard.com/report/github.com/wroge/wms)

# Web Map Service - Manager

A command-line-tool for easy use of Web Map Services. 
You can download WMS-Tiles and check the Capabilities of a service. Including:

- Set specific requests in a configuration file
- Get helpful error messages
- Automatic Coordinate Transformation into a supported format
- Download several bounding boxes at the same time

## Install

- Linux (i386/x86_64)
- MacOS (i386/x86_64)
- Windows (i386/x86_64)

[Releases](https://github.com/wroge/wms/releases)

Alternatively, you can install ```wms``` via Homebrew, Scoop or Docker. Of course, you can also create the executable file from source.

### Homebrew (MacOS)

```
brew install wroge/tap/wms
```

### Scoop (Windows)

```
scoop bucket add app https://github.com/wroge/scoop-bucket
scoop install wms
```

### Docker

```
docker pull wroge/wms:latest
docker run -v "$(pwd)/output:/output" -v "$HOME/wms-config:/wms-config" wroge/wms
```

### From Source

This Go-Project is using ```go mod```. Please clone this repository outside of ```GOPATH```.

```
git clone https://github.com/wroge/wms.git
cd wms
go build -o wms ./cli
```

## Features

### Configuration

You can change the configuration using ```--save``` or edit the configuration file ```$HOME/wms-config/.wms.yaml``` directly. 

```
wms map -u http://ows.terrestris.de/osm/service -n example -e 25832 -l TOPO-WMS --save terrestris --dry-run
wms cap terrestris
wms map terrestris -b 565000,5930000,570000,5935000 -w 1000
```

### Helpful error-messages

You can look up the capabilities ```wms cap``` or just try it out.

```
wms cap -u http://ows.terrestris.de/osm/service -l
wms map -u http://ows.terrestris.de/osm/service -l abc
Error: Invalid Layer: abc
Valid Layers: [OSM-WMS OSM-Overlay-WMS TOPO-WMS TOPO-OSM-WMS SRTM30-Hillshade SRTM30-Colored SRTM30-Colored-Hillshade SRTM30-Contour]
```

### Automatic Coordinate Transformation

Supported by [go-coo](https://github.com/wroge/go-coo).  Some WMS allow only a few coordinate reference systems. With this program you can choose from a larger number of EPSG codes. Please open an issue in the [go-coo](https://github.com/wroge/go-coo) repository to support your specific system.

```
wms map -u http://ows.terrestris.de/osm/service -e 12345
Error: Invalid EPSG: 12345
Valid EPSGs: [4326 3857 900913 25833 5668 5669 31467 31468 31469 32632 3067 4647 4462 25832 31466 32633 5650]
```

### Download several bounding boxes

You can create a text file that contains all the required bounding boxes and download them at the same time.

```
cat $HOME/bbox-wgs84.txt
9,52,9.2,52.2
9.2,52,9.4,52.2
9.4,52,9.6,52.2
wms map -u http://ows.terrestris.de/osm/service -B $HOME/bbox-wgs84.txt -w 1000 -e 4326
```

### More

- Automatic image size calculation (width, height or dpi & scale)
- Expand & Cut bounding boxes (interesting for dynamically generated texts and symbols)
- Basic Authentication
- ```wms map --help"```
- ```wms cap --help"```

## FAQ

...For any problems/questions please open an issue.