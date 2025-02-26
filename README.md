# sslh
`sslh` is a tool in Kali Linux used for multiplexing SSL and non-SSL traffic on the same port. It allows you to run multiple services (such as HTTPS and SSH) on the same port by differentiating between the two based on the protocol. This is particularly useful for environments with strict firewall rules.

### Installation

To install `sslh` on Kali Linux, you can use the following command:

```bash
sudo apt-get install sslh
```

### Basic Usage

The basic syntax for using `sslh` is:

```bash
sslh -f <config_file>
```

Here, `<config_file>` contains the configuration settings for `sslh`.

### Configuration File Example

A simple configuration file (`/etc/sslh/sslh.cfg`) might look like this:

```
daemon: true
debug: 2
foreground: false

protocols:
  https:
    listener: 0.0.0.0:443
    backend: 127.0.0.1:8443
  ssh:
    listener: 0.0.0.0:443
    backend: 127.0.0.1:2222
```

In this example:
- Both HTTPS and SSH traffic are directed to port 443.
- HTTPS traffic is forwarded to port 8443, and SSH traffic is forwarded to port 2222.

### Starting `sslh`

To start `sslh` with the configuration file, use:

```bash
sudo sslh -f /etc/sslh/sslh.cfg
```

### Example Output

When `sslh` is running, it may display logs similar to the following:

```
[INFO] sslh v1.18 (https://github.com/yrashk/sslh)
[INFO] Listening on 0.0.0.0:443
[INFO] Detected protocol: SSL
[INFO] Connecting to backend 127.0.0.1:8443 for HTTPS
```

Or for SSH traffic:

```
[INFO] Detected protocol: SSH
[INFO] Connecting to backend 127.0.0.1:2222 for SSH
```

### Conclusion

`sslh` is a powerful tool for managing multiple protocols over a single port, enhancing flexibility in network service configurations. Always ensure you have proper configurations to avoid conflicts between services.




                                  ALTERNATIVE
`sslh` is a Kali Linux tool that allows multiplexing of multiple protocols over the same port. It is particularly useful for bypassing firewall restrictions by forwarding connections to the appropriate service based on the initial protocol handshake.

### How to Use `sslh`

1. **Installation**:
   `sslh` is often pre-installed in Kali Linux. If not, you can install it using:
   ```
   sudo apt-get install sslh
   ```

2. **Basic Command Structure**:
   The basic syntax for using `sslh` is:
   ```
   sslh [options] [protocol:]address[:port] [...]
   ```
   Here, `options` are used to configure `sslh`, and the `protocol:address:port` arguments specify the services to which `sslh` will forward the connections.

### Common Options

- `-F <config_file>`: Specify a configuration file instead of using the command-line arguments.
- `-v`: Increase verbosity (can be used multiple times for more verbose output).
- `-d`: Run in daemon mode.
- `-P <pidfile>`: Specify a PID file for the daemon.
- `-t <timeout>`: Set the timeout for protocol detection (default is 2 seconds).

### Example Usage

1. **Forwarding HTTP, HTTPS, and SSH Traffic**:
   ```
   sslh -v --http 192.168.1.100:80 --ssl 192.168.1.100:443 --ssh 192.168.1.100:22
   ```
   This command will listen on all interfaces and forward:
   - HTTP traffic to `192.168.1.100:80`
   - HTTPS traffic to `192.168.1.100:443`
   - SSH traffic to `192.168.1.100:22`

   **Expected Output**:
   ```
   sslh version 1.21 started
   Listening on 0.0.0.0:80 (http)
   Listening on 0.0.0.0:443 (ssl)
   Listening on 0.0.0.0:22 (ssh)
   ```

2. **Using a Configuration File**:
   Create a configuration file (e.g., `sslh.conf`) with the following content:
   ```
   pptp 192.168.1.100:1723;
   openvpn 192.168.1.100:1194;
   http 192.168.1.100:80;
   https 192.168.1.100:443;
   ```
   Then, run `sslh` with the configuration file:
   ```
   sslh -F sslh.conf
   ```
   This will listen for PPTP, OpenVPN, HTTP, and HTTPS traffic and forward them to the specified addresses.

3. **Daemon Mode**:
   To run `sslh` as a daemon:
   ```
   sslh -d --http 192.168.1.100:80 --ssl 192.168.1.100:443 --ssh 192.168.1.100:22
   ```
   This will start `sslh` in the background as a daemon, listening for the specified protocols and forwarding them accordingly.

### Conclusion

`sslh` is a versatile tool that allows you to multiplex various protocols over a single port, making it useful for bypassing firewall restrictions and simplifying network configurations. By using the appropriate options and configuration, you can effectively forward different types of traffic to their respective services.




                                      ALTERNATIVE
