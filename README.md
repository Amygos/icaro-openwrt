# Openwrt port of Icaro HotSpot

Minimum HW requirements:

| RAM   | Flash |
|-------|-------|
| 32 MB |  8 MB |

Pre compiled architectures:

  * mips_24kc

List of compatible devices: https://openwrt.org/supported_devices

## Installation

1. Add Icaro repository:
```shell
	# echo "src/gz icaro  http://nethesis.github.io/icaro-openwrt_repo/mips_24kc/icaro" >> /etc/opkg/customfeeds.conf
```
2. Disable signature check commenting the line ``option check_signature 0`` in ``/etc/opkg.conf``

3. Update packages list and install `openwrt-dedalo`:
```shell
	# opkg update
	# opkg install openwrt-dedalo
```

## Network Configuration

Add  at least one network interface to hotspot bridge.

## Configuration

Available options:

- `disabled`: Enable/disable dedalo service (default true)
- `network`: network for clients connected to Dedalo eg: `192.168.69.0/24`
- `splash_page`: Wings (capitve portal) URL hosted on your Icaro installation, eg: ``http://icaro.mydomain.com/wings``
- `aaa_url`:  Wax (Radius over HTTP) URL hosted on your Icaro installation, eg: ``https://icaro.mydomain.com/wax/aaa``
- `api_url`: Sun APIs URL hosted on your Icaro installation, eg: ``https://icaro.mydomain.com/api``
- `hotspot_id`:  the id of the Hotspot already present inside Icaro
- `unit_name`: hostname of local installation, eg: ``hotelthesea.example.org``
- `unit_description`: a descriptive name of local installation, eg: ``MyHotelAtTheSea``
- `unit_uuid`:  a unique unit idenifier, usually a UUID, eg ``161fre6d-8578-4247-b4a2-c40dced94bdd``
- `secret`: a shared secret between this unit and Icaro installation, eg: ``My$uperS3cret``


Configuration example:

```
config dedalo
	option disabled '0'
	option network '192.168.69.0/24'
        option splash_page 'http://icaro.mydomain.com/wings'
        option aaa_url 'https://icaro.mydomain.com/wax/aaa'
        option api_url 'https://icaro.mydomain.com/api'
	option hotspot_id '176'
	option unit_name 'hotelthesea.example.org'
	option unit_description 'MyHotelAtTheSea'
	option unit_uuid '161fre6d-8578-4247-b4a2-c40dced94bdd'
	option secret 'My$uperS3cret'
```

## First setup

1. Change `/etc/config/dedalo` with yours configurations setting, you can generate a UUID using:
 ```shell
	# uuidgen
 ```
2. Reload dedalo:
 ```shell
	# /etc/init.d/dedalo reload
 ```
3. Register dedalo unit:
 ```shell
	# dedalo register -u <your reseller username> -p <your reseller password>
 ```
4. Restart dedalo:
 ```shell
	# dedalo restart
 ```