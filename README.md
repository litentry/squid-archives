# Squid Archives

## Configuring a server for an archive

### Requirements

- git
- docker engine https://docs.docker.com/engine/install/ubuntu/

### Process

```sh
cd /srv
mkdir www
chown -R {username}:docker www
cd www
git clone https://github.com/litentry/squid-archives.git
cd squid-archives/{chain}
./init-letsencrypt.sh
docker-compose up -d
```

### Domains

You can check the status on the domain configured with nginx:

https://{chain}-squid-archive.litentry.io/ e.g. https://polkadot-squid-archive.litentry.io/
