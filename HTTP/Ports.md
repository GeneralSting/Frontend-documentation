# Ports

- a port is not physical connection, it's a `logical connection` what's used by programs and services to exchange information
- it specifically determines which program or service on a computer or server that is going to be used
  - web page
  - ftp
  - email
- always associated with an `IP address`
  - port number determines wich service or program on that server we want to use
    - ports will have a unique number that identifies them, 0-65553
    - assigned by `IANA`, Internet assigned Numbers Authority
      - 80 - HTTP
      - 443 - HTTPS
      - 21 - FTP
      - 25 - email (SMTP)
    - three categories
      - 0-1023 - `system` or well-known ports
      - 1024-49151 - user or `registered ports`, can be registered by companies and developers for a particular service
        - 1102 - Adobe Server
        - 1433 - Microsoft SQL Server
        - 1527 - Oracle
      - 49152-65535 - dynamic or `private ports`, client-side ports that are free to use during a session (viewing the web page)

## Netstat

- short for `Network Statistics`
  - command line tool that is used to display the current network connections and port activity on you computer

## FTP

- `File Transfer Protocol` is the standard protocol used to transfer files over a network
- port 21
