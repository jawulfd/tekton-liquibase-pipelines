# Tekton Pipeline

This folder contains the files to configure [liquibase-pipeline](liquibase-pipeline.yaml) and [liquibase-rollback-pipeline](liquibase-rollback-pipeline.yaml)
and sample configurations for executing PipelineRuns for previous pipelines

### Liquibase Pipeline and Pipeline Run

Inside [liquibase-pipeline.yaml](liquibase-pipeline.yaml), the flow for the liquibase pipeline can be found. This flow is
composed of different steps:

1. **Git Clone Step**:
Using the input parameters for git-url and git-revision, the repository is clone into the configured persisten volume 
so it can be reutilized in the following steps. Due to the behaviour of this step, 
a retryStrategy checking network transient errors is configured to retry the git-clone task in case of network errors

2. **Liquibase Validate Step**:
In this step, the liquibase changeset configurations are validated in order to stop the execution 
in case there is any changelog error

3. **Liquibase Status Step**:
After executing the validation of the changelog, the status of pending changesets is checked in order to continue
with the pipeline execution. If there is no changeset pending to be applied, the pipeline execution is stopped

4. **Liquibase Pre-Update Step**:
Before executing the liquibase update command, in case it is not prod environment, a snapshot of current database state
is taken in order to compare with the post-update state. Also, the liquibase update-sql command is executed in order to get
a report of the sql statements that are going to be executing in the liquibase update step

5. **Liquibase Update Step**:
During this step execution the pending changesets will be applied to the database. In non-production environments
the update-testing-rollback command will be executed to test the rollback capability after applying the changesets,
while in production environments the update command will be executed to apply and persist the pending changesets

6. **Liquibase Post-Update Step**:
In the post-update step, different commands are executed depending on the environment where the pipeline is being applied.
In non-production environments, the liquibase diff command is executed using the previous generated snapshot in order to
show the differences between the pre-update and the post-update database states. In production environments, the liquibase
tag command is executed to mark latest applied changeset with the provided git tag

The file [liquibase-pipeline-run.yaml](liquibase-pipeline-run.yaml) contains a sample PipelineRun to trigger a single execution
of liquibase pipeline

### Liquibase Rollback Pipeline and Pipeline Runs

Inside [liquibase-rollback-pipeline.yaml](liquibase-rollback-pipeline.yaml), the flow for the liquibase pipeline can be found.
This workflow is composed of different steps:

1. **Git Clone Step**:
Using the input parameters for git-url and git-revision, the repository is clone into the configured persisten volume 
so it can be reutilized in the following steps. Due to the behaviour of this step, 
a retryStrategy checking network transient errors is configured to retry the git-clone task in case of network errors

2. **Liquibase Check Tag Step**:
In this step, the liquibase tag-exists command is invoked to check if the input tag exists in the liquibase DATABASECHANGELOG Table.
In case the tag does not exist, the execution is stopped

3. **Liquibase Rollback Step**:
Depending on the value of the input parameter dry-run, a different liquibase rollback command is executed. When the parameter
dry-run is set to "yes", the rollback-sql command will be executed to get a report of the sql statements that are going to be
executed in the liquibase rollback command and database is not modified. When the parameter dry-run is set to "no", the rollback
command will be executed and all the changesets until the tag provided will be removed from database

The file [liquibase-rollback-pipeline-run-dryrun.yaml](liquibase-rollback-pipeline-run-dryrun.yaml) contains a sample PipelineRun 
to trigger a single execution of liquibase rollback pipeline with the dry-run parameter set to yes,
while the file [liquibase-rollback-pipeline-run.yaml](liquibase-rollback-pipeline-run.yaml) contains a sample PipelineRun 
to trigger a single execution of liquibase rollback pipeline with the dry-run parameter set to no
