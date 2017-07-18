# Using Docker With SRA Project

A quick attempt to get docker up and running. This should allow easier building
of the database and running tools like `attribute_selector`.

This requires [docker-compose](https://docs.docker.com/compose/). I have only
tested these on Linux, but everything should work on OSX and Windows as well.

## Prepare Database

The MongoDB is central to the SRA project. This sections shows how to download
and restore a pre-built version of the database, or build the database from
scratch.

### Restore A Pre-Built Databases `download_database`

To download the pre-built database, containing the `ncbi` and `biometa` collections, run `download_database`.

```bash
git clone https://github.com/jfear/simple_docker.git
cd simple_docker
docker-compose run download_database
```

### Build Database from Scratch

If you want to build the database yourself then run `sra2mongo` and
`build_biometa` sequentially.

#### `sra2mongo`

`sra2mongo` will download and generate a collection called `ncbi` in a database
called `sra`. The docker container will add a hidden folder called
`./data/.cache`.

```bash
git clone https://github.com/jfear/simple_docker.git
cd simple_docker
docker-compose run sra2mongo
```

#### `build_biometa`

The `biometa` collection is a slight re-organization of the `ncbi` collection
focused on biological sample information. It is indexed by BioSample accession.
To build the `biometa` collection run.

```bash
docker-compose run build_biometa
```

## Run Attribute Selector

Attribute selector is a command line tool which allows the user to look at
attribute types and keep/merge/ignore them.
[More details](https://github.com/jfear/biometalib#attribute-selector)

### Using a local database

If you either restored the pre-built database or created the database from
scratch you can run `attribute_selector` using:

```bash
docker-compose run attribute_selector
```

### Using a remote database
If you do not want to mess with getting a local version of the database
running, but still want to run `attribute_selector` you are in luck because I
have a public version of the database running. To run using
this database run:

```bash
docker-compose run attribute_selector_underground
```
