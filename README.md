Vert Podman User Quadlet
========================

**Disclaimer:** I am not affiliated with, associated, authorized, endorsed by, or in any way officially connected with the Vert project.  Although this should function as a drop in replacement, please backup data before proceeding.

This guide demonstrates how to deploy **Vert**—a simple and private file converter—as a **User (Rootless) Quadlet** on Ubuntu 25.10.

Performance & Privacy: tmpfs
----------------------------

**Note:** This configuration mounts `/tmp` as a `tmpfs`. This means all files uploaded for conversion are stored in your system's RAM rather than the physical disk. This increases conversion speed and ensures that files are completely wiped when the container stops.

System Information
------------------

*   **Tested Environment:** Ubuntu 25.10
*   **Podman Version:** 5.4.x
*   **Type:** User-level Quadlet (Rootless)

1\. Installation & Setup
------------------------

### Step A: Prepare the Directory

`mkdir -p ~/.config/containers/systemd`

### Step B: Move and Edit

Move the `vert.container` file and update the `PUB_HOSTNAME` variable to match your network address:

`mv vert.container ~/.config/containers/systemd/`
`nano ~/.config/containers/systemd/vert.container`

### Step C: Enable Linger

`sudo loginctl enable-linger $USER`

2\. Activation
--------------

Reload the user systemd daemon and start Vert:

`systemctl --user daemon-reload`
`systemctl --user start vert`
`systemctl --user enable vert`

3\. Verification
----------------

### Check Status

`systemctl --user status vert`

### Check Logs

`journalctl --user -u vert -f`

Once running, access Vert at: `http://[Your-IP]:3123`

4\. Maintenance
---------------

Update automatically via the registry:

`podman auto-update`
