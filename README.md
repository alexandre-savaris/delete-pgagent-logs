# delete-pgagent-logs
## A pgAgent job used to delete its own log records

["pgAgent is a job scheduling agent for Postgres databases, capable of running multi-step batch or shell scripts and SQL tasks on complex schedules."](https://www.pgadmin.org/docs/pgadmin4/6.18/pgagent.html)

A task (or job) in pgAgent generates logs as a result for the execution of its steps. For each execution previously scheduled, pgAgent inserts the generated logs (one record for the job, and one record for each of its steps) into tables of its own schema. These records compose the history of job execution. Over time, the volume of these logs can impact the performance of [pgAdmin](https://www.pgadmin.org/), a PostgreSQL client to which pgAgent is fully integrated.

If the complete history of pgAgent logs is not necessary, older records can be removed from its log tables. The script in this project creates a pgAgent job who takes care of this removal. It must be executed by a user with enough permissions, connected to the database where the pgAgent schema was created.

The job removes log records older than 60 days, and is executed once a day at 5 a.m. These specifications can be customized by changing the SQL code, or by accessing the pgAgent's job administration interface (after the job is created).
