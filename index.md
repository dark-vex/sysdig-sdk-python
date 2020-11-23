---
description: Sysdig SDK for Python
---
A Python client API for Sysdig Monitor/Sysdig Secure.

This module is a wrapper around the Sysdig Monitor/Sysdig Secure APIs. It
exposes most of the sysdig REST API functionality as an easy to use and easy to
install Python interface.

## Installation

### Automatic with PyPI

```console
$ pip install sdcclient
```

### Manual (development only)

This method requires [Poetry](https://python-poetry.org/) installed

```console
$ git clone https://github.com/sysdiglabs/sysdig-sdk-python.git
$ cd python-sdc-client
$ poetry install
```

## Usage

_Note:_ in order to use this API you must obtain a Sysdig Monitor/Secure API token.
You can get your user's token in the _Sysdig Monitor API_ section of the settings page
for [monitor](https://app.sysdigcloud.com/#/settings/user) or
[secure](https://secure.sysdig.com/#/settings/user).

The library exports two classes, `SdMonitorClient` and `SdSecureClient` that
are used to connect to Sysdig Monitor/Secure and execute actions.

They can be instantiated like this:

``` python
from sdcclient import SdMonitorClient

api_token = "MY_API_TOKEN"

#
# Instantiate the Sysdig Monitor client
#
client = SdMonitorClient(api_token)
```

For backwards compatibility purposes, a third class `SdcClient` is exported which is an alias of `SdMonitorClient`.

Once instantiated, all the methods documented below can be called on the object.

### Return Values
Every method in the SdMonitorClient/SdSecureClient classes returns **a list with two entries**. The first one is a boolean value indicating if the call was successful. The second entry depends on the result:
- If the call was successful, it's a dictionary reflecting the json returned by the underlying REST call
- If the call failed, it's a string describing the error

For an example on how to parse this output, take a look at a simple example like [get_data_simple.py](examples/get_data_simple.py)


## On-Premises Installs

For [On-Premises Sysdig Monitor installs](https://support.sysdigcloud.com/hc/en-us/articles/206519903-On-Premises-Installation-Guide),
additional configuration is necessary to point to your API server rather than
the default SaaS-based one, and also to easily connect when using a self-signed
certificate for SSL. One way to handle this is by setting environment variables
before running your Python scripts:

```console
export SDC_URL='https://<YOUR-API-SERVER-HOSTNAME-OR-IP>'
export SDC_SSL_VERIFY='false'
```

Alternatively, you can specify the additional arguments in your Python scripts
as you instantiate the SDC client:

```
client = SdMonitorClient(api_token, sdc_url='https://<YOUR-API-SERVER-HOSTNAME-OR-IP>', ssl_verify=False)
```
