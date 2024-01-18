# Telegraf release for BOSH

## Deploy with BOSH runtime-config

- Update BOSH runtime config with telegraf job configuration as listed below

  ```shell
  bosh update-config --type=runtime --name=telegraf runtime-telegraf.yml
  ```

- `runtime-telegraf.yml` file example

  ```yaml
  releases:
    - name: c-telegraf
      sha1: 14c2211a58ee659a7467b8e6b991d2b7f7e20027
      url: https://github.com/Comcast/telegraf-boshrelease/releases/download/v10/c-telegraf-10.tgz
      version: "10"

  addons:
    - name: c-telegraf
      include:
        stemcell:
          - os: ubuntu-bionic
          - os: ubuntu-jammy
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
