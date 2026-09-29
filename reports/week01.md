# Week 01

## Johdanto

- Ympäristö simuloi yritysverkkoa ja mahdollistaa verkkolaitteiden hallinnan, dokumentoinnin ja automaation harjoittelun.

## Ympäristön käyttöönotto 

- Containerlab asennus
- Ympäristön käynnistys
- Topologian tutkiminen

## 1.1 Topologian kartoitus

- Laite -- Tarkoitus: -

# R1		-- R1 on "solmu" YAML-konfiguraatio tiedostossa
# R2		-- R2 on toinen "solmu" node YAML-konfiguraatiossa
# R3		-- R3 on kolmas reititin/solmu samassa rakenteessa
# Client1	-- on yleisesti määritelty kevyenä Linux hostina näiden r1-r3 solmujen yhteydessä.
# attacker	-- Simuloi kyberturvallisuutta hyökkääjän, palomuurin ja hyökkäyksen kohteena olevan serverin kautta.
# Web1		-- Web-palvelin (Nginx)
# db1		-- Tietokanta Linux-palvelimessa (database1)
# brand-client	-- Työasema, josta harjotukset tehdään
# ansible	-- Tyäaseman automaatio- ja hallintapalvelin
# Prometheus	-- Kerää dataa/metriikkaa muilta labran laitteilta.
# Grafana	-- Ohjelmisto visualisointiin ja raportointiin.
# Zabbix	-- Datan kerääjä ja prosessoiva valvontajärjestelmä.

## 1.2 Verkkokaavio

- kts. /reports/images/ -kansio

## 1.3 IP-osotteiden dokumentointi

- Verkko -- Tarkoitus -- Yhdyskäytävä -

10.10.10.0/24 | Asiakasverkko | 10.10.10.1
10.10.20.0/24 | Palvelinverkko | 10.10.20.1
10.10.30.0/24 | Työasemaverkko | 10.10.30.1
10.10.99.0/24 | Hallintaverkko | 10.10.99.1
10.255.12.0/30 | R1-R2 reititinlinkki | ei yhdyskäytävää
10.255.23.0/30 | R2-R3 reititinlinkki | ei yhdyskäytävää

- Mitä laitteita kuhunkin verkkoon kuuluu?
R1 kuuluu client ja attacker. R2 Web1 ja db1. R3 on branch-client.

- Mikä reititin toimii yhdyskäytävänä?
10.255.12.0 R1:n ja R2:n välinen siirtoverkko. 10.255.23.0 R2:n ja R3:n välinen siirtoverkko.

- Mitä tarkoitusta verkko palvelee?
Verkko palvelee asiakkaiden, palvelimien, hallintajärjestelmän tai verkkolaitteiden välistä tiedonsiirtoa niiden käyttötarkoituksen mukaisesti.

## Tehtävä 1.4 Reitityksen tutkiminen

- Löytyykö yhteys kaikkiin verkkoihin
Yhteys löytyy raportin vaativiin komentojen yhteyksiin.

- Mitä reittiä liikenne kulkee
Verkko 10.10.20.0 kulkee reittiä Client1-R1-R2-
Verkko 10.10.30.0 kulkee reittiä Client1-R1-R2-R3-

- Mitä reitittimiä reitille kuuluu
Ekassa R1 ja R2, toisessa R1,R2 ja R3

- Komentojen tulosteet kuvana!

## Yhteenveto

- Mitkä asiat verkon dokumentaation muodostamisessa kuluttivat eniten aikaa ja miksi?
Dokumentointi yleisesti ja alkuun verkon hahmottaminen ja sen tutkiminen.

- Miten dokumentaatio mielestäsi auttaa palvelusta vastaavaa it-asiantuntijaa työssään?
Hahmottamaan verkon yhteyksiä ja verkon rakennetta/struktuuria.
