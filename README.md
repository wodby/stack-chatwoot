# Chatwoot stack for Wodby

Deploy [Chatwoot](https://www.chatwoot.com/) on Kubernetes with Wodby.

<!-- wodby:generated:start -->

## Stack contract

- [Chatwoot stack on Wodby](https://wodby.com/stacks/chatwoot)
- [Browse Wodby application stacks](https://wodby.com/stacks)
- [Wodby stack documentation](https://wodby.com/docs/2.0/stacks/)
- [Stack manifest reference](https://wodby.com/docs/2.0/stacks/template/)

## Service definitions

- [Chatwoot service](https://github.com/wodby/service-chatwoot)
- [PostgreSQL service](https://github.com/wodby/service-postgres)
- [Redis service](https://github.com/wodby/service-redis)
- [Ganesha NFS provisioner service](https://github.com/wodby/service-nfs-provisioner)
- [OpenSMTPD service](https://github.com/wodby/service-opensmtpd)

## What's included

| Component / service | Default configuration |
| --- | --- |
| Chatwoot<br>`chatwoot` | required; enabled by default; volumes: `storage` 20 GB; links: `db` → `postgres`, `redis` → `redis`, `storage` → `storage`, `sendmail` → `opensmtpd` |
| PostgreSQL<br>`postgres` | required; enabled by default; volumes: `data` 20 GB |
| Redis<br>`redis` | required; enabled by default; volumes: `data` 5 GB |
| Shared attachment storage<br>`storage` | required; enabled by default; volumes: `data` 25 GB |
| OpenSMTPD<br>`opensmtpd` | optional; enabled by default |

Enabled optional services are selected by default but can be excluded when an
app is created. Disabled optional services are available but not selected by
default. Required services cannot be excluded.

## Validate the stack manifest

```bash
wodby stack validate-manifest stack.yml --org <org-id>
```

<!-- wodby:generated:end -->

## First administrator

After the first deployment, open the app's main domain. Chatwoot redirects to
`/installation/onboarding`. Enter a name, company name, email, and password to
create the super admin account and the first Chatwoot account, then sign in.
Finish this right away: the page is open to anyone who can reach the address
until it is submitted.

The page does not depend on the **Account signup** setting, which stays `false`
by default, or on mail delivery. See the
[Chatwoot guide](https://wodby.com/docs/2.0/stacks/catalog/chatwoot/).

## Persistence and backups

Chatwoot's relational data is stored in PostgreSQL, queue data is persisted by
Redis, and local attachments are written to the shared `/app/storage` volume.
Back up both the PostgreSQL database and the NFS storage service to preserve a
complete installation.

For cloud object storage, attach a variable integration to Chatwoot with the
environment variables required by its selected Active Storage provider.

See the [Chatwoot self-hosting documentation](https://developers.chatwoot.com/self-hosted/)
and the [Wodby stack documentation](https://wodby.com/docs/2.0/stacks/).
