## Running the services in dev mode

Starting the services with exposed ports by including the `docker-compose.dev.yml` file as following:

### default

`docker-compose -f docker-compose.yml -f docker-compose.dev.yml up`

### minio

`docker-compose -f docker-compose.minio.yml -f docker-compose.dev.yml up`

### full

`docker-compose -f docker-compose.full.yml -f docker-compose.dev.yml up`

## Releasing a new version

We use semver.

Every commit to master triggers [CI via GH Actions](https://github.com/sorry-cypress/sorry-cypress/tree/master/.github/workflows), which builds new docker images, assign tags and pusher the new images to dockerhub.

After pushing a new tagged please go ahead and create a new Github [release](https://github.com/sorry-cypress/sorry-cypress/releases) with a summary and attributions.

### Prevent CI

Add `skip ci` to commit message to skip running CI

### Releasing `latest` tag

Pushing to master automatically created new docker images with `latest` tags

### Releasing tagged version e.g. `v1.0.0-beta.4`

1. Run `yarn release` to create a new release.
2. Push to master. Push to master, together with tags `git push origin master --tags`. Pushing to master will trigger CI that will actually update dockerhub.

Pushing a properly formatted (semver) git tag starts release of dockerhub images tagged accordingly. E.g. `v0.5.2` will release dockerhub tags `v0, v0.5, v0.5.2`.

The script does the following behind the scenes:

- Update all `package.json` files (we release all together and do not increase / release individual packages version)
- Commit with message, e.g. `v0.5.2`
- Add git tag, e.g. `git tag v0.5.2`
