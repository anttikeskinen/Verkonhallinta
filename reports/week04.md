# 1. Johdanto

Mikä on infrastructure as code?

# 2. Inventory

Ympäristön rakenne:
- mitä laitteita inventory sisältää? Reitittimet, palvelimet ja verkon hallintalaitteet (r1-r3, db1, web1, branch-client, attacker, Prometheus, grafana, zabbix etc.)
- miten ryhmät on muodostettu? Routers=r1-r3, Client Workstation=client1,branch ja attacker, Serverit=web1 ja db1, Monitorointi=Prometheus,Grafana,Zabbix ja Cadvisor, Management=Ansible, Verkon segmentti=user_network(client1,attacker), server_network(web1,db1), branch_office(branch_client)
- mitä hyötyä ryhmistä on? Kohdennettu hallinta, muuttujat (variables), ryhmät ja selkeä dokumentaatio.

# 3. Ensinmäinen playbook

- mitä playbook tekee? Playbook testaa, voidaanko inventaariossa määritettyihin laitteisiin muodostaa yhteys Ansiblella.
- mitä tuloksista voidaan päätellä? Ansible pystyy hallitsemaan laitteita, joissa SSH-palvelu on käynnissä. Reitittimet vastaa ja web1 (sen jälkeen kun manuaalisesti kävin yhteyden muodostamassa).

# 4. Esimerkkiplaybookit

Havainnot SNMP- ja Node Exporter -playbookeista
- mitä moduuleja palybookeissa käytetään (esim. apt, copy, Service, get_url, unarchive? SNMP: apt, copy, service, shell & register, debug Node: apt, file, get_url, unarchive, copy, Shell, debug
- miten muuttujia (vars) hyödynnetään? esim. versionumerossa ja polkujen määrittelyssä.
- miten handlers -lohkoa käytetään SNMP-playbookissa? Handlers käytetään snmp-palvelun uudelleenkäynnistyksessä.
- miksi Node Exporter -playbook ei tarvitse handleria? Koska palvelua ei tarvitse käynnistää uudelleen konfiguraatiomuutosten takia.

# 5. Oma playbook

Koodi ja suorituksen tulokset (web-palvelin ja/tai tietokantapalvelin)
- ota talteen suorituksen tuloste (ansible-playbook output) raporttia varten
ansible-playbook tuloste kuvakaappauksena /reports/images/oma_playbook.png

root@web1:/# curl http://localhost
<html>
  <body>
    <h1>web1</h1>
    <p>Web server installed by Ansible</p>
  </body>
</html>

# 6. Kerää järjestelmätietoja

- käyttöjärjestelmä 24.04
- IP-osoite 172.20.20.4
- prosessorien määrä 6
- muistin määrä 7318

# 7. Vertailu

Käsin vs. automaatio

- vertaa käsin tehtyjä asennuksia. Käsin tehtävät asennukset antavat hyvän ymmärryksen siitä, mitä järjestelmässä tapahtuu, mutta ne vievät aikaa ja mahdollisesti virheitä tulee enemmän.
- Ansiblella tehtyjä asennuksia. Ansiblella tehtävät asennukset ovat nopeampia ja toistettavia useilla laitteilla.
- mitä hyötyjä automaatiosta on? Vähentää kuormaa, nopeuttaa prosessia, vähentään virheitä ja mahdollistaa saman konfiguraation käyttämisen useilla laitteilla.
- missä tilanteissa automaatio on välttämätön? Automaatio on erityisen hyödyllistä suurissa ympäristöissä, joissa hallitaan useita palvelimia tai verkkolaitteita ja toistuvissa ylläpitotehtävissä.

# 8. Yhteenveto

Opitut asiat

Tässä harjoituksessa tutustuttiin Ansibleen ja sen käyttöönottoon verkko- ja palvelinympäristössä ja niiden hallinnassa. Harjoituksessa tarkasteltiin inventory-tiedostoa, suoritettiin valmiita playbookeja ja luotiin oma web1 -palvelimen asennusplaybook sekä kerättiin järjestelmätietoja Ansiblella.