SSLH is a Kali Linux tool that allows you to multiplex SSH, SSL/TLS, and HTTP protocols over a single port. This can be useful for penetration testers and security professionals who need to access multiple services behind a single port.

Here's how to use SSLH:

**Basic Syntax:**
```
sslh [options] <proto> <listen_addr> <listen_port> <target_addr> <target_port>
```
**Options:**

* `-v` : Verbose mode
* `-d` : Daemon mode
* `-f` : Configuration file
* `-l` : Listen address
* `-p` : Listen port
* `-t` : Target address
* `-T` : Target port

**Examples:**

1. **Simple SSH over SSL/TLS:**
```
sslh ssh 0.0.0.0 443 localhost 22
```
This will allow you to access an SSH server on port 22 using SSL/TLS on port 443.

2. **Multiplexing SSH and HTTP:**
```
sslh ssh,http 0.0.0.0 443 localhost 22,localhost 80
```
This will allow you to access an SSH server on port 22 and an HTTP server on port 80 using SSL/TLS on port 443.

**Output:**

The output of SSLH will depend on the protocol being accessed. For example, if you access an SSH server using SSLH, you will see the standard SSH login prompt.

Here's an example of the output when accessing an HTTP server using SSLH:
```
$ curl https://localhost:443
<html>
  <head>
    <title>Example Domain</title>
  </head>
  <body>
    <h1>Example Domain</h1>
    <p>This is an example web page.</p>
  </body>
</html>
```
Note that the output will vary depending on the server and protocol being accessed.

I hope this helps! Let me know if you have any further questions.




                                        ALTERNATIVE
`sslh` is a tool in Kali Linux used to multiplex multiple SSL and non-SSL protocols on a single port. It allows you to serve multiple services (like HTTPS and SSH) on the same port, providing a way to manage traffic efficiently.

### Installation

If `sslh` is not installed on your Kali Linux system, you can install it using:

```bash
sudo apt-get install sslh
```

### Basic Usage

The basic syntax for running `sslh` is:

```bash
sslh -p <port> -l <listen_address> -s <service1>:<port1> -s <service2>:<port2>
```

### Common Options

- `-p <port>`: Specify the port to listen on (default is 443).
- `-l <listen_address>`: Specify the address to listen on (default is all interfaces).
- `-s <service>:<port>`: Specify a service and its corresponding port. You can specify multiple services.

### Example Usage

1. **Basic SSL and SSH Multiplexing**:
   To serve HTTPS (port 443) and SSH (port 22) on the same port, you can run:

   ```bash
   sudo sslh -p 443 -l 0.0.0.0 -s https:443 -s ssh:22
   ```

   **Expected Output**:
   ```
   [INFO] Listening on 0.0.0.0:443
   [INFO] Protocol "https" on port 443
   [INFO] Protocol "ssh" on port 22
   ```

2. **Using a Configuration File**:
   You can also configure `sslh` using a configuration file for more complex setups. Create a file (e.g., `/etc/sslh/sslh.conf`) with the following content:

   ```ini
   foreground: true
   listen:
     - { address: "0.0.0.0:443", protocols: ["https", "ssh"] }
   service:
     - { name: "https", port: 443 }
     - { name: "ssh", port: 22 }
   ```

   Then start `sslh` with:

   ```bash
   sudo sslh -f /etc/sslh/sslh.conf
   ```

   **Expected Output**:
   ```
   [INFO] Configuration loaded from /etc/sslh/sslh.conf
   [INFO] Listening on 0.0.0.0:443
   ```

3. **Verbose Output**:
   To enable verbose logging for debugging, use the `-v` option:

   ```bash
   sudo sslh -p 443 -l 0.0.0.0 -s https:443 -s ssh:22 -v
   ```

   **Expected Output**:
   ```
   [DEBUG] Verbose logging enabled
   [INFO] Listening on 0.0.0.0:443
   ```

### Conclusion

`sslh` is a versatile tool for multiplexing traffic, allowing you to manage various services seamlessly on a single port. This can simplify firewall configurations and enhance security by reducing the number of open ports. Always ensure you configure it according to your network policies and security practices.




                                  ALTERNATIVE
`sslh` is a tool used in Kali Linux to multiplex protocols on a single port, most commonly HTTPS and SSH. It listens on a specified port and determines which protocol is being used by analyzing the first data packet. It then forwards the connection to the appropriate backend service. This is useful when you want to run multiple services (like SSH and HTTPS) on the standard HTTPS port (443) to bypass firewalls or other network restrictions.

### How to Use `sslh`

1.  **Installation**:

    `sslh` may not be pre-installed on Kali Linux. If it is not, you can install it using:

    ```bash
    sudo apt-get install sslh
    ```
