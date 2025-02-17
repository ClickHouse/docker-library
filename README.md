# Repository for sources of ClickHouse in [Docker Official Library][DOL]
[DOL]: https://github.com/docker-library/official-images
[CH/CH]: https://github.com/ClickHouse/ClickHouse/

The repo provides sources for [clickhouse](https://hub.docker.com/_/clickhouse).<!-- break false underscore_ -->

The content here is autogenerated by the [official_docker.py](https://github.com/ClickHouse/ClickHouse/blob/master/tests/ci/official_docker.py) and shouldn't be edited manually.

## Update process

### Images update

The script has two working modes:

- Generating source-tree for `docker build` command in `server` or `keeper` directory
- Generating LDF (Library Definition File) for [official-images][DOL] repository

After new releases are created, one should follow the next steps:

0. Clone this repository to `$LDF_SRC_DIR` and [ClickHouse/ClickHouse][CH/CH] somewhere nearby.
0. Run the script from [ClickHouse/ClickHouse][CH/CH] repository:  
  `python tests/ci/official_docker.py generate-tree -vvv --directory $LDF_SRC_DIR --dockerfile-glob Dockerfile.ubuntu --build --commit`
0. Regenerate the LDF:  
  `python tests/ci/official_docker.py generate-ldf -vvv --directory ../docker-library --dockerfile-glob Dockerfile.ubuntu --commit`
0. Push changes to our [fork](https://github.com/ClickHouse/docker-library-official-images) of [docker-library][DOL] and create a pull request in the upstream.

### Documentation update
[readme.src]: https://github.com/ClickHouse/ClickHouse/tree/master/docker/server/README.src

The documentation sources live in [docker/server/README.src][readme.src] directory.

0. Update the corresponding part of the sources.
0. Launch [README.sh](https://github.com/ClickHouse/ClickHouse/blob/master/docker/server/README.sh) and update the `README.md` in upstream.
0. Copy [sources][readme.src] to our [fork](https://github.com/ClickHouse/docker-library-docs) of [docker-library/docs](https://github.com/docker-library/docs), **remove the part between comments, related to our repository**, and make a pull request.
