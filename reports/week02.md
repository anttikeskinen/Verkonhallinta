1. Johdanto 

# Mikä on SNMP? 

Simple Network Management Protocol, joka valvoo verkon laitteita.

# Mihin SNMP:tä käytetään verkonhallinnassa? 

Verkkolaitteiden valvonnassa ja tiedonkeruussa.

2. Asennus 

# Miten SNMP-agentti asennettiin? 

apt update
apt install snmp snmpd -y

# Mitä konfiguraatiomuutoksia tehtiin? 

SNMP-agentti konfiguroitiin palvelimelle web1. Yhteisönimeksi tarkistettiin public

3. Kerätyt tiedot 

# Suoritetut SNMP-kyselyt 

sysName
sysDescr
sysUpTime

# Keskeiset komentotulosteet ja havainnot 

järjestelmän nimi: web1
käyttöjärjestelmä: Linux
uptime: 0:13:40.71

4. Verkkorajapinnat 

# SNMP:n avulla kerätyt verkkorajapintatiedot 

iso.3.6.1.2.1.2.2.1.2.1 = STRING: "lo"
iso.3.6.1.2.1.2.2.1.2.2 = STRING: "eth0"
iso.3.6.1.2.1.2.2.1.2.39 = STRING: "eth1"

# Rajapintojen tunnistaminen ja tulkinta 

Rajapintoja löytyi kaksi ja niitä yhdistää eth1.

5. OID-analyysi 

# Käytetyt OID-objektit 

# Mitä tietoa ne tarjoavat ja mihin niitä käytetään? 

OID		Tarkoitus
sysName.0	Laitteen nimi
sysDescr.0	Laitteen käyttöjärjestelmä ja kuvaus
sysUpTime.0	Laiteen käyttöaika
ifDescr		Verkkorajapintojen nimet/kuvaukset
ifOperStatus	Verkkorajapinnan toimintatila

# 5.2

Laite:	Nimi:	Käyttöjärjestelmä	Uptime
db1	db1	Linux			0:18:36:92
branch	branch-client Linux		0:18.33:75

6. Pohdinta 

# Mitä opit tehtävän aikana? 

SNMP käyttöä ja siihen tutustumista.

# Mitkä ovat SNMP:n tärkeimmät hyödyt? 

Mahdollistaa verkkolaitteiden keskitetyn valvonnan.

# Mitkä ovat SNMP:n rajoitukset tai haasteet?

Väärät asetukset voivat estää tiedonkeruun ja ne ovat heikko tapa tunnistautua, eivät salaa liikennettä.
