# IPv6 skoleni

Autori skoleni:
- **Petr Cernohouz**, cz.nic
- **Emanuel Petr**, cz.nic

## Historie

- *1980* IPv4
- *1981* IPv4 CIDR
- *1995-8* IPv6

## IPv6

- IPv4 adresy dosly 2011
- kratkodobe reseni
  - CIDR - nedostatecne
  - NAT - *spatne!*

- vlastnosti, vyhody:
  - *dost* adres :smile:
  - *IPsec* - temer - by default
  - hlavicka:
    - 40 B fix! - IPv4 20 B *a vice*
    - neobsahuje nesmysly jako IPv4 - napr CRC (je na 2. i 4. vrstve)
  - unicast, multicast
    - broadcast je *all-hosts* multicast adresa (moc se nepouziva)
  - u IPv6 je bezne vice adres na jednom interface

## Sikovne prikazy

- pridelene adresy + multicast skupiny

```
ip -6  address
ip -6 maddress
```

- ping multicast adresy *all-nodes* ci *all-routers*

```
ping6 -c 2 ff02::1%eth0
ping6 -c 2 ff02::2%eth0
```

- cistsi zjisteni sousedu:

```
ip -6 neighbor
```

- informace o ohlasenem smerovaci

```
rdisc6 eth0
```
