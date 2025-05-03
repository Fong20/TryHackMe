
# Reconnaissance
Reconnaissance is defined as the preliminary survey to gather information about a target. It is the first step in The Unified Kill Chain to gain an initial foothold on a system.

## Types of Reconnaissance

### Passive Reconnaissance
Uses publicly available resources, no direct interaction.

Examples:
- Looking up DNS records of a domain from a public DNS server.
- Checking job ads related to the target website.
- Reading news articles about the target company.

### Active Reconnaissance
Requires direct engagement with the target. Due to the invasive nature of active reconnaissance, it is highly legally sensitive.

Examples:
- Connecting to one of the company servers such as HTTP, FTP, and SMTP.
- Calling the company in an attempt to get information (social engineering).
- Entering company premises pretending to be a repairman.

## Passive Reconnaissance Tools

### `whois`
- **Purpose**: Queries WHOIS records to obtain registrar, registrant contact info, domain creation, update and expire dates, and name servers.
- **Command**: `whois DOMAIN_NAME`
- **Example**: `whois tryhackme.com`

![image](https://github.com/user-attachments/assets/8284aa90-d5a8-49d5-8863-1ca1cdb7d043)

### `nslookup` (Name Server Lookup)
- **Purpose**: Queries DNS servers for various DNS records.
- **Syntax**: `nslookup -type=QUERY_TYPE DOMAIN_NAME DNS_SERVER`
- **Query Types**:
  - `A`: IPv4
  - `AAAA`: IPv6
  - `CNAME`: Canonical name
  - `MX`: Mail exchange
  - `SOA`: Start of authority
  - `TXT`: Text records
- **Examples**:
  - `nslookup -type=A tryhackme.com 1.1.1.1` returns all the IPv4 addresses used by tryhackme.com.

    ![image](https://github.com/user-attachments/assets/cd5514a7-a434-44f6-9c59-72f9ef492124)

  - `nslookup -type=MX tryhackme.com` returns email servers and configurations for a particular domain.

    ![image](https://github.com/user-attachments/assets/f347d4d5-e687-43d3-8560-a512a83dfb65)

### `dig` (Domain Information Groper)
- **Purpose**: Advanced DNS querying tool which provides more information as compared to nslookup.
- **Syntax**: `dig @SERVER DOMAIN_NAME RECORD_TYPE`
- **Examples**:
  - `dig tryhackme.com A`

    ![image](https://github.com/user-attachments/assets/f56b93c7-f183-4ebb-ab43-ad411d4a8bb1)

  - `dig @1.1.1.1 tryhackme.com MX`
  - `dig tryhackme.com TXT`

### Online Services

#### DNSDumpster
- **Purpose**: DNS lookup tools, such as nslookup and dig, cannot find subdomains on their own. As a result, DNSDumpster is used to discover DNS records, subdomains, IPs, and geolocation info.
- **Features**:
  - Graphical output
  - Exportable data
  - Visualized network maps

#### Shodan.io
- **Purpose**: Search engine for internet-connected devices.
- **Information Provided**:
  - IP addresses
  - Hosting providers
  - Geo-location
  - Server type/version

## Useful Commands Summary

| Purpose                          | Commandline Example                                 |
|----------------------------------|------------------------------------------------------|
| Lookup WHOIS record              | `whois tryhackme.com`                                |
| Lookup DNS A records             | `nslookup -type=A tryhackme.com`                     |
| Lookup DNS MX records (DNS srv) | `nslookup -type=MX tryhackme.com 1.1.1.1`            |
| Lookup DNS TXT records          | `nslookup -type=TXT tryhackme.com`                  |
| Lookup DNS A records with dig   | `dig tryhackme.com A`                                |
| Lookup DNS MX with dig (server) | `dig @1.1.1.1 tryhackme.com MX`                      |
| Lookup DNS TXT with dig         | `dig tryhackme.com TXT`                              |
