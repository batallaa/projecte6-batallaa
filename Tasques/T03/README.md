# 🚀 T03: Missió Nginx — Migració d'Alt Rendiment i Arquitectura Lleugera

## 📝 Breu descripció

### 🔧 Introducció
La vostra implementació amb Apache ha estat un èxit i el client està satisfet. No obstant això, a la reunió d'estratègia tècnica d'ahir, la directiva va plantejar un nou repte: **l'escalabilitat** 📈.  
Es preveu que Projecte Nexus rebi un pic de visites molt elevat durant la propera campanya de presentació.

Per aquest motiu, obrim una línia de **R+D** per provar **Nginx**, un servidor conegut per la seva arquitectura orientada a esdeveniments ⚡, capaç de gestionar milers de connexions concurrents amb molt poc consum de memòria.

L'objectiu és **replicar exactament la infraestructura que teníem amb Apache** però utilitzant Nginx, per poder comparar rendiment i disposar d’una alternativa d’altes prestacions.

> ⚠️ **Importante:** No poden funcionar dos serveis escoltant el port **80/443** alhora a la mateixa IP.  
> Cal **aturar Apache** abans de començar.

---

## 📘 Descripció de l'activitat

Migrar tota la infraestructura web a **Nginx sobre Ubuntu Server** 🐧.  
Cal documentar tot el procés en un informe tècnic.

---

## 1️⃣ Preparació de l'Entorn i Instal·lació

- 🛑 Atureu i deshabiliteu **Apache2** per alliberar els ports.
- 📥 Instal·leu el servidor web **Nginx**.
- 🔍 Verifiqueu que està actiu i que la pàgina per defecte es veu al navegador.

---

## 2️⃣ Configuració de Server Blocks (Multidomini) 🌐🌐

- Reutilitzeu les carpetes existents:  
  - `/var/www/nexus`  
  - `/var/www/academia`  
- Ajusteu permisos si cal (`www-data`).
- Creeu **dos Server Blocks** a `/etc/nginx/sites-available/`.
- Activeu-los amb enllaços simbòlics cap a `sites-enabled/`.
- Comproveu la sintaxi amb: `nginx -t` ✔️

---

## 3️⃣ Personalització d'Errors ❌➡️📄

- Configureu la directiva:  
  `error_page 404 /error/404.html;`
- Verifiqueu que la pàgina d’error personalitzada apareix quan demaneu un fitxer inexistent.

---

## 4️⃣ Seguretat i Certificats (HTTPS) 🔐

- Reutilitzeu o genereu els certificats SSL.
- Configureu el bloc de servidor per escoltar a `443` amb:
  - `ssl_certificate`
  - `ssl_certificate_key`
- Afegiu redirecció **301** permanent del port `80` cap a `https://disseny.local`.

---

## 5️⃣ Optimització amb HTTP/2 ⚡📡

- Afegiu el paràmetre `http2` a la directiva `listen` del bloc SSL.
- Verifiqueu al navegador que el contingut es serveix amb HTTP/2 (pestanya Network).

---

## 📤 Què cal lliurar

- Una **memòria tècnica detallada** amb:
  - Explicacions clares 🧠
  - Proves de funcionament 🖼️
- Recordeu que els clients *no són experts*, així que el llenguatge ha de ser entenedor.

---

## 📚 Material de suport

**UD5.AA2. El servidor Nginx**  
Disponible al Moodle del mòdul de Serveis de Xarxa.
