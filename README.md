# prisma-cloud-cwp-bulk-deletion

## Description

Script for bulk deletion of inactive and orphan accounts in Prisma Cloud CWP (Runtime Security)


## Installation

Create a python virtual environment, activate the environment and install the required packages

```
python3 -m venv env
source env/bin/activate
pip install -r requirements.txt
```
## Prerequisite

Create an Access Key on Prisma Cloud, you can refer to the [online documentation](https://docs.prismacloud.io/en/enterprise-edition/content-collections/administration/create-access-keys)

## Configuration

Create or update credentials and the Prisma Cloud stack configuration file`.prismacloud/credentials.json`  Below is the syntax of the file:

```
{
    "identity": "<PC_ACCESS_KEY>",
    "secret": "<PC_SECRET_KEY>",
    "app_stack": "<PC_API, exemple: api0>", 
    "ca_cert": ""
}
```

`ca_cert` is needed to eliminate some warning messages while using global protect or other VPN services.  To create the ca_cert file you can user the following script: https://github.com/PaloAltoNetworks/prismacloud-api-python/blob/main/scripts/pcs_ssl_configure.py

`app_stack` should match the stack you are connecting to `app,app0,app2,app3,app4,app.eu,app2.eu,app.fr, etc...`

`identity` is the Prisma Cloud access key

`secret` is the Prisma Cloud secret key

## Executing Script

Go to bulk folder and run script 

```
cd bulk
python3 cwp-bulk-purge.py -x credentials.json -c
```

 * `-h` for help

 * `-x` to specify the name of the authentication file in the `~/.prismacloud` directory. For example `-x credentials.json`. The path is hard-coded so just specify the file name.

 * `-c` most of the scripts will build a local cache file and this option will trigger that action. On subsequent calls of the script the `-c` options may not be needed, as the data you are acting on is stored locally. 

 * `-f` will identify the cache file.  Most scripts have a default file, but this option will give you the flexibility to change the file name. 

   

### Credits

Based on the work of Stephen Gordon
