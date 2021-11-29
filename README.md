# DOCSIS templates for Zabbix

## What is it exactly?

It is just four templates and one script for Zabbix 5.0 that I wrote for myself and which I want to share with people.

Note: At the moment I don't have access to this equipment and I can no longer make significant changes to these templates and scripts.

## Templates

### cisco-ubr7246.xml

It's a template for CMTS CISCO uBR7246.

Items:
* Description
* Model
* Serial Number
* MAC address

Discovery rules:
* Ethernet Interfaces Discovery
    - Incoming Traffic (item)
    - Outcoming Traffic (item)
    - Incoming/Outcoming Traffic (graph)
* Downstream Cable Interfaces Discovery
    - Traffic (item)
* Upstream Cable Interfaces Discovery
    - SNR (item)
    - Low SNR (trigger)
    - Zero SNR (trigger)
    - Traffic (item)

Depends:
* Template Module ICMP Ping
* Template docsis-settings

### `motorola_cable_modem.xml`

It's a template for Motorola cable modem.

Items:
* Description
* MAC address
* Model
* Serial Number
* Uptime
* Vendor
* Upstream SNR (an external check is used)
* Upstream Power
* Downstream SNR
* Downstream Power
* Upload Traffic
* Download Traffic

Triggers:
* Low Upstream SNR
* Very low Upstream SNR
* High Upstream Power level
* Low Upstream Power level
* Low Downstream SNR
* Very low Downstream SNR
* High Downstream Power level
* Low Downstream Power level

Graphs:
* Traffic

Depends:
* Template docsis-settings

### `thomson_cable_modem.xml`

It's a template for Thomson cable modem.

Items: Same as Motorola

Triggers: Same as Motorola

Graphs: Same as Motorola

Depends: Same as Motorola

### `docsis_settings.xml`

Contains settings for the templates above. To modify the settings open template properties and look for the Macros tab.

Configurable parameters:
* `SNMP_COMMUNITY`
* `$CMTS_ADDR`
* `CMTS_UPSTREAM_SN_MIN_VALUE`
* `MODEM_DOWNSTREAM_POWER_MAX_VALUE`
* `MODEM_DOWNSTREAM_POWER_MIN_VALUE`
* `MODEM_DOWNSTREAM_SN_CRITICAL_MIN_VALUE`
* `MODEM_DOWNSTREAM_SN_MIN_VALUE`
* `MODEM_UPSTREAM_POWER_MAX_VALUE`
* `MODEM_UPSTREAM_POWER_MIN_VALUE`
* `MODEM_UPSTREAM_SN_CRITICAL_MIN_VALUE`
* `MODEM_UPSTREAM_SN_MIN_VALUE`

Each parameter has a description.

## Scripts

### `cmts_modem_param`

This script are used in the `motorola_cable_modem.xml` and `thomson_cable_modem.xml` templates.
For detaild see the comments in it and [External checks in Zabbix documentation](https://www.zabbix.com/documentation/5.0/manual/config/items/itemtypes/external).

