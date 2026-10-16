# 1 - Johdanto

- Prometheus on monitorointijärjestelmä, joka kerää palvelimelta ja sovelluksilta mittaustietoja exporterin avulla.
- Kerättyä tietoa voidaan tarkastella erillaisten PromQL-kyselyiden avulla ja visualisoida esimerkiksi Grafanassa.

# 2 - Node Exporterin käyttöönotto

- Ensiksi varmistetaan, että ympäristö on käynnissä ja sen jälkeen latasin Node Exporterin uusimman version web1-palvelimelta.
- Seuraavana purettiin paketti ja käynnistettiin se node exporterin hakemistosta.
- Tarkistetaan, että ohjelma vastaan ja tulos antaa vastauksena pitkän listan eri mittariarvoja tekstinä.
- Mittareita kerätään yhteensä viiten eri kyselyyn ja näkymään, joita ovat prosessorin-, muistin- ja levytilan käyttö %, sekä verkkodatan vastaanotto ja lähetys.


# 3 - Prometheus

- Avataan Prometheus selaimessa osoittesta http://localhost:9090 ja ylävalikosta Status välilehdeltä Target Health.
- Sieltä näkyy eri kohteita ja Web1 pitäisi näkyä alempana tilassa UP.

# 4 - Dashboard

- Grafana otetaan käyttöön ja tehdään oma dashboard joka näyttää mittausarvot diagramina. Kirjaudutaan Grafana sivulta http://localhost:3000 ja se kysyy tunnusta ja salasanaa.
- Kun Grafana on päästy kirjautuun, tehdään uusi dashboard nimeltä Golden Topology Monitoring. Vasemmasta valikosta Dashboards ja sieltä New -> New dashboard. Valitse Add visualization ja valitse Prometheus tietolähteeksi.
- Tehdään paneelit CPU Usage %, Memory Usage %, Disk Usage %, Network Receive ja Network Transmit. Käytetään niihin tehtävän PromQL-kyselyjä.

# 5 - Kuormitustesti

- Tehdään kuormitustesti web1-palvelimelle. Aloitetaan se asentamalla stress-ng paketti jolla saadaan generoitua kuormitusta testaus menetelmällä.
- Ajetaan komento stress-ng --cpu 4 --timeout 60s, ja tarkkaillaan dashboardin muutoksia.
- Jokaisessa paneelissa huomataan "piikki" web1-palvelimen kuvaavalla käyrällä. Pienin muutos CPU Usagen kohdalla suhteessa sen koko skaalaan, mutta toisaalta se on myös hyvin tasainen ennen ja jälkeen.
- Levytilan käyttö nousi pykälän korkeammalle ja pysyy siinä samassa stabiilina.
- Verkkoliikenteessä näkyi molemmissa suht. korkea tasainen piikki.

# 6 - SNMP vs Prometheus

-- Ominaisuus --	-- SNMP --					-- Prometheus --
Tiedonkeruu		Kyselyt verkkolaitteilta SNMP:n avulla		Kerää metriikat exportereilta HTTP:n kautta
Käyttöönotto		Yksinkertainen, mutta vaatii SNMP asetukset	Tarvii Prometheuksin ja exporterit
Mittarien määrä		Rajallinen, MIB-objektit			Erittäin laaja määrä eri metriikoita
Visualisointi		Ei omaa visualisointia				Toimii hyvin Grafanan kautta
Hälytysmahdollisuudet	Rajalliset					Alertmanagerin avulla
Soveltuvuus pilveen	Kohtalaiset					Erinomainen

# 7 - Pohdinta

1. Prometheus tarjoaa enemmän mittareita, tehokkaat kyselyt sekä paremman integraation Grafanan kanssa.
2. CPU:n käyttöä, muistin käyttöä, levytilaa, verkkoliikennettä ja palveluiden saatavuutta.
3. Dashboard näyttää käyttäjälle palvelimien suorituskyvyn, kuormituksen ja resurssien käytön yhdellä näkymällä.
4. Levytilan käyttöasteen, verkkoirheet ja palveluiden vasteajat.
5. Monitorointitiedot auttavat tunnistamaan ongelman ajankohdan,syyn ja vaikutuksen järjestelmän toimintaan.

# 8 - Yhteenveto

- Harjoituksessa otettiin käyttöön Node Exporter, kerättiin metriikoita Prometheuksella ja visualisoitiin niitä Grafanassa. Lisäksi opittiin käyttämään PromQL-kyselyitä ja rakentaamaan monitorointidashboardin, jonka avulla palvelimen toimintaa voidaan seurata keskitetysti.

