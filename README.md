# Beekeeper Liquibase Clickhouse

This is the parent repository for Beekeeper Liquibase Clickhouse, a liquibase extension for Clickhouse.

## Usage

### Compiling

`./mvnw package -s settings.xml`

### Installing snapshots for local development

You can install the current state into the local Maven repository with
`./mvnw install -s settings.xml`

The version will be `SNAPSHOT`

### Releasing
Make sure you bump the version in `version.properties`. The release will be done by our [jenkins-job](https://jenkins.internal.beekeeper.io/job/libs/job/quarkus-extensions/) when the PR branch is merged back to master.
Please add your and explain your change to the changelog below.

#### Local Release

`./mvnw -Drevision=${VERSION} -U clean deploy -s settings.xml`


# liquibase-clickhouse
Supported operations: update, rollback (with provided SQL script), tag


Maven dependency:

```
<dependency>
    <groupId>com.mediarithmics</groupId>
    <artifactId>liquibase-clickhouse</artifactId>
    <version>Latest version from Maven Central</version>
</dependency>
```

The cluster mode can be activated by adding the **_liquibaseClickhouse.conf_** file to the classpath (liquibase/lib/).
```
cluster {
    clusterName="{cluster}"
    tableZooKeeperPathPrefix="/clickhouse/tables/{shard}/{database}/"
    tableReplicaName="{replica}"
}
```
In this mode, liquibase will create its own tables as replicated.<br/>
All changes in these files will be replicated on the entire cluster.<br/>
Your updates should also affect the entire cluster either by using ON CLUSTER clause, or by using replicated tables.

<hr/>

###### Important changes
From the version 0.7.0 the liquibase-clickhouse supports replication on a cluster. Liquibase v4.6.1.

From the version 0.6.0 the extension adapted for the liquibase v4.3.5.

