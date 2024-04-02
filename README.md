# CloudQuery Container Demo

A demo project with CloudQuery, Metabase, and Postgres containers syncing Simple Analytics data with the [SimpleAnalytics](https://hub.cloudquery.io/plugins/source/simple-analytics/simple-analytics/latest/docs) source plugin.

## How to run this

The metabase container is built for ARM processors. Use `metabase/metabase` if you're on x86 architecture.

You will need Docker and docker-compose installed.

Copy `.env.example` to `.env` and insert your own API key and user ID for Simple Analytics ([see how to get them](https://docs.simpleanalytics.com/api/authenticate)).

You will also need to fill in your CloudQuery API key. [Here's how to get it](https://docs.cloudquery.io/docs/deployment/generate-api-key).

Run `docker-compose up -d` to start the containers.

Visit [localhost:3000](http://localhost:3000) and add the destination database. Use the values below, leave other fields set to default.

- Type: Postgresql
- Host: `cq_demo_postgres`
- Database name: cq
- Username: cq
- Password: password123

## Run the first sync

Open the terminal and run the shell with the `demo_cq_cron` container:

```shell
docker exec -it demo_cq_cron bash
```

From the `/app` directory, run `sync.sh`:

```shell
./sync.sh daily.yml
```

## Scheduled syncs

The sync will run daily at 9 AM in the morning. To change it, edit the `cloudquery/crontab` file and rebuild the container using `docker-compose build demo_cq_cron`.
