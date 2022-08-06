# dremio-dbt-azure-devops
This repo contains an example of azure devops MS-hosted pipelines when using 1.0.6 of dremio-dbt.

## azure-pipelines-docker

This executes dbt-dremio in a docker build process (Centos7, Python) on an MS-hosted Ubuntu image.

Originally I leveraged similar code outside of a  Docker build process, but MS updated the Ubuntu image and subsequently broke ODBC comms.

## Assumption:

You have a DEV, UAT and PROD environment

## Pipeline prerequisites:
The following variables should be defined in the pipeline (assuming the three environments)

DEV_DREMIO_HOST
DEV_DREMIO_USER
DEV_DREMIO_PWD

UAT_DREMIO_HOST
UAT_DREMIO_USER
UAT_DREMIO_PWD

PROD_DREMIO_HOST
PROD_DREMIO_USER
PROD_DREMIO_PWD

# Things to note

I pass in the AZDO Branch to the dbt process as target.environment.  Note the Dockerfile arguments passing this in.  This can then be referenced via Jinja in a model, if for example you have datasources named in Dremio like data-dev, data-uat, data-prod for example.

I also enable --network host.  In my original build , I needed to leverage an SSH tunnel, which was set up in the azure-pipelines-docker.yaml
Sharing the network allowed me to port-forward 31010
