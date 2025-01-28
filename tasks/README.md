# Tekton Tasks

This folder contains the tekton tasks which are referenced in [liquibase-pipeline](../pipelines/liquibase-pipeline.yaml)
and in [liquibase-rollback-pipeline](../pipelines/liquibase-rollback-pipeline.yaml)

### Liquibase diff

[liquibase-diff.yaml](liquibase-diff.yaml) file contains the implementation of liquibase diff command

The diff command is typically used at the completion of a project to verify all expected changes are in the changelog or 
to detect drift between a model schema and a database's actual schema

Reference [Liquibase diff command](https://docs.liquibase.com/commands/inspection/diff.html)

### Liquibase rollback

[liquibase-rollback.yaml](liquibase-rollback.yaml) file contains the implementation of liquibase rollback command

The rollback command is typically used to revert all changes that were made to the database after the tag you specify

Reference [Liquibase rollback command](https://docs.liquibase.com/commands/rollback/rollback.html)

### Liquibase rollback-sql

[liquibase-rollback-sql.yaml](liquibase-rollback-sql.yaml) file contains the implementation of liquibase rollback-sql command

The rollback-sql command is typically used to inspect the SQL Liquibase uses to revert changes associated with a tag you specify when you run the rollback command. 
It is best practice to use the rollback-sql command before running the rollback command to ensure that you eliminate any potential risks.

Reference [Liquibase rollback-sql command](https://docs.liquibase.com/commands/rollback/rollback-sql.html)

### Liquibase snapshot

[liquibase-snapshot.yaml](liquibase-snapshot.yaml) file contains the implementation of liquibase snapshot command

The snapshot command is typically used when you want to see changes in your target database or keep a record of your current database state.
You can use the output of snapshot with the diff and diff-changelog commands.

Reference [Liquibase snapshot command](https://docs.liquibase.com/commands/inspection/snapshot.html)

### Liquibase status

[liquibase-status.yaml](liquibase-status.yaml) file contains the implementation of liquibase status command

The status command states the number of undeployed changesets. Running status lists all undeployed changesets. 
It also lists the id, author, and file path name for each undeployed changeset. The status command does not modify the database.

Reference [Liquibase status command](https://docs.liquibase.com/commands/change-tracking/status.html)

### Liquibase tag

[liquibase-tag.yaml](liquibase-tag.yaml) file contains the implementation of liquibase tag command

The tag command is typically used to mark the current database state, version, release, or any other information 
by adding the tag to the last row in the DATABASECHANGELOG table

Reference [Liquibase tag command](https://docs.liquibase.com/commands/utility/tag.html)

### Liquibase tag-exists

[liquibase-tag-exists.yaml](liquibase-tag-exists.yaml) file contains the implementation of liquibase tag-exists command

The tag-exists command is typically used to identify whether the specified tag exists in the database or specifically in the DATABASECHANGELOG table

Reference [Liquibase tag-exists command](https://docs.liquibase.com/commands/utility/tag-exists.html)

### Liquibase update

[liquibase-update.yaml](liquibase-update.yaml) file contains the implementation of liquibase update command

The update command deploys any changes that are in the changelog file and that have not been deployed to your database yet.

Reference [Liquibase update-testing-rollback command](https://docs.liquibase.com/commands/update/update.html)

### Liquibase update-testing-rollback

[liquibase-update-testing-rollback.yaml](liquibase-update-testing-rollback.yaml) file contains the implementation of liquibase update-testing-rollback command

update-testing-rollback tests rollback support by deploying all pending changesets to the database, executes a rollback sequentially 
for the equal number of changesets that were deployed, and then runs the update again deploying all changesets to the database.

Reference [Liquibase update-testing-rollback command](https://docs.liquibase.com/commands/update/update-testing-rollback.html)

### Liquibase update-sql

[liquibase-updatesql.yaml](liquibase-updatesql.yaml) file contains the implementation of liquibase update-sql command

The update-sql command outputs the expected SQL of an update operation so that you can evaluate it. 
The command does not automatically check SQL for correctness and does not anticipate database deployment errors resulting from malformed SQL

Reference [Liquibase update-sql command](https://docs.liquibase.com/commands/update/update-sql.html)

### Liquibase validate

[liquibase-validate.yaml](liquibase-validate.yaml) file contains the implementation of liquibase validate command

The validate command checks your changelog and identifies any possible errors with Liquibase syntax 
that may cause the update command to fail

The validate command only looks for possible errors in the changelog. It does not check for possible errors 
that might result from applying the changes to a specific database.

Reference [Liquibase validate command](https://docs.liquibase.com/commands/utility/validate.html)
