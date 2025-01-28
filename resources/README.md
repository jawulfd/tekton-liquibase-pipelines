# Resources

This folder contains the resources, like service accounts, secrets configurations,...
which are required for a proper execution of tekton pipelines and events

### Tekton Events Service account

The [tekton-sa.yaml](tekton-sa.yaml) file contains the service account required to trigger pipelines
from event listeners

This service account require the roles **tekton-triggers-eventlistener-roles** and 
**tekton-triggers-eventlistener-clusterroles**

### JDBC Database Secret Configuration

The [jdbc-database-secret.yaml](jdbc-database-secret.yaml) file contains a sample yaml file to configure 
the kubernetes secret to be able to execute the tekton pipelines and connect to the target database

- [jdbc-postgresql-secret.yaml](jdbc-postgresql-secret.yaml) is a sample file for postgresql database
- [jdbc-mysql-secret.yaml](jdbc-mysql-secret.yaml) is a sample file for mysql database
