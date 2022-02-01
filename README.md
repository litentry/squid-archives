# Squid Archives

## Preparing the server

```sh
wget -q -O - https://raw.githubusercontent.com/litentry/squid-archives/main/init.sh | bash
cd /srv/www/squid-archives
./init-letsencypt.sh
```

## Importing from backup

Replace {chain} and {file} below
```shell script
sudo apt install pv postgresql-client-12 postgresql-client-common
mkdir /data/archive
chain={chain} docker-compose up -d db
psql -h 0.0.0.0 -U postgres -c "CREATE DATABASE \"{chain}-archive\""
pv {file}.sql | psql -h 0.0.0.0 -U postgres -d {chain}-archive
```

## Running the archiver

```shell script
chain={chain} docker-compose up -d
```
Grab a coffee to celebrate! 

## Domains

You can check the status on the domain configured with nginx:

https://{chain}-squid-archive.litentry.io/ e.g. https://polkadot-squid-archive.litentry.io/


