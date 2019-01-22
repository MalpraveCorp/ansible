
# Mongo Cluster Sync Across Environements

This set of playbooks is used to rebuild the Mongo ACC cluster with the latest dump from PROD. This can be used to launch a new environment or to run nightly to keep non-prod databases up to date with production.

The playbooks are split to facilitate comprehension and avoid hitting a 1h limit that has been set for each playbook execution (global limit, unrelated to this).

 - get_mongo_nodes.yml: Connects to mongo clusters to determine master/slave for each environement.
    - Assumes first slave is running backups which will be used as donor host.
 - mongo_migration.yml: Send latest dump from PRD slave to ACC master.
    - Test connection between clusters
    - Enable SSH connection from donor slave (runs backups) to recipient master.
    - Run rsync job to transfer data
- restore_mongo.yml: Restores the dump in ACC master and then performs binary restore in the remaining slaves.
    - Test connection between recipent cluster nodes.
    - Enable SSH connection from master to slave nodes.
    - Run mongorestore on master node.
    - Stop mongo and perform binary restore to remaining nodes.

Depending on the amount of data all this _may_ take awhile.

Recommend you run this from `Rundeck` or `screen`.

## Usage

```
ansible-playbook -e "from_cluster=mal_mongo_p to_cluster=mal_mongo_a"

ansible-playbook -e "to_cluster=mal_mongo_a restore_database=my_database_name"

```

## Notice

This was developed under Ansible 2.1 and Mongo v3.6.

Some of the changes (e.g. SSH login changes) are rolled back by an independent process, they're only enabled on-demand.

Use at your own peril.
