# Week06

# 1. Johdanto

- Zabbix on avoimen lähdekoodin valvontajärjestelmä, jolla voidaan seurata palvelimia, verkkolaitteita ja sovelluksia. Sen avulla voidaan kerätä suorituskykytietoja, seurata palveluiden toimintaa sekä lähettää hälytyksiä ongelmatilanteissa.

# 2. Hostin lisääminen

- Zabbixiin lisättiin valvottavia kohteita kurssiympäristöstä. Valvonta toteutettiin SNMP:n avulla käyttäen community-arvoa public. Web1-palvelimella SNMP-agentti konfiguroitiin kuuntelemaan UDP-porttia 161.

# 3. Dashboard

- Dashboardiin luotiin näkymä palvelimen valvontatiedoille. Dashboard mahdollistaa valvontatietojen tarkastelun yhdestä näkymästä.

# 4. Mittarit

- CPU-kuormitus
- Muistin käyttö
- Verkkoliikenne
- SNMP-agentin tila
- CPU- ja muistimittarit kertovat palvelimen kuormituksesta. Verkkoliikenteen seuranta auttaa tunnistamaan häiriöitä sekä poikkeuksellista liikennettä. SNMP-agentin seuranta varmistaa, että valvontaliikenne toimii.

# 5. Triggerit

- Luotiin triggeri, joka hälyttää mikäli valvottava palvelin ei vastaa SNMP-kyselyihin tai jos resurssien käyttö ylittää määritetyn raja-arvon.
- High CPU Usage
- {web1:system.cpu.util[snmp,0].last()}>80
- Warning
- Low Free Disk Space
- {web1:system.swap.free[memAvailSwap.0].last()}<20
- Warning


# 6. Häiriötilanne

- Testi tehtiin cpu-kuormituksella yes > /dev/null, josta syntyi triggeri ja hälytys. Tarpeeksi monta kertaa kun teki niin pienellä viiveellä syntyi kuorma joka nousi 100% asti.
- Tämän jälkeen pysäytettiin palvelu pkill node_exporter jonka jälkeen mittarit hiljenivät. noin parin minuutin kuluttua.

# 7. Vertailu

- SNMP soveltuu hyvin verkkolaitteiden valvontaan. Prometheus tarjoaa tehokkaan mittarien keruun ja toimii erityisen hyvin Grafanan kanssa. Zabbix yhdistää valvonnan, visualisoinnin ja hälytykset samaan järjestelmään.
- taulukko vertailu.png

# 8. Yhteenveto

- Harjoituksessa tutustuttiin Zabbixin käyttöön valvontajärjestelmänä. Zabbixiin lisättiin valvottavia kohteita, tarkasteltiin mittareita ja dashboardeja sekä testattiin SNMP-agentin toimintaa. Harjoituksen aikana opittiin SNMP:n, Prometheuksen ja Zabbixin välisiä eroja sekä valvonnan ja hälytysten merkitystä verkonhallinnassa.
