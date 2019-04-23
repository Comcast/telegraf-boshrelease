# Telegraf release for BOSH

## Deploy with BOSH runtime-config

Update BOSH runtime config with telegraf job configuration as listed below

```shell
# review existing runtime config
bosh runtime-config
# merge with content listed below and save in file runtime-config.yml
# upload updated runtime config
bosh update-runtime-config runtime-config.yml
```

## `runtime-config.yml` file example

```yaml
releases:
- name: c-telegraf
  sha1: c714124b04e1c1a718be96d935f87a6faaaf8fb2
  url: https://github.com/Comcast/telegraf-boshrelease/releases/download/v9/c-telegraf-9.tgz
  version: 9

addons:
- name: c-telegraf
  include:
    stemcell:
    - os: ubuntu-trusty
    - os: ubuntu-xenial
  jobs:
  - name: telegraf-system
    release: c-telegraf
    properties:
      telegraf:
        influxdb:
          url: http://influxdb.example.com:8086
          database: system
          retention_policy: default
        tags:
          region: us-east-1
```
