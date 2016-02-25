# snap-plugin-collector-keystone

snap plugin for collecting metrics from OpenStack Keystone module. 

1. [Getting Started](#getting-started)
  * [System Requirements](#system-requirements)
  * [Installation](#installation)
2. [Documentation](#documentation)
  * [Collected Metrics](#collected-metrics)
  * [Examples](#examples)
  * [Roadmap](#roadmap)
3. [Community Support](#community-support)
4. [Contributing](#contributing)
5. [License](#license)
6. [Acknowledgements](#acknowledgements)

## Getting Started

Plugin collects metrics by communicating with OpenStack by REST API.
It can be used in- as well as out-of-bands. 

### System Requirements

 - Linux
 - OpenStack deployment available

### Installation
#### Download keystone plugin binary:
You can get the pre-built binaries for your OS and architecture at snap's [Github Releases](https://github.com/intelsdi-x/snap/releases) page.

#### To build the plugin binary:
Fork https://github.com/intelsdi-x/snap-plugin-collector-keystone
Clone repo into `$GOPATH/src/github/intelsdi-x/`:
```
$ git clone https://github.com/<yourGithubID>/snap-plugin-collector-keystone
```
Build the plugin by running make in repo:
```
$ make
```
This builds the plugin in `/build/rootfs`

## Documentation

### Collected Metrics
This plugin has the ability to gather the following metrics:

Namespace | Data Type | Description (optional)
----------|-----------|-----------------------
intel/openstack/keystone/\<tenant_name\>/users_count | int | Total number of users for given tenant
intel/openstack/keystone/total_tenants_count | int | Total number of tenants
intel/openstack/keystone/total_users_count | int | Total number of users 
intel/openstack/keystone/total_endpoints_count | int | Total number of endpoints
intel/openstack/keystone/total_services_count | int | Total number of services

### snap's Global Config
Global configuration files are described in snap's documentation. You have to add section "keystone" in "collector" section and then specify following options:
- `"admin_endpoint"` - URL for OpenStack Identity admin endpoint (ex. `"http://keystone.public.org:35357"`)
- `"admin_user"` -  administrator user name
- `"admin_password"` - administrator password
- `"admin_tenant"` - administration tenant

### Examples
It is not suggested to set interval below 20 seconds. This may lead to overloading Keystone with authentication requests. 

Example task manifest to use keystone plugin:
```
{
    "version": 1,
    "schedule": {
        "type": "simple",
        "interval": "60s"
    },
    "workflow": {
        "collect": {
            "metrics": {
		        "/intel/openstack/keystone/total_tenants_count": {},
		        "/intel/openstack/keystone/total_users_count": {},
		        "/intel/openstack/keystone/total_endpoints_count": {},
		        "/intel/openstack/keystone/admin/users_count": {}
           },
            "config": {
            },
            "process": null,
            "publish": null
        }
    }
}
```


### Roadmap
There isn't a current roadmap for this plugin, but it is in active development. As we launch this plugin, we do not have any outstanding requirements for the next release.

## Community Support
This repository is one of **many** plugins in **snap**, a powerful telemetry framework. See the full project at http://github.com/intelsdi-x/snap To reach out to other users, head to the [main framework](https://github.com/intelsdi-x/snap#community-support)

## Contributing
We love contributions!

There's more than one way to give back, from examples to blogs to code updates. See our recommended process in [CONTRIBUTING.md](CONTRIBUTING.md).

## License
[snap](http://github.com/intelsdi-x/snap), along with this plugin, is an Open Source software released under the Apache 2.0 [License](LICENSE).

## Acknowledgements

* Author: [Marcin Krolik](https://github.com/marcin-krolik)

And **thank you!** Your contribution, through code and participation, is incredibly important to us.