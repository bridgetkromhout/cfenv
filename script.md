# Cloud Foundry `master` Deployment

```sh
cf target -o pivotal -s demo # already created org and space
cf enable-feature-flag diego_docker
```

## Buildpack

```sh
cf push
open http://cfenv.bosh-lite.com/
```

## Docker

```sh
cf push --docker-image caseywest/cfenv-docker:master cfenv-docker
open http://cfenv-docker.bosh-lite.com/
```

## Teardown

```sh
cf delete cfenv
cf delete cfenv-docker
```

---

# Cloud Foundry `enterprise-features` Deployment

```sh
cf marketplace
cf create-service p-redis shared-vm cfenv-redis
```

## Buildpack

```sh
cf bind-service cfenv cfenv-redis
cf push
open http://cfenv.bosh-lite.com/
```

## Docker

```sh
cf bind-service cfenv-docker cfenv-redis
cf push --docker-image caseywest/cfenv-docker:enterprise-features cfenv-docker
open http://cfenv-docker.bosh-lite.com/
```

## Demo Scalability

```sh
cf scale -i 5 cfenv
cf app cfenv
cf logs cfenv
open http://cfenv.bosh-lite.com/
```

---

## Demo Teardown

```sh
cf unbind-service cfenv cfenv-redis
cf delete-service cfenv-redis
cf delete cfenv
cf delete cfenv-docker
git checkout master
```
