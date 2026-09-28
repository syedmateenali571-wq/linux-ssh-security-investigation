# Findings
## Finding 01 — SSH Service Status

The OpenSSH service was installed on the Kali Linux system, but
the service was currently inactive and configured as disabled at boot.

Status:
- Service: OpenSSH Secure Shell server
- Current state: inactive (dead)
- Boot configuration: disabled


## Finding 02 — SSH Port 22 Status

A check was performed to determine whether TCP port 22
was listening for SSH connections.

### Command Used

sudo ss -tlnp | grep :22

### Result

No output was returned.


### Conclusion

No service was detected listening on TCP port 22 at the
time of the investigation. This is consistent with the
OpenSSH service being inactive.


## Finding 03 — SSH Authentication Activity

SSH authentication logs were reviewed using systemd journal logs.

### Authentication Activity

A failed SSH authentication attempt was recorded for the local `kali` user.

- Timestamp: Sep 28 10:29:33
- Username: kali
- Source: ::1 (localhost)
- Result: Failed password
- Protocol: SSH

Approximately 12 seconds later, a successful authentication was recorded:

- Timestamp: Sep 28 10:29:45
- Username: kali
- Source: ::1 (localhost)
- Result: Accepted password
- Protocol: SSH

The SSH session was subsequently opened successfully for the `kali` user.

### Analysis

The evidence shows one failed authentication attempt followed by a successful authentication from the same local source.

The available evidence does not indicate a brute-force attack because only one failed attempt was observed.

Additional PAM/Winbind authentication messages were also recorded during the failed authentication sequence. These messages were treated as authentication-module errors rather than confirmed malicious activity.




## Finding 04 — SSH Configuration

The effective SSH configuration was reviewed using `sshd -T`.

### Configuration

- SSH Port: 22
- IPv4 Listen Address: 0.0.0.0:22
- IPv6 Listen Address: [::]:22

### Authentication Configuration

- Password Authentication: Enabled
- Public Key Authentication: Enabled
- Root Password Authentication: Prohibited

### Analysis

The SSH server is configured to listen on port 22 on both IPv4 and IPv6 wildcard addresses.

Password-based authentication is enabled, while root password-based SSH authentication is prohibited.



## Finding 05 — SSH Authentication Controls

The effective SSH authentication controls were reviewed.

### Configuration

- Maximum authentication attempts per connection: 6
- Login grace time: 120 seconds
- Empty passwords: Not permitted

### Analysis

The SSH configuration limits authentication attempts per connection to six and does not permit empty passwords.

The login grace period is configured to 120 seconds.




## Finding 06 — SSH Logging Configuration

The SSH logging configuration was reviewed.

### Configuration

- Log Level: INFO
- Syslog Facility: AUTH

### Analysis

SSH is configured with the INFO logging level and AUTH syslog facility.

Authentication activity was available through the systemd journal and was used during the investigation.
