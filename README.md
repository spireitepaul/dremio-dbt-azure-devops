# dremio-dbt-azure-devops
This repo contains some examples of azure devops MS-hosted pipelines when using 1.0.6 of dremio-dbt

## azure-pipelines-docker

This executes dbt-dremio in a docker build process (Centos7, Pyton) on an MS-hosted ubuntu image

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

