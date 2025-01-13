# NAIRR Metrics Data Interchange format

Metrics reporting for NAIRR allocated HPC resources requires three datasets:

1. Resource manager logs
1. Username mappings
1. Project name mappings

## Resource manager logs

Resource manager log files should be reported in the same format as supported
by [Open XDMoD](https://open.xdmod.org/). Log files should be gnerated once
per day. It is not necessary to filter out the NAIRR jobs - the Metrics team
will do this and only load NAIRR job data into XDMoD.

## Username mappings

The Metrics team requires the mapping between the identifier for a person and their system username
on a NAIRR allocated resource, where system username is the username that appears in
the resource manager logs. For example, for the Slurm resource manager, this will be the `User`
field from the `sacct` command.

Mapping information must be UTF-8 encoded in JSON format. All timestamps must be in UTC. We support both JSON 
and JSON lines formats.

[Example username mapping \(JSON format\)](examples/person_map.json)

[Example username mapping \(JSON Lines format\)](examples/person_map.jsonl)

## Project name mappings

The Metrics team requires the mapping between the identifier for a NAIRR project and the corresponding
identifier in the resource manager logs. For example, if a compute resource is using
Slurm accounts to manage access, then the Metrics team needs the mapping
between the NAIRR project `NAIRRxxxxxx` and the `Account` field from the `sacct` command.

Mapping information must be UTF-8 encoded in JSON format. All timestamps must be in UTC. We support both JSON 
and JSON lines formats.

[Example project mapping \(JSON format\)](examples/project_map.json)

[Example project mapping \(JSON Lines format\)](examples/project_map.jsonl)

# Sending data to the Metrics team

Data should be sent to the Metrics team via HTTPS POST request to the relevant endpoint following the 
instructions on the [ACCESS Roadmap](https://readthedocs.access-ci.org/projects/integration-roadmaps/en/latest/tasks/NonACCESSUtilizationReporting_v1.html):

|  Data  | Endpoint | Update frequency |
| ------ | -------- | ---------------- |
| Resource manager logs | `https://data.ccr.xdmod.org/resource-manager-logs` | Daily |
| Username mappings     | `https://data.ccr.xdmod.org/username-maps` | When new users are added. OK to resend complete list. |
| Project mappings      | `https://data.ccr.xdmod.org/project-maps` | When new projects are added. OK to resend complete list. |
