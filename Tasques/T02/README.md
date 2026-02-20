
# 🔐 T02: Missió Apache  
## 🌍 Desplegament Multidomini i Segur

## 📝 Breu Descripció
Els assessors de la incubadora tenien raó: el primer client ja ha arribat!  
**Nexus**, una nova empresa de formació a Mataró, necessita desplegar i gestionar la seva infraestructura web. Abans de migrar al núvol, volen establir una base robusta i segura als seus serveis corporatius.

Els requisits del client són:
- 🌐 Allotjar **dos portals web independents** en un únic servidor.
- 🔒 Garantir **comunicacions segures** amb SSL/TLS.
- ⚡ Optimitzar el **rendiment** amb protocols moderns (HTTP/2).

Tot això sobre **Ubuntu Server + Apache**, primer en una màquina virtual local, i després en un VPS real.

---

# 🎯 Objectiu del Projecte
Configurar un servidor Apache professional amb suport multidomini, HTTPS, redireccions segures i optimització HTTP/2, documentant tot el procés en una memòria tècnica.

---

# 🧩 Tasques a Realitzar

## 1️⃣ Instal·lació i Configuració Base

### 🔧 Accions
Instal·lar Apache:
```bash
sudo apt update
sudo apt install apache2
```

Verificar estat:
Shellsudo apachectl statusMostra més línies
Verificació d’usuari i permisos:
Shellls -ld /var/wwwgetent passwd www-dataMostra més línies

## 2️⃣ Desplegament de VirtualHosts (Multidomini)
🌐 Dominis

projectenexus.test
academia.test

📁 Estructura de directoris
/var/www/
 ├── projectenexus/
 │    └── public_html/
 └── academia/
      └── public_html/

🛠️ Configuració de VirtualHosts
Shellsudo nano /etc/apache2/sites-available/projectenexus.confsudo nano /etc/apache2/sites-available/academia.confMostra més línies
Activació:
Shellsudo a2ensite projectenexus.confsudo a2ensite academia.confsudo systemctl reload apache2Mostra més línies
DNS local:
127.0.0.1   projectenexus.test
127.0.0.1   academia.test


## 3️⃣ Personalització d’Errors
Directiva al VirtualHost:
Apache ConfigErrorDocument 404 /errors/404.htmlMostra més línies
Arxiu:
/var/www/projectenexus/public_html/errors/404.html


## 4️⃣ Seguretat i Certificats (HTTPS)
Habilitar SSL:
Shellsudo a2enmod sslMostra més línies
Certificat autosignat:
Shellsudo openssl req -new -newkey rsa:2048 -nodes -keyout nexus.key \  -x509 -days 365 -out nexus.crtMostra més línies
VirtualHost HTTPS:
Apache Config<VirtualHost *:443>    ServerName projectenexus.test    DocumentRoot /var/www/projectenexus/public_html    SSLEngine on    SSLCertificateFile /etc/ssl/certs/nexus.crt    SSLCertificateKeyFile /etc/ssl/private/nexus.key</VirtualHost>Mostra més línies
Redirecció HTTP → HTTPS:
Apache Config<VirtualHost *:80>   ServerName projectenexus.test   Redirect "/" "https://projectenexus.test/"</VirtualHost>Mostra més línies

## 5️⃣ Optimització amb HTTP/2
Habilitar:
Plain Textsudo a2enmod http2Mostra més línies
Afegir a VirtualHost 443:
Apache ConfigProtocols h2 http/1.1Mostra més línies
Verificar:
Shellcurl -I --http2 https://projectenexus.testMostra més línies

## 📄 Què Cal Lliurar

Memòria tècnica completa.
Explicacions clares per a no tècnics.
Captures de verificació.
Proves de funcionament (curl, DevTools).
Estructura final del servidor.


## 📚 Material
UD5.AA2 — El servidor Apache (Moodle Serveis de Xarxa)

## 🏁 Tancament
Aquesta pràctica et prepara per desplegar un servidor Apache professional, segur, multidomini i optimitzat, tal com exigeixen els entorns empresarials moderns.
