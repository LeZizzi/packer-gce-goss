# packer-gce-goss

## Overview

This repository will create a GCE image and will run tests against it.

## Build Image

Execute the following to create the Packer Image:

```
packer build -var project_id="$project_id" packer.json
```

## Cloud Build Builder

Before using this builder , it must be built and pushed to the registry in your 
project. Run the following command:

```
cd cloudbuild/
gcloud builds submit .
```

## Questions?

Open an issue.
