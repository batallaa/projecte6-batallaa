# 🛡️📊 T08: Vigilància i Auditoria de Sistemes

## 📝 Breu descripció

### 🔍 Introducció
TransLògic S.A. vol garantir la integritat de les dades i detectar possibles intrusions o activitats sospitoses.  
Com a consultors, heu d’implantar mecanismes de **monitorització**, **auditoria** i **anàlisi forense** per convertir el servidor en un entorn auditables com una “caixa negra”.

---

# 🧩 1. Monitorització de Recursos

## 🎯 Objectiu
Verificar si el servidor està treballant correctament i si suportarà la càrrega del dia a dia.

## 🖥️ Accions
- Accedir al **Monitor de Rendiment**, **Gestor de Tasques** o **Performance Monitor**.
- Fer captura de:
  - Ús de CPU (%)  
  - Memòria RAM disponible

## 🧠 Interpretació
A l’informe heu d’explicar:
- Si el servidor està 🔥 **saturat** (CPU > 80%, RAM baixa)
- O si treballa 🟢 **sense estrès**

---

# 🧩 2. Configuració d’Auditoria de Seguretat

## 🎯 Objectiu
Detectar intents d’intrusió i atacs de força bruta.

## 🛠️ Accions
Activar l’auditoria d’inici de sessió mitjançant GPO:

Ruta:  
```
Local Security Policy
→ Security Settings
→ Local Policies
→ Audit Policy
→ Audit logon events
```

Activar:
- ✔️ Success (èxits)
- ✔️ Failure (fracassos)

Cal aportar:
- 📸 Captura de la GPO o política local configurada

---

# 🧩 3. Simulació d’Incidents (Hacking Ètic)

## 🎯 Objectiu
Generar esdeveniments de seguretat per validar l’auditoria.

## 🔐 Accions
1. Tancar sessió del servidor.
2. Fer **3 o 4 intents fallits** d’inici de sessió amb un usuari real (ex: magatzem).
3. Finalment, iniciar sessió correctament amb l’administrador.

Això generarà:
- Errors de tipus *Logon Failed*
- Inici de sessió correcte final

---

# 🧩 4. Anàlisi Forense (Event Viewer)

## 🎯 Objectiu
Demostrar que l’auditoria funciona i identificar intrusions.

## 🛠️ Accions
1. Obrir:
   ```
   Event Viewer → Windows Logs → Security
   ```
2. Buscar els esdeveniments de:
   - ❌ intents fallits d’inici de sessió
   - ✔️ inici de sessió correcte
3. Obrir un esdeveniment i mostrar:
   - Usuari que ha fallat
   - Hora exacta
   - Codi d’error
   - IP d’origen (si apareix)

## 🔍 Tasca d’investigació
Indicar quin és l’**Event ID** d’un inici de sessió fallit.

### ✔️ Resposta:
**Event ID 4625** → *Failed logon attempt*  
(A Windows Server modern — 2012, 2016, 2019, 2022, 2025.)

---

# 📤 Què cal lliurar (Informe d’Auditoria)

## 1️⃣ Captura de recursos del sistema
- CPU / RAM
- Interpretació del seu estat

## 2️⃣ Captura de la política d’auditoria
- Audit logon events → Success + Failure

## 3️⃣ Evidència forense del Visor d’Esdeveniments
- Captura del Security Log amb els errors 4625
- Detalls d’un esdeveniment obert (usuari, hora, etc.)

## 4️⃣ Resposta tècnica
**Event ID dels intents d’inici de sessió fallits:**  
➡️ **4625**

---

# 📚 Material de suport
- 0224 SOX – UD7: AA3 (Moodle)
- Documentació oficial de Windows Event Logging  
- Windows Security Audit Policy
