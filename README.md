# Unifi Controller

## Setup

1. Create .env file with following variables:
```
ROOT_PASSWORD=<YOUR_PASSWORD>
UNIFI_DB_PASSWORD=<YOUR_PASSWORD>
```
2. Run container with `docker compose up -d`
3. The webui is available at https://ip:8443⁠, setup with the first run wizard.

## Adoption

For Unifi to adopt other devices, e.g. an Access Point, it is required to change the inform IP address. Because Unifi runs inside Docker by default it uses an IP address not accessible by other devices. To change this go to Settings > System > Advanced and set the Inform Host to a hostname or IP address accessible by your devices. Additionally the checkbox "Override" has to be checked, so that devices can connect to the controller during adoption (devices use the inform-endpoint during adoption).

Please note, Unifi change the location of this option every few releases so if it's not where it says, search for "Inform" or "Inform Host" in the settings.

In order to manually adopt a device take these steps:

```
ssh ubnt@$AP-IP
set-inform http://$address:8080/inform
```
The default device password is ubnt. $address is the IP address of the host you are running this container on and $AP-IP is the Access Point IP address.
