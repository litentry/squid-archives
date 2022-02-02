# Squid Archives

## Preparing the server

```sh
wget -q -O - https://raw.githubusercontent.com/litentry/squid-archives/main/init.sh | bash

# reload terminal session here to enable new docker group for the current user

cd /srv/www/squid-archives
chain={chain} ./init-letsencrypt.sh
```

## Importing from backup

Replace {chain} and {file} below
```shell script
sudo apt install pv postgresql-client-12 postgresql-client-common
sudo chown -R {user}:docker /data
mkdir /data/archive
cd /srv/www/squid-archives/
chain={chain} docker-compose up -d db
psql -h 0.0.0.0 -U postgres -c "CREATE DATABASE \"{chain}-archive\""
# run the next command from within tmux as it can take a long time
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


