# packer-gce-goss

## Overview

This repository will create a GCE image and will run tests against it.

## Build Image

Execute the following to create the Packer Image:

```
packer build -var project_id="$project_id" packer.json
```

## Questions?

Open an issue.