2.  **Basic Configuration**:

    `sslh` is typically configured via a configuration file. The default configuration file is usually located at `/etc/default/sslh`. You need to edit this file to specify which protocols to listen for and where to forward them.

    ```bash
    sudo nano /etc/default/sslh
    ```

    Here's a basic example configuration:

    ```
    RUN=yes
    DAEMON_OPTS="--user sslh --listen 0.0.0.0:443 --ssh 127.0.0.1:22 --ssl 127.0.0.1:444 --pidfile /var/run/sslh.pid"
    ```

    *   `RUN=yes`: Enables `sslh`.
    *   `DAEMON_OPTS`: Specifies the options for the `sslh` daemon:
        *   `--user sslh`: Runs `sslh` as the `sslh` user.
        *   `--listen 0.0.0.0:443`: Listens on all interfaces on port 443.
        *   `--ssh 127.0.0.1:22`: Forwards SSH traffic to localhost on port 22.
        *   `--ssl 127.0.0.1:444`: Forwards HTTPS traffic to localhost on port 444.
        *   `--pidfile /var/run/sslh.pid`: Specifies the PID file.

3.  **Starting `sslh`**:

    After configuring `sslh`, start or restart the service:

    ```bash
    sudo systemctl restart sslh
    ```

    Check the status to ensure it's running correctly:

    ```bash
    sudo systemctl status sslh
    ```

### Common Options

*   `--listen address:port`: Specifies the address and port to listen on.
*   `--ssh address:port`: Specifies the address and port to forward SSH traffic to.
*   `--ssl address:port`: Specifies the address and port to forward SSL/HTTPS traffic to.
*   `--openvpn address:port`: Specifies the address and port to forward OpenVPN traffic to.
*   `--tinc address:port`: Specifies the address and port to forward Tinc traffic to.
*   `--http address:port`: Specifies the address and port to forward HTTP traffic to.
*   `--pidfile file`: Specifies the PID file.
*   `--user user`: Runs `sslh` as the specified user.
*   `--foreground`: Runs `sslh` in the foreground (useful for debugging).
*   `--verbose`: Increases verbosity.

### Example Usage

1.  **Basic Setup**:

    Assume you want to run an SSH server and an HTTPS server on the same public port (443). Configure `sslh` to listen on port 443 and forward traffic accordingly.

    *   Edit `/etc/default/sslh`:

    ```
    RUN=yes
    DAEMON_OPTS="--user sslh --listen 0.0.0.0:443 --ssh 127.0.0.1:22 --ssl 127.0.0.1:444"
    ```

    *   Ensure your SSH server is running on port 22 (default).
    *   Configure your HTTPS server (e.g., Apache or Nginx) to listen on port 444 on localhost. For example, in your Nginx configuration:

    ```nginx
    server {
        listen 444 ssl;
        server_name localhost;
        # SSL configuration
        ssl_certificate /path/to/your/certificate.pem;
        ssl_certificate_key /path/to/your/privatekey.pem;

        location / {
            root /var/www/html;
            index index.html;
        }
    }
    ```

    *   Restart `sslh`:

    ```bash
    sudo systemctl restart sslh
    ```

    Now, SSH and HTTPS traffic to port 443 will be correctly forwarded.

2.  **Using OpenVPN**:

    To multiplex SSH, HTTPS, and OpenVPN on port 443:

    *   Edit `/etc/default/sslh`:

    ```
    RUN=yes
    DAEMON_OPTS="--user sslh --listen 0.0.0.0:443 --ssh 127.0.0.1:22 --ssl 127.0.0.1:444 --openvpn 127.0.0.1:1194"
    ```

    *   Ensure your OpenVPN server is running on port 1194.
    *   Restart `sslh`:

    ```bash
    sudo systemctl restart sslh
    ```

### Example Output

Since `sslh` is a multiplexer, it doesn't produce a direct output in the same way as a traffic analyzer like `tcpdump` or `ssldump`. Instead, its operation is reflected in how it routes traffic.

1.  **Checking Status**:

    To check if `sslh` is running:

    ```bash
    sudo systemctl status sslh
    ```

    **Expected Output**:

    ```
    ● sslh.service - SSL/TLS muxer
         Loaded: loaded (/lib/systemd/system/sslh.service; enabled; vendor preset: enabled)
         Active: active (running) since Tue 2025-02-25 16:00:00 UTC; 10s ago
           Docs: man:sslh(1)
                 man:sslh.cfg(5)
        Process: 12345 ExecStart=/usr/sbin/sslh $DAEMON_OPTS (code=exited, status=0/SUCCESS)
       Main PID: 12346 (sslh)
          Tasks: 1 (limit: 4621)
         Memory: 1.2M
         CGroup: /system.slice/sslh.service
                └─12346 /usr/sbin/sslh --user sslh --listen 0.0.0.0:443 --ssh 127.0.0.1:22 --ssl 127.0.0.1:444

    Feb 25 16:00:00 kali systemd[1]: Starting SSL/TLS muxer...
    Feb 25 16:00:00 kali systemd[1]: Started SSL/TLS muxer.
    ```

