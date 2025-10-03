# UniFi Controller (Docker)

A Dockerized UniFi Network Controller to manage UniFi Access Points and other UniFi devices.

---

## Setup

1. Create a `.env` file with the following variables:

   ```bash
   ROOT_PASSWORD=<YOUR_PASSWORD>
   UNIFI_DB_PASSWORD=<YOUR_PASSWORD>
   ```

2. Start the container:

   ```bash
   docker compose up -d
   ```

3. Open the UniFi Controller web interface at:

   ```
   https://<HOST-IP>:8443
   ```

   and complete the **first-run wizard**.

---

## Device Adoption

UniFi devices (e.g., Access Points) need to know how to reach the controller.
Because the controller runs inside Docker, the internal container IP is **not accessible** to devices on your LAN. You must set the **Inform Host** to your Docker host’s LAN IP (or a hostname reachable by your devices).

### Configure Inform Host

1. In the UniFi web interface, go to:
   **Settings → System → Advanced → Inform Host**

2. Enter your Docker host’s LAN IP or hostname (e.g., `192.168.1.50`).
   Check the **Override Inform Host** box.

   > ⚠️ The exact location of this setting may vary between UniFi versions.
   > If you don’t see it, search for **“Inform”** or **“Inform Host”** in the settings.

---

### Manual Adoption via SSH

If a device does not appear for adoption automatically, you can manually point it to the controller:

```bash
ssh ubnt@<AP-IP>
set-inform http://<HOST-IP>:8080/inform
```

* Default device SSH password: `ubnt`
* `<AP-IP>` = the IP address of your Access Point
* `<HOST-IP>` = the LAN IP of your Docker host (the same one you used in the Inform Host setting)

Run the `set-inform` command twice: the first attempt makes the device contact the controller, the second confirms adoption.

---

## Notes

* All UniFi devices on your network (AP1, AP2, AP3, etc.) use the **same controller address** (`<HOST-IP>`).
* Ensure ports `8080` (inform) and `8443` (web UI) are accessible on your Docker host.
* After adoption, devices will remember the controller address and no longer need manual intervention.
