[Install Docker in Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

Generate a new SSH key and add it to the ssh-agent

```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ssl-certs/mykey.key -out ssl-certs/mycert.pem
ssh-add ssl-certs/mykey.key
```

import data into postgis

```bash
raster2pgsql -s 5070 -I -C -e -Y -F -t 256x256 data/*.tif or_forest_own | psql -U gis -d gis -h localhost -p 5432
ogr2ogr -f "PostgreSQL" PG:"host=localhost port=5432 dbname=gis user=gis password=password" "data/or_us_county.geojson" -nln or_us_county
```

Launch bash within the postgis container

```bash
sudo docker exec -it postgis-postgis-1 /bin/bash
```
