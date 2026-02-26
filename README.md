# RHADS-tsf Conforma Data

This is the Conforma rule data used by the Conforma policy configurations for the RHADS-tsf
project.

The [data](/data) directory contains the rule data. See the [examples](/examples) directory for
more details on how to use this repository in your policy configurations.

### Useful Commands

Listing the Task bundle references from a PipelineRun resource:

```bash
yq '.spec.pipelineSpec.tasks[].taskRef.params[] | select(.name == "bundle") | .value' | sort -u
```

Track a Task bundle in the list of trusted Tasks:

```bash
ec track tekton-task --output data/trusted-tasks.yaml
```

Combining the two commands to track multiple Task bundles:

```bash
cat pipelinerun.yaml | \
  yq '.spec.pipelineSpec.tasks[].taskRef.params[] | select(.name == "bundle") | "--bundle=" + .value' | \
  sort -u | \
  xargs ec track tekton-task --output data/trusted-tasks.yaml
```

