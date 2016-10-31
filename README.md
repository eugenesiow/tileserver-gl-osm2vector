## Setting up a Personal Vector Tile Server with OpenStreetMaps

If you have need of a personal vector tile server, serving OpenStreetMap tiles from the mbtiles format inexpensively with Tileserver GL, utilising the great work from the OSM2VectorTiles project and open source Mapbox styles, this is a quick tutorial on how to.

### Get your tiles

Download your tiles from OSM2VectorTiles:

        http://osm2vectortiles.org/downloads/

You might want the world.mbtiles:

        https://osm2vectortiles-downloads.os.zhdk.cloud.switch.ch/v2.0/planet_2016-06-20_3d4cb571d3d0d828d230aac185281e97_z0-z14.mbtiles

Or your own city, like:

        https://osm2vectortiles-downloads.os.zhdk.cloud.switch.ch/v2.0/extracts/southampton_england.mbtiles

### Setup the environment with Docker

1. Clone this repository `git clone https://github.com/eugenesiow/tileserver-gl-osm2vector`
2. Put your `.mbtiles` file into the folder `tileserver-gl-osm2vector`.
3. Install [https://docs.docker.com/engine/installation/](docker).
4. Modify `config.json` by changing `world.mbtiles` to the `.mbtiles` file you obtained from the previous section. For example, if you had downloaded the Southampton map, change:

        "world": {
            "mbtiles": "world.mbtiles"
        }        
to
        
        "southampton": {
            "mbtiles": "southampton_england.mbtiles"
        }
        
5. Modify `/mapbox-gl-styles/styles/bright-v9.json` by changing `http://localhost:8080/data/world.json` to the name of your map. For example, if in the previous step you've changed `world` to `southampton`, change:

        "mapbox": {
            "url": "http://localhost:8080/data/world.json",
            "type": "vector"
        }

to

        "mapbox": {
            "url": "http://localhost:8080/data/southampton.json",
            "type": "vector"
        }
        
6. Run docker `docker run -it -v $(pwd):/data -p 8080:80 klokantech/tileserver-gl` in the directory (the `tileserver-gl-osm2vector` directory).

### Copyright

The styles Basic and Bright are derived from https://github.com/mapbox/mapbox-gl-styles therefore Mapbox Open Styles are copyright (c) 2014, Mapbox, all rights reserved.

The OSM2VectorTile project is a basis http://osm2vectortiles.org/ for this tutorial and all credit goes to their work in making the vector tiles usable and hosting the files.
