# T03: Missió Nginx: Migració d'Alt Rendiment i Arquitectura Lleugera

## Breu descripció

### Introducció
La vostra implementació amb Apache ha estat un èxit i el client està satisfet. No obstant això, a la reunió d'estratègia tècnica d'ahir, la directiva va plantejar un nou repte: **l'escalabilitat**. Es preveu que Projecte Nexus rebi un pic de visites molt elevat durant la propera campanya de presentació.

Per aquest motiu, hem decidit obrir una línia de recerca i desenvolupament (R+D) per provar **Nginx**. Aquest servidor és conegut per la seva arquitectura orientada a esdeveniments, capaç de gestionar milers de connexions concurrents amb un consum de memòria molt inferior.

L'objectiu d'aquesta activitat és **replicar exactament la infraestructura** que vam muntar amb Apache, però utilitzant Nginx. Això ens permetrà comparar rendiment i tenir una alternativa d'altes prestacions al nostre catàleg de serveis.

> **Nota important:** Recordeu que dos serveis no poden escoltar pel mateix port (80/443) simultàniament a la mateixa IP. Haureu d'aturar Apache abans de començar.

---

## Descripció de l'activitat

L'activitat consisteix en la migració de la infraestructura web a un entorn **Nginx sobre Ubuntu Server**. Heu de documentar tot el procés en l'informe tècnic.

---

## 1. Preparació de l'Entorn i Instal·lació

- Atureu i deshabiliteu el servei Apache2 per alliberar els ports 80 i 443.
- Instal·leu el servidor web Nginx.
- Verifiqueu que el servei està actiu i que la pàgina de benvinguda de Nginx es mostra correctament al navegador.

---

## 2. Configuració de Server Blocks (Multidomini)

- Aprofiteu l'estructura de carpetes ja creada (`/var/www/nexus` i `/var/www/academia`).  
  Si cal, ajusteu els permisos (propietari `www-data`).
- Configureu **dos Server Blocks** (l'equivalent a VirtualHosts a Apache) a `/etc/nginx/sites-available/`.
- Creeu els **enllaços simbòlics** a `sites-enabled/` per activar les configuracions.
- Verifiqueu la sintaxis amb `nginx -t` abans de reiniciar el servei.

---

## 3. Personalització d'Errors

- Configureu la directiva `error_page 404` dins del bloc de servidor corresponent.
- Assegureu-vos que, quan es demani un fitxer inexistent, es mostri la pàgina d'error personalitzada creada anteriorment.

---

## 4. Seguretat i Certificats (HTTPS)

- Reutilitzeu els certificats SSL generats en l'activitat anterior (o genereu-ne de nous).
- Configureu el Server Block per escoltar al port 443 i indiqueu les rutes:
  - `ssl_certificate`
  - `ssl_certificate_key`
- Configureu una **redirecció 301** des del port 80 cap a la versió HTTPS del domini `disseny.local`.

---

## 5. Optimització amb HTTP/2

- Habiliteu el protocol HTTP/2 afegint el paràmetre `http2` a la directiva `listen` del bloc SSL.
- Comproveu amb les eines de desenvolupador del navegador que el contingut s'està servint amb aquest protocol.

---

## Què cal lliurar

- Una **memòria tècnica** de la instal·lació i configuració.
- Ha d’incloure **explicacions clares** i **proves de funcionament**.
- Els vostres clients no són tècnics, així que el document ha de ser entenedor.

---

## Material de suport

**UD5.AA2. El servidor Nginx.**  
Disponible al Moodle del mòdul de Serveis de Xarxa.
