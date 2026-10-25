Campuslab replacement

1. Ympäristön tarkistaminen

R1 - 172.20.20.8
R2 - 172.20.20.12
R3 - 172.20.20.11
Ansible - 172.20.20.3

Lyhyt kuvaus

2. SSH-yhteydet ja Ansible-inventaario

- ssh yhteys kahteen reitittimeen, r2 172.20.20.12 ja r3 172.20.20.11 antavat connection refused.
- userak@WIN-3IEVE0CBEQN:~/Verkonhallinta/automation-lab$ ansible-inventory -i inventory/hosts.yml --graph
@all:
  |--@ungrouped:
  |  |--r1-edge
  |  |--r2-core
  |  |--r3-branch
- userak@WIN-3IEVE0CBEQN:~/Verkonhallinta/automation-lab$ ansible all -i inventory/hosts.yml -m ping
[WARNING]: ansible-pylibssh not installed, falling back to paramiko
r3-branch | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
r2-core | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
r1-edge | SUCCESS => {
    "changed": false,
    "ping": "pong"
}

3. Verkon automaattinen inventointi

- Laadin playbookin facts.yml, joka sisälsi seuraavat tiedonkeruukomennot: hostname, ip addr, uname -a, uptime.
- R1 yhdistää verkon 10.10.10.0/24 runkoverkkoon
- R2 toimii keskusreitittimenä ja sisältää useampia rajapintoja sekä verkkoja
- R3 yhdistää verkon 10.10.30.0/24 runkoverkkoon.

4. Konfiguraatioiden varmistaminen

- Backup-playbook luotiin tehtävänannon mukaisesti hakemaan FRRouting-konfiguraatio komennolla vtysh -c "show running-config" ja tallentamaan se varmuuskopiotiedostoksi. Playbook kohtasi saman SSH-yhteysongelman kuin inventointitehtävä eikä varmuuskopioita voitu muodostaa.

5. Verkon tila Git-versionhallintaan

- Versionhallinnan avulla muutokset voidaan jäljittää, dokumentoida ja tarvittaessa palauttaa aiempaan toimivaan konfiguraatioon.

6. Haliitu konfiguraatiomuutos

- Playbook luotiin tehtävänannon mukaisesti lisäämään loopback-rajapinta R3-reitittimelle. Suoritus kuitenkin epäonnistui samasta SSH/portti 22 -yhteysongelmasta kuin aiemmissa inventointi- ja varmuuskopiointitehtävissä, minkä vuoksi muutosta ei voitu toteuttaa eikä idempotenssia voitu käytännössä todentaa.

7. Muutoksen tarkistaminen

- Muutoksen tekeminen ei takaa, että muutos toteutui oikein. Tarkistus varmistaa, että haluttu lopputulos saavutettiin ja että järjestelmä toimii edelleen odotetusti.

8. Muutoksen tallentaminen

- Yhteysvirheen takia tätäkään osa-aluetta ei saatu tehtyä tehtävän vaatimalla tasolla ja onnistuneesti.

9. Virhetilanne ja palautuminen

- Sama tässäkin kuin aiemmissa tehtävissä ongelmaksi koitui ssh-yhteyden saanti ja siihen liittyvät ongelmat. Havaitut ongelmat olivat kurssin omassa playbooks/ping.yml ja omatekemät playbookit, jotka palauttivat virheen Unable to connect to port 22. Lisäksi reitittimissä ei havaittu käytössä olevaa SSH-palvelua.

# Yhteenveto

- Harjoituksessa tutustuttiin Ansible-inventaarioihin, playbookeihin, verkkoautomaation perusteisiin sekä Git-versionhallintaan. Inventaario ja yhteystestit toimivat onnistuneesti, mutta reitittimien hallinta pysähtyi SSH-yhteysongelmaan, minkä vuoksi automaattista tiedonkeruuta ja konfigurointia ei saatu vietyä loppuun.

- Tehtävän vaaditut playbookit saatiin tehtyä, mutta niiden toimivuutta en pystynyt testaamaan ssh-yhteyden ongelmien takia. Tästä syystä otin kuvakaappaukset: Oma inventaario, Reitittimen Ansible-yhteydestä, Kurssin oma ping.yml epäonnistumisesta, Reitittimen ssh-palvelinta ei ole, ssh-avain tehty, omasta facts.yml, backup.yml, loopback.yml ja verify.yml

inventory.png
ansible-routers.png
ansible-ping.png
routers-ssh.png
ssh-avain.png
facts.png
backup.png
loopback.png
verify.png
