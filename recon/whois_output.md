# WHOIS

WHOIS is a *network protocol* used to query a database that contains information about domain name registrations and IP address assignments.  

The WHOIS database is maintained by various organizations, including:
- Internet Service Providers (ISPs)  
- Domain name registrars  
- Regional Internet registries  

---

## Common Use
The most common use of WHOIS is to obtain information about a particular *domain name* or *IP address*.  

You can use a WHOIS lookup tool or the command line to query the appropriate WHOIS server and return the relevant information.  

---

## WHOIS Command


whois DOMAIN_NAME

---

## Information Provided by WHOIS

- *Registrar* → Shows via which registrar the domain name was registered.  
- *Contact* → Provides name, organization, address, phone, and other details.  
- *Name Server* → Indicates which server is used to resolve the domain name.  
- *Dates* → Lists the creation date, last update date, and expiration date of the domain.

---

## Example WHOIS Command

whois example.com

---

## Example WHOIS Output

```bash
Domain Name: EXAMPLE.COM
Registry Domain ID: 2336799_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.iana.org
Registrar URL: http://www.iana.org
Updated Date: 2024-05-01T07:00:00Z
Creation Date: 1995-08-14T04:00:00Z
Registry Expiry Date: 2030-08-13T04:00:00Z
Registrar: Internet Assigned Numbers Authority
Registrar IANA ID: 376
Registrar Abuse Contact Email: abuse@iana.org
Registrar Abuse Contact Phone: ‪+1.3103015820‬
Domain Status: active
Name Server: A.IANA-SERVERS.NET
Name Server: B.IANA-SERVERS.NET


