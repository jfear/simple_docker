# Using Docker With SRA Project

This is a just a quick attempt to get docker up and running and working with
docker containers. Currently I am playing with running a database server along
with running either `sra2mongo` or `attribute_selector`.

This requires [docker-compose](https://docs.docker.com/compose/). I have only
tested these on Linux, but everything should work on OSX and Windows as well.

## Restore A Pre-Built Databases `download_database`

To download a database containing the `ncbi` and `biometa` collection run `download_database`.

```bash
git clone https://github.com/jfear/simple_docker.git
cd simple_docker
docker-compose run download_database
```

## Build Database from Scratch

If you want to build the database yourself then run `sra2mongo` and
`build_biometa` sequentially.

### `sra2mongo`

`sra2mongo` will download and generate a collection called `ncbi` in a database
called `sra`. The docker container will add a hidden folder called `.cache` in
the data folder. To run you need `docker-compose` installed.

```bash
git clone https://github.com/jfear/simple_docker.git
cd simple_docker
docker-compose run sra2mongo
```

### `build_biometa
To build the `biometa` collection run.

```bash
docker-compose run build_biometa
```

# Run Attribute Selector
## Using a local database

If you either restored the pre-built database or created the database from
scratch you can run `attribute_selector` using:

```bash
docker-compose run attribute_selector
```

## Using a remote database
If you do not want to mess with getting a local version of the database
running, but still want to run `attribute_selector` you are in luck because I
have a public version of the database running on my web server. To run using
this database run:

```bash
docker-compose run attribute_selector_underground
```
