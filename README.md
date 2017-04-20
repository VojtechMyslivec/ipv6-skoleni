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

## Router advertisment

- oznameni lokalniho prefixu a defaultni cesty
- casovace
    - `valid_lifetime`
        - jak dlouho bude cesta platna
        - nejmene 2 h
    - `preferred_lifetime`
        - kdyz vyprsi, je po dobu `valid_lifetime` jeste deprecated
        - pokud bude jina platna cesta, pouzije ji
        - po dobu `valid` tedy zustava jako zalozni cesta
- host si vezme vsechny IP, ktere obdrzi v *RA*

- nastroj `ramond` pro monitorovani *RA*

### Konfigurace bird

Viz soubor `conf/bird6.conf`

[docs](http://bird.network.cz/?get_doc&f=bird-6.html#ss6.9)

### Konfigurace radvd

Viz soubor `conf/radvd.conf`

## Rozbehnuti IPv6 konektivity

1. RA od poskytovatele
    - prefix
    - def. GW
    - dhcp
1. DHCPv6 client
    - DNS?
    - prideleny delegovany prefix?
1. DHCPv6 server
    1. **RA**
        - def. gw
        - prefix
        - DHCPv6 varianta (stateless, ...)
    1. **stateless DHCPv6**
        - DNS
        - lokalni domena

### Alternativa

**`pass-through`**/**`ndproxy`**?

Pokud neni prideleny delegovany prefix, muze se router chovat
jako bridge/switch pro IPv6 - IPv6 'proxy', preposila ND

## 6-to-4 tunel

- rozbehnuti IPv6 konektivity pres IPv4 only uplink
- vyzaduje verejnou IPv4 adresu
- vnitrni sit ma prideleny prefix
    - `2002:IP:v4::/48`
    - hranicni router tuneluje do IPv4 packetu
    - konec tunelu je *anycast* IP `192.88.99.1`
        - v CR provozuje **cz.nic** :tada:
