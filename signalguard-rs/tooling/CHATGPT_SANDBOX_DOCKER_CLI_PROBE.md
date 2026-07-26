# ChatGPT Sandbox Portable Docker CLI Probe

Date: 2026-07-26

This supplement records the tested distinction between a portable Docker client and an actually available Docker daemon inside the ChatGPT sandbox.

## Artifact bridge

A temporary GitHub Actions workflow packaged:

- Docker CLI `28.0.4`;
- Docker Compose plugin `2.38.2`;
- a wrapper that installs the plugin under a bundle-local `DOCKER_CONFIG`.

The GitHub artifact was `39298539` bytes with digest:

`sha256:98c56b18c4dac5fa2885dc15ddf684ab5b39c0d0e33af663dc860bc011ec0ace`

The GitHub connector downloaded the artifact and ChatGPT mounted it under `/mnt/data`.

## Executed successfully in the ChatGPT Debian 13 sandbox

- `docker --version`;
- `docker compose version`;
- `docker compose -f <minimal-compose-file> config`.

The Compose command parsed and rendered a Redis service definition without requiring a daemon.

## Expected daemon failure

`docker info` exited with status `1` and reported that it could not connect to:

`unix:///var/run/docker.sock`

No Docker socket or daemon is present in the sandbox.

## Operational conclusion

A web worker can be provisioned with portable Docker CLI and Compose binaries for static tasks such as:

- `docker compose config`;
- Compose syntax validation;
- client-side configuration inspection;
- version reporting.

This does not provide container execution. `docker run`, image pulls, container networking, and daemon-backed integration tests must remain on GitHub Actions unless a separate usable daemon is supplied.

SignalGuard Redis tests should run against the already verified portable `redis-server` bundle rather than depending on nested Docker.

The temporary experiment branch was reset after the probe; no experimental workflow remains in the active coordination branch.
