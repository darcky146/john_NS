# tap-netsuite
Tap for extracting data from the NetSuite.

## Installation

All required libraries specified in setup.py and will setup with tap automatically. Important mention: it is required to use netsuitesdk 2.7.4 version for this tap.

### Install Netsuite Tap

```bash
$ python3 -m venv ~/.venvs/tap-netsuite
$ source ~/.venvs/tap-netsuite/bin/activate
$ pip3 install tap-netsuite
$ deactivate
```

## Configuration

After tap installation it is required to specify corresponding fields, which are used in Token Based Authentification:

NS_ACCOUNT,
NS_CONSUMER_KEY,
NS_CONSUMER_SECRET,
NS_TOKEN_KEY,
NS_TOKEN_SECRET

This fields can be specified in config.json file for standalone tap usage or in the meltano.yml file when using it with meltano.

```json
{
  "ns_account":"foo",
  "ns_consumer_key":"key_ck",
  "ns_consumer_secret":"key_cks",
  "ns_token_key":"key_t",
  "ns_token_secret" :"key_ts",
  "select_fields_by_default": true,
  "is_sandbox": false,
  "start_date": "2019-09-02T00:00:00Z"
}
```

## NetSuite Account (ns_account)

Your account Id. This can be found under Setup -> Company -> Company Information. Look for Account Id. Note “_SB” is for Sandbox account.

## NetSuite Consumer Key (ns_consumer_key)

Your consumer key for token based authentication consumer key for SOAP connection. Visit the https://support.cazoomi.com/hc/en-us/articles/360010093392-How-to-Setup-NetSuite-Token-Based-Authentication-as-Authentication-Type for details.

## NetSuite Consumer Secret (ns_consumer_secret)

Your consumer secret for token based authentication consumer key for SOAP connection. Visit the https://support.cazoomi.com/hc/en-us/articles/360010093392-How-to-Setup-NetSuite-Token-Based-Authentication-as-Authentication-Type for details.

## NetSuite Token Key (ns_token_key)

Your token key for token based authentication consumer key for SOAP connection. Visit the https://support.cazoomi.com/hc/en-us/articles/360010093392-How-to-Setup-NetSuite-Token-Based-Authentication-as-Authentication-Type for details.

## NetSuite Token Secret (ns_token_secret)

Your token secret for token based authentication consumer key for SOAP connection. Visit the https://support.cazoomi.com/hc/en-us/articles/360010093392-How-to-Setup-NetSuite-Token-Based-Authentication-as-Authentication-Type for details.

## Select Fields By Default (select_fields_by_default)

When new fields are discovered in NetSuite objects, the select_fields_by_default key describes whether or not the tap will select those fields by default.

## Is Sandbox (is_sandbox)

The is_sandbox should always be set to “true” if you are connecting Production account of NetSuite. Set it to false if you want to connect to SandBox acccount.

## Start Date (start_date)

Determines how much historical data will be extracted. Please be aware that the larger the time period and amount of data, the longer the initial extraction can be expected to take.

## Capabilities

properties,
discover,
state


## Discovery

```bash
$ ~/.venvs/tap-netsuite/bin/tap-netsuite --config=config/netsuite.config.json --discover
```

The tap will generate a [Catalog](https://github.com/singer-io/getting-started/blob/master/docs/DISCOVERY_MODE.md#the-catalog) to stdout. To pass the Catalog to a file instead, simply redirect it to a file:

```bash
$ ~/.venvs/tap-netsuite/bin/tap-netsuite --config=config/netsuite.config.json --discover > catalog.json
```

Discovery mode will not select all streams for replication by default. To instruct Discovery mode to select all streams for replication, use the `--select-all` flag:

```bash
$ ~/.venvs/tap-netsuite/bin/tap-netsuite --config=config/netsuite.config.json --discover --select-all > catalog.json
```
