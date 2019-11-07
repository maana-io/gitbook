# Upgrading the Platform Configuration

## Fixing currently deployed/misconfigured clusters

1. Update nginx configuration:

[https://bitbucket.corp.maana.io/projects/H4/repos/h4/browse/deployment/nginx/nginx.con](https://bitbucket.corp.maana.io/projects/H4/repos/h4/browse/deployment/nginx/nginx.conf)

2. Entire file has to be replaced. Most likely only one thing will need to be done. Replace the following:

```text
> ssl_certificate /etc/keys/cert.pem; ssl_certificate_key /etc/keys/key.pem; ssl_password_file /etc/keys/global.pass; > with
> ssl_certificate /etc/keys/wildcard.knowledge.maana.io.combined.pem; ssl_certificate_key /etc/keys/knowledge.maana.io.key; >
```

3. Restart nginx:

```text
docker service update --force infrastructure_nginx
```

4. Update saqserver and kinddb endpoint mode

```text
docker service update --force core_saqserver --endpoint-mode dnsrr
docker service update --force core_maana-kinddb --endpoint-mode dnsrr
```

## Redeploying previously deployed 3.1.4

### Cleanup

1. Remove old stack
2. docker stack ls docker stack rm azureDeploy13
3. Prune all containers, volumes and networks from all swarm nodes
4. ansible all -i scripts/d.py -m shell -a "echo y \| docker system prune -a" ansible all -i scripts/d.py -m shell -a "echo y \| docker volume prune"
5. Delete old SAQ data
6. sudo rm -rf /maana/saq/SAQ

## Update configuration

  
1. Update nginx configuration: [https://bitbucket.corp.maana.io/projects/H4/repos/h4/browse/deployment/nginx/nginx.conf](https://bitbucket.corp.maana.io/projects/H4/repos/h4/browse/deployment/nginx/nginx.conf)

2. Entire file has to be replaced. Most likely, only one thing will need to be done. Replace the following:

```text
> ssl_certificate /etc/keys/cert.pem; ssl_certificate_key /etc/keys/key.pem; ssl_password_file /etc/keys/global.pass; > with
> ssl_certificate /etc/keys/wildcard.knowledge.maana.io.combined.pem; ssl_certificate_key /etc/keys/knowledge.maana.io.key; >
```

3. Copy deployment package 'cluster' version. 

{% hint style="info" %}
After official RC1 cutover, there was a critical bugfix in deployment files.
{% endhint %}

4. Edit all environment variables: All tags for all components must be set to "v3.1.5.RC1", e.g.: \`\`\`export TAG\_SAQ=v3.1.5.RC1

```text
For any project "# Environment configuration" section must be updated

For any CS project installation, **every single value in #Auth section must be updated**

- Create network
```docker network create --attachable -d overlay --subnet=10.6.6.0/24 --gateway 10.6.6.1 maanaq
```

5. Deploy infrastructure stack

```text
```
cd cluster
source deploy.env.sh
docker stack deploy --with-registry-auth -c infrastructure.yml infrastructure
```

{% hint style="info" %}
Before proceeding to the next step, make sure that all containers in the infrastructure stack are running.
{% endhint %}

6. Docker stack ps infrastructure\|grep Running

7. At this point, logging and telemetry should be accessible, e.g. \[[https://stable.knowledge.maana.io:8443/graylog/ui](https://stable.knowledge.maana.io:8443/graylog/ui)\]

8. Deploy platform core

```text
source deploy.env.sh docker stack deploy --with-registry-auth -c core.yml core
```

9. Make sure that core is running.

```text
docker stack ps core |grep Running
```

10. Make sure that all SAQ nodes have started and registered with consul - following graylog query must return 3 messages.

```text
tag:saq AND "new session"
```

11. Deploy additional stacks.

```text
docker stack deploy --with-registry-auth -c arbots.yml arbots docker stack deploy --with-registry-auth -c azure.yml azure docker stack deploy --with-registry-auth -c samples.yml samples
```

12. Perform bootstrap - Same as before.

