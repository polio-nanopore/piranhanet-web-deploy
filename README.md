# piranhanet-web-deploy
:fish: :spider_web: :fish: :spider_web: :fish: :spider_web:

Deploy tool for [PiranhaNET](https://github.com/polio-nanopore/piranhaNET/) on the web.

The tool uses [Docker Compose](https://docs.docker.com/compose/) to run the PiranhaNET web front end and API. It optionally also runs an [nginx](https://nginx.org/) proxy
and [acme-buddy](https://github.com/reside-ic/acme-buddy) for certificate management. 

Pre-requisites:
- [Docker](https://docs.docker.com/get-docker/)
- [Vault](https://www.hashicorp.com/en/products/vault)

## Usage

All functionality is available through the `./piranhanet-web-deploy` script. Run the following steps to get started on a new server.

1. Clone this repository
2. `./piranhanet-web-deploy configure [ENVIRONMENT]` where environment may be "local", "dev" or "production". This copies the relevant .env file from the `config` folder to repo root .env
3. `./piranhanet-web-deploy pull` - pulls latest docker images
4. `./piranhanet-web-deploy up` - runs all containers

When a redeploy is required, run `./piranhanet-web-deploy down` to stop all containers, then repeat steps 3.-4.

## Local testing

Use the steps above with the "local" enivronment, i.e. start with `./piranhanet-web-deploy configure local`.
For local testing, a no-proxy configuration will be used which will not run the proxy or acme-buddy. 

The web app should be available locally at [http://localhost:5173](http://localhost:5173).

## Configuration

The following configurations are available in the `config folder`:
- local: for local testing, with no proxy
- dev: for deploying to piranhanet-dev.dide.ic.ac.uk
- production: for deploying to piranhanet.dide.ic.ac.uk

Each configuration file contains the following values:
- `DOMAIN` - the domain or base URL of the application
- `API_URL` - the base URL at which the web front end will find the API
- `DOCKER_COMPOSE_PROFILE` - this should be `proxy` or `no-proxy`
- `API_REF` - set this to a branch name to test a github branch of the PiranhaNET API. Defaults to main.
- `WEB_REF` - set this to a branch name to test a github branch of the PiranhaNET Web front end. Defaults to main.

## Troubleshooting

You may see this error on docker pull: `Error response from daemon: error from registry: unauthorized`. This means you
need to login to the ghcr.io registry with `docker login ghcr.io`. You will need to provide your GitHub username and
personal access token. 

