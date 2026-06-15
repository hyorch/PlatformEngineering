# Backstage on Docker

## Config Backstage Container

```bash
docker run --rm -p 3000:3000 -it -v /home/jpastor/dev/jpastor/PlatformEngineering/Backstage/docker/backstage-app:/app -w /app node:24-bookworm-slim bash

# Inside the container
cd /app
npx @backstage/create-app@latest

cd my-backstage-app # the name of the crated app
yarn start
```

Edit app-config.yaml to change the host to 0.0.0.0. Install vim on the container.

```yaml
app:
  title: Scaffolded app
  baseUrl: http://localhost:3000
  listen:
    host: 0.0.0.0   
```
Test connection to the app from Windows machine
```bash
cd my-backstage-app
yarn start
```
