# 🏭🔐 T07: TransLògic — Administració Avançada i Seguretat Corporativa

## 📝 Breu Descripció

### 🌐 Introducció  
Tot i el volum de feina amb Projecte Nexus, TransLògic S.A. necessita que completeu la fase final del seu projecte basat en **Directori Actiu**.  
L’empresa demana millores al seu entorn corporatiu basades en:

- 🔐 Seguretat de contrasenyes  
- 🧭 Mobilitat d’usuaris  
- 📦 Desplegament automàtic de programari  
- 🗂️ Seguretat de dades  
- 👨‍🔧 Delegació de funcions per a un helpdesk sense privilegis totals  

Cal documentar **tots els passos amb captures i explicacions tècniques**.

---

# 🧩 0. Redisseny d’Estructura d’OU (abans de començar)

Repasseu la vostra estructura inicial i considereu simplificacions com:

- **OU TransLogic**  
  - OU Gerencia  
  - OU Gestio  
  - OU Magatzem  
  - OU Equipaments  
  - OU Perfils  
  - OU Helpdesk

L’objectiu és:  
➡️ Aplicar GPO de manera ordenada  
➡️ Delegar permisos fàcilment  
➡️ Gestionar usuaris i equips sense confusió

---

# 🔐 1. Polítiques de Seguretat i Contrasenyes

## 🔸 1.1 Política Global (Default Domain Policy)
Aplica a TOT EL DOMINI:

- Contrasenya mínima: **8 caràcters**
- Es modifica a:  
  **Default Domain Policy → Password Policy**

## 🔸 1.2 Política per a Gerència (GPO específica)
A l’OU *Gerencia*:

- Mínim **18 caràcters**
- Caducitat cada **28 dies**
- ❌ Complexitat deshabilitada
- La GPO només afecta al grup **gerencia**

## 🔸 1.3 Bonus — 3a GPO proposada (Seguretat en logística)
### Proposta recomanada:  
🔒 **Bloqueig automàtic de sessió als usuaris de Magatzem**  
- Justificació: en un entorn logístic els equips sovint queden desatesos, i això pot provocar:
  - Accés no autoritzat  
  - Manipulació de comandes  
  - Pèrdua de dades  

Es configura un bloqueig automàtic de pantalla als 3–5 minuts.

Altres opcions possibles:  
- Fons corporatiu  
- Prohibició d’instal·lar programari extern  
- Limpieza del perfil temporal  

---

# 📦 2. Desplegament Automatitzat de Programari

## 🔸 2.1 Departament de Gestió → Instal·lació Assignada (7zip)
Per al grup **gestio**:

1. Col·loqueu el `.msi` de 7zip a una carpeta compartida.
2. Creeu una GPO → *Assign Software*
3. S’instal·la automàticament al reiniciar.

## 🔸 2.2 Departament de Gerència → Desplegament Publicat (Firefox)
Per al grup **gerencia**:

1. Col·loqueu el `.msi` de Firefox a la carpeta compartida.
2. Creeu una GPO → *Publish Software*
3. S’instal·la des de:
   ```
   Tauler de Control → Add/Remove Programs → Install a program from the network
   ```

---

## ❓ Pregunta del Client  
**“Com podem crear els nostres propis fitxers .msi si una aplicació només ve amb .exe?”**

### ✔️ Resposta breu:
Cal utilitzar eines de *reempacatge* (*repackaging*), com:

- **Advanced Installer**
- **EMCO MSI Package Builder**
- **WiX Toolset**
- **MSIX Packaging Tool (Microsoft)**

Aquestes eines capturen els canvis del sistema realitzats per l’instal·lador `.exe` i generen un **paquet .msi** gestionable pel Directori Actiu.

---

# 🧭 3. Mobilitat d’Usuaris (Perfils Mòbils)

Els usuaris de **gestio** utilitzen diversos equips.

## Procediment:
1. Crear una carpeta compartida al servidor:
   ```
   \\server\perfils
   ```
2. Donar permisos:
   - Usuari → *Create folder / Append Data*
   - Admins → Full Control
3. A l’usuari del grup **gestio**, configurar:
   ```
   Profile path: \\server\perfils\%username%
   ```
4. Crear un nou usuari de prova i iniciar sessió.
5. Verificar que s'ha generat automàticament:
   ```
   \\server\perfils\NOM_USUARI
   ```

---

# 🗄️ 4. Redirecció de Carpetes (Documents)

Per evitar pèrdua de dades:

1. Crear GPO a nivell de domini.
2. Configurar:
   ```
   User Configuration → Policies → Windows Settings → Folder Redirection → Documents
   ```
3. Redirigir a:
   ```
   \\server\home\%username%\documents
   ```
4. Prova:
   - Guardar un fitxer a Documents en el client  
   - Comprovar que apareix al servidor

---

# 🧑‍💻 5. Delegació de Funcions (Helpdesk)

La direcció vol crear un auxiliar que pugui:

- 🔁 Reiniciar contrasenyes
- 👥 Modificar pertinença a grups

però **no**:

- ❌ Crear usuaris nous
- ❌ Eliminar comptes
- ❌ Modificar GPO

## Procediment:
1. Crear usuari: **adminOU** a l’OU Usuaris.
2. Botó dret sobre l’OU principal (TransLogic):  
   → *Delegate Control*
3. Assignar permisos:
   - Reset Password  
   - Read all user information  
   - Modify group membership  
4. Provar des del client:
   - ✔️ Canviar contrasenya d’un usuari  
   - ✔️ Afegir-lo a un grup  
   - ❌ Intentar crear usuari → *Permís denegat*

Aquestes captures han d'aparèixer a l’informe.

---

# 📤 Què cal lliurar

## 📝 Informe tècnic (Markdown)
Incloure:

### ✔️ Estructura d’OU revisada i justificació  
### ✔️ Captures comentades:
- GPO creades  
- Resultats de perfils mòbils  
- Redirecció de carpetes aplicada  
- Delegació de permisos  
- Instal·lació automàtica i publicada de programari  
- Logs d’auditoria si aplica  

### ✔️ Justificació de la 3a GPO  
### ✔️ Resposta tècnica sobre creació de MSI  
### ✔️ Proves de funcionament:
- `gpresult /r` o `gpresult /h informe.html`
- Carpeta "Documents" redirigida
- Perfil mòbil generat
- Error al crear usuari amb adminOU

---

# 📚 Material de Suport

📘 **UD7 – SOX: AA1, AA2 i AA4 (Moodle)**  
🪟 Documentació oficial de Microsoft – Group Policy, AD DS, Folder Redirection  
📦 Guia de paquets MSI – Advanced Installer, EMCO, MSIX Packaging Tool
