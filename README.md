# piranhanet-web-deploy
Deploy tool for PiranhaNET on the web

Pre-requisites:
- Docker and Docker Compose
- Vault

## Usage

## Troubleshooting

You may see this error on docker pull: `Error response from daemon: error from registry: unauthorized`. This means you
need to login to the ghcr.io registry with `docker login ghcr.io`. You will need to provide your GitHub username and
personal access token. 