2.  **Verifying Connection**:

    To verify that `sslh` is correctly routing traffic, you can use `netstat` or `ss` to check the listening ports:

    ```bash
    sudo netstat -tulnp | grep 443
    ```

    **Expected Output**:

    ```
    tcp        0      0 0.0.0.0:443             0.0.0.0:*               LISTEN      12346/sslh
    ```

    This shows that `sslh` is listening on port 443.

3.  **Testing SSH**:

    Attempt to connect to the Kali machine on port 443 using SSH:

    ```bash
    ssh user@kali_ip -p 443
    ```

    If `sslh` is configured correctly, you should be able to establish an SSH connection.

4.  **Testing HTTPS**:

    Access the HTTPS server via a web browser using the Kali machine's IP address on port 443 (`https://kali_ip`). If `sslh` is configured correctly, you should see the web page served by your HTTPS server.

### Conclusion

`sslh` is a valuable tool for multiplexing services on a single port, which is particularly useful in situations where you need to bypass firewall restrictions or conserve public IP addresses. Proper configuration is key to ensuring that traffic is correctly routed to the appropriate backend services.




                                            ALTERNATIVE
`sslh` is a versatile tool available in Kali Linux that allows multiple protocols to share a single port. This is particularly useful for running services like HTTPS, SSH, OpenVPN, and others on the same port, which can help bypass firewall restrictions that often block non-standard ports. Below is an overview of how to use `sslh`, along with examples and expected outputs.

### Installation

To install `sslh`, you can use the following command:

```bash
sudo apt install sslh
```

During installation, you will be prompted to choose how `sslh` should run; selecting "standalone" is recommended for most users.

### Basic Usage

`sslh` can be configured to listen on a specific port and forward traffic to different services based on the protocol. The basic command structure is:

```bash
sslh -p <host:port> --ssh=<host:port> --tls=<host:port> --http=<host:port>
```

### Configuration Example

1. **Basic Configuration**:
   Here’s a simple example of how to configure `sslh` to listen on port 443 and forward traffic to SSH and HTTPS services:

   ```bash
   sslh -p 0.0.0.0:443 --ssh=127.0.0.1:22 --tls=127.0.0.1:443
   ```

   In this command:
   - `-p 0.0.0.0:443`: Listens on all interfaces on port 443.
   - `--ssh=127.0.0.1:22`: Forwards SSH traffic to port 22.
   - `--tls=127.0.0.1:443`: Forwards HTTPS traffic to port 443.

   **Expected Output**:
   ```
   Listening on 0.0.0.0:443
   Forwarding SSH to 127.0.0.1:22
   Forwarding TLS to 127.0.0.1:443
   ```

2. **Using a Configuration File**:
   You can also create a configuration file (e.g., `/etc/sslh/sslh.cfg`) for more complex setups. Here’s an example configuration:

   ```plaintext
   verbose: true;
   listen:
   (
       { host: "0.0.0.0"; port: "443"; }
   );
   protocols:
   (
       { name: "ssh"; host: "127.0.0.1"; port: "22"; },
       { name: "tls"; host: "127.0.0.1"; port: "443"; }
   );
   ```

   To run `sslh` with this configuration, use:

   ```bash
   sslh -F /etc/sslh/sslh.cfg
   ```

   **Expected Output**:
   ```
   Starting sslh with configuration from /etc/sslh/sslh.cfg
   Listening on 0.0.0.0:443
   ```

3. **Verbose Logging**:
   To enable verbose logging for debugging purposes, you can add the `--verbose` option:

   ```bash
   sslh -p 0.0.0.0:443 --ssh=127.0.0.1:22 --tls=127.0.0.1:443 --verbose
   ```

   **Expected Output**:
   ```
   [INFO] Listening on 0.0.0.0:443
   [INFO] Forwarding SSH to 127.0.0.1:22
   [INFO] Forwarding TLS to 127.0.0.1:443
   ```

### Conclusion

`sslh` is a powerful tool for multiplexing multiple protocols over a single port, making it easier to manage services and bypass firewall restrictions. By configuring `sslh` properly, you can streamline your network services and enhance security.

---
Learn more:
1. [sslh | Kali Linux Tools](https://www.kali.org/tools/sslh/)
2. [sslh installation guide - wiki](https://wiki.meurisse.org/wiki/sslh)
3. [Implementing Transparent Proxying Using sslh on Linux Systems](https://linuxsecurity.com/howtos/secure-my-network/implementing-transparent-proxying-on-linux-systems-with-sslh)
