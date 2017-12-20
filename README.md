# Telegraf release for BOSH

## Deploy with BOSH add-on

Instructions below are for bosh v2 client.

* Upload release to BOSH director

        bosh upload-release https://github.com/Comcast/telegraf-boshrelease/releases/download/v5/c-telegraf-5.tgz

* Update BOSH runtime config with telegraf job configuration as listed below

        # review existing runtime config
        bosh runtime-config
        # merge with content listed below and save in file runtime-config.yml
        # upload runtime config
        bosh update-runtime-config runtime-config.yml

## Example of `runtime-config.yml` file

    releases:
    - name: c-telegraf
      version: 5
    addons:
    - name: c-telegraf
      jobs:
      - name: telegraf-system
        release: c-telegraf
      properties:
        telegraf:
          tags:
            region: us-east-1
          influxdb:
            url: http://influxdb.example.com:8086
            database: system
            retention_policy: default
