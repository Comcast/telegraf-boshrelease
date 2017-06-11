# Telegraf release for BOSH

## Deploy using BOSH add on

* Download release tarball from https://github.com/Comcast/telegraf-boshrelease/releases
* Upload release to BOSH director

        bosh upload release c-telegraf-4.tgz

* Update BOSH runtime config with telegraf job configuration as listed below

        # review existing runtime config
        bosh runtime-config
        # merge with content listed below and save in file runtime-config.yml
        # upload runtime config
        bosh upload runtime-config runtime-config.yml

## Example of `runtime-config.yml` file

    releases:
    - name: c-telegraf
      version: 4
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
