# Google Dorking Toolkit

## Overview
Google dorking is a passive reconnaissance method leveraging advanced Google search operators to discover exposed resources, files, and sensitive information on the internet. This README guides penetration testers and bug bounty hunters in using Google dorks efficiently.[web:7][web:3]

## Table of Contents
- Overview
- Getting Started
- Common Google Dork Operators
- Example Dorks
- Useful Resources
- References
- License

## Getting Started
To use these resources, clone the repository and try out the example Google dorks listed below.

---

## Common Google Dork Operators

| Operator      | Description                          | Example                       |
|---------------|--------------------------------------|-------------------------------|
| site:         | Search results from a domain         | site:target.com             |
| inurl:        | Keyword in result URL                | inurl:admin                 |
| intitle:      | Keyword in page title                | intitle:index of            |
| intext:       | Keyword in page body                 | intext:password             |
| filetype:     | Search for file type                 | filetype:pdf                |
| ext:          | Alternate filetype search            | ext:xml                     |
| cache:        | Cached version of a page             | cache:example.com           |

## Example Google Dorks

```text
intitle:"index of" "password"
filetype:env "DB_PASSWORD"
inurl:login
intitle:"web client: login"
site:example.com intext:"confidential"
inurl:read.php?=
inurl:profile_view.php?id=
filename:.npmrc _auth
