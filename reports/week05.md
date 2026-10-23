# Week05 - Wireshark

# Johdanto

- Tässä harjoituksessa tutustuttiin Wireshark-verkkoprotokolla-analyysiin käyttöön. Työn tavoitteena oli opetella verkkoliikenteen kaappaamista, suodattamista ja analysointia erilaisissa tilanteissa. Harjoituksen aikana tutkittiin DNS-kyselyitä, HTTP-yhteyksien ja TLS-kättelyä sekä HTTP basic authentication -todennusta.

# Osa 1
# Kaappaus

- Harjoituksessa kaapattiin liikennettä Wireshark ohjelmaa käyttäen ja suoritettiin kaappaus käyttämällä sekä capture filtteriä ja display filtterillä.

# Porttiskannaus

- Porttiskannaus tehtiin vierailemalla www.yle.fi sivustolla ja capture filterissä sekä display filtterissä etsittiin tuloksia port 443 haulla.

# Wireshark 

- Mistä IP-osoitteesta skannaus tuli? 192.168.100.89
- Mitä portteja testattiin? portti 443
- Mitä vastauksia palvelin lähetti? dns haku ei näyttänyt vastauksia, mutta tcp.port ja ip.addr saatiin tuloksia

# Osa 2

# DNS learn.hamk.fi

- IP-osoite: 195.148.239.84
- TTL aika: 1699, 28min 19sec

# TLS learn.hamk.fi

- versio: TLSv1.3
- Client Hello: TLS 1.2 ja Cipher suites length 32 ja 16 suites
- Server Hello: TLS 1.2 ja TLS_AES_128_GCM_SHA256

# Osa 3
# HTTP

- Docker-komento: docker run -d --env AUTH_USER=testi --env AUTH_PASS=salasana123 -v ~/site:/var/www -p 8888:80 tjarvenpaa/basic_auth
- käytetty suodatin kaappauksesta: http.authorization
- Authorization: Basic dGVzdGk6c2FsYXNhbmExMjM=
- Base64-koodauksen purku: testi:salasana123

# Yhteenveto

- Tehtävässä harjoiteltiin ja tutustuttiin Wireshark -ohjelman käyttöön ja analysoitiin verkkoliikennettä sen kaappauksen ansiosta. Tehtävä tehtiin pääosin moodlen ohjeitten mukaan, mutta vähän soveltaen viikkokohtaista tehtäväraportointia. Raportin yhteydessä on kuva lopun HTTP basic authentication tuloksen kuvakaappaus ja jokaisen osan suoritetussa wireshark kaappaus -tiedostot.

