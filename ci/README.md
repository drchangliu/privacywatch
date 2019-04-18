# Pipeline Configuration

Files in this directory are configuration for Concourse CI.

## Docker Image

The `analysis-image` directory contains Dockerfile necessary to create Docker image for the task in the
pipeline to use. To build the image please run the following command.  

`$ docker build -t analysis-image analysis-image`  

## Credentials

To setup the pipeline a credential file is required. This file is a YAML file that specify values for the following
variables.

- `git-username`
- `git-private-key`

These are credentials to allow Concourse CI to push new commit to the repository.
