# 🏢🔐 T06: Projecte Nexus — Implantació de PKI i Signatura Digital Corporativa

## 📝 Breu Descripció

### 🌐 Introducció
Després de protegir la confidencialitat de les dades, Projecte Nexus ha detectat una nova necessitat crítica: garantir **integritat**, **autenticitat** i **no repudi** dels seus documents interns i contractes.  
Fins ara signaven en paper, però ara volen adoptar un sistema intern de **certificats digitals corporatius** per signar documents PDF oficials.

Aquesta tasca consisteix en crear una **Prova de Concepte (PoC)** per demostrar que es pot desplegar una infraestructura PKI pròpia dins l’empresa Nexus.

---

# 🧩 Descripció de l’Activitat

L’activitat es divideix en **tres fases principals** i s’ha de treballar en parelles:

- 👨‍💼 **Administrador de Nexus** → Windows Server 2025  
- 👨‍💻 **Treballador de Nexus** → Client Windows

---

# 🛠️ Fase 1: Desplegament de la CA a Windows Server 2025 (Servidor)

L’administrador ha de:

1. Instal·lar el rol **AD CS – Active Directory Certificate Services**
2. Configurar una **Autoritat de Certificació (CA)** corporativa
3. Permetre que els empleats sol·licitin certificats via web a:
   ```
   http://SERVERNAME/certsrv
   ```
4. Validar i emetre els certificats sol·licitats  
5. Verificar a `certsrv.msc` que apareixen emesos

---

# 🛠️ Fase 2: Sol·licitud i Emissió de Certificats via Web (Client)

El treballador de Nexus ha de:

1. Obrir el navegador i accedir a:
   ```
   http://SERVERNAME/certsrv
   ```
2. Seleccionar **Request a certificate**
3. Sol·licitar un certificat d’usuari
4. Descarregar-lo i instal·lar-lo al seu equip
5. Verificar-lo a:
   ```
   certmgr.msc
   ```
   dins *Personal → Certificates*

---

# 🛠️ Fase 3: Signatura Digital i Verificació (Acrobat Reader)

Amb el certificat personal instal·lat:

1. Obrir un PDF oficial de Nexus
2. Fer **Signatura Digital** des d’Acrobat Reader
3. Escollir el certificat corporatiu
4. Guardar el document ja signat
5. Verificar:
   - Validació correcta
   - Cadena de confiança fins a la CA perquè el client ha importat el certificat arrel

---

# 📤 Què cal lliurar al repositori

A la carpeta d’aquesta tasca heu de lliurar:

## 📘 **1. Memòria tècnica (memoria.md)**

Incloure:

### 📸 Captures del servidor
- Instal·lació del rol **AD CS**  
- Configuració de la CA  
- Consola `certsrv.msc` mostrant certificats emesos

### 📸 Captures del client
- Portal `certsrv` obert al navegador  
- Instal·lació del certificat a `certmgr.msc`  
- Certificat personal visible

### 🧠 Explicació: Clau Pública vs Clau Privada

Redactar un text curt explicant:

- 🔑 **Clau privada**:  
  - Es guarda al dispositiu de l’usuari  
  - Serveix per signar digitalment  
  - No s’ha de compartir mai  

- 🌍 **Clau pública**:  
  - La distribueix la CA  
  - Serveix perquè altres puguin verificar signatures  
  - No permet signar ni suplantar l’usuari  

---

## 🖊️ **2. Evidència de la Signatura**

Incloure:

- ✔️ El PDF oficial de Nexus **signat digitalment** per un membre del grup.

---

## 🏅 **3. Certificat Arrel de la CA**

Incloure:

- El fitxer `.cer` de la vostra **Autoritat de Certificació** (clau pública)

---

# 📚 Material de Suport

📘 **Materials de l’assignatura Seguretat Informàtica — RA3**  
📎 Guia de l’activitat proporcionada pel professorat  
🔗 Conceptes bàsics de PKI i CA (AD CS): Microsoft Docs  
🔗 Acrobat Reader — Digital ID & Signatures (Adobe)
