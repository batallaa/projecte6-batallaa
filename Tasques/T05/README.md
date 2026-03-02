# 🕵️‍♂️ T05: Top Secret — Protegint els Secrets

## 📝 Breu Descripció

### 🔐 Introducció
Projecte Nexus gestiona dades molt sensibles:  
- informació personal d’alumnes  
- exàmens oficials  
- certificats acadèmics  

La direcció vol una demostració clara de com garantiu els **tres pilars de la seguretat**:  
**Confidencialitat**, **Integritat** i **Autenticitat**.

Aquesta pràctica està dividida en dues tasques centrades en:
1. 🔒 **Protecció de dades en repòs (xifratge)**  
2. 🧬 **Verificació d'integritat (funcions hash)**

---

# 🧩 Tasca 1: Protecció de dades en repòs (Xifratge Simètric)

Els caps de departament volen transportar exàmens en USB sense risc de filtracions.  
Per això creareu un **contenidor xifrat** amb VeraCrypt.

### 🎯 Requisits
- Crear un volum de **100 MB**
- Algoritme de xifratge **AES‑256**
- Contrasenya robusta 🔑
- Dins del volum, crear el fitxer:  
  **EXAMEN_FINAL_SEGURETAT.txt**
- Comprovar que sense muntar el volum ➜ **el fitxer és inaccessible**

### 📸 Evidències a incloure (en l’informe final)
1. Captura de la configuració del volum (algorisme AES‑256)  
2. Captura de la unitat muntada amb l’examen a dins  
3. Captures mostrant el procés d’accés  
4. Captura demostrant que el volum no muntat és inaccessible

---

# 🧩 Tasca 2: Verificació d'Integritat (Hashing)

Nexus vol assegurar-se que cap alumne o atacant modifica fitxers del servidor.  
Cal demostrar com un **petit canvi** en un document modifica completament la seva empremta digital (hash).

### 🛠️ Procediment
1. Crear un fitxer:  
   **nota_final_curs.txt**  
   Contingut:  
   `"L'alumne ha aprovat amb un 5"`
2. Calcular el hash **SHA‑256**  
3. Modificar una sola xifra → `"L'alumne ha aprovat amb un 9"`
4. Tornar a calcular el hash  
5. Comparar ➜ els hashos seran completament diferents

### 📸 Evidències a incloure
- Captura mostrant el **hash original**
- Captura mostrant el **hash modificat**
- Han de ser diferents per demostrar manipulació

---

# 📤 Què cal lliurar (Informe Markdown)

L’informe final ha d’incloure:

---

## 📘 1. Justificació Teòrica (màx. 10 línies)

Explicació clara per al client de la diferència entre:

### 🔒 Xifratge
- Serveix per **ocultar la informació**
- Es pot recuperar amb la **contrasenya/clau**
- S'usa per protegir dades en repòs o en trànsit

### 🧬 Hashing
- Genera una **empremta digital** única
- *No es pot desxifrar* (és un procés unidireccional)
- S’utilitza per detectar canvis i garantir **integritat**

---

## 🖼️ 2. Evidències de la Tasca 1 (Xifratge)

Incloure:
- ✔️ Captura del volum (100MB, AES‑256)  
- ✔️ Captura de la unitat muntada  
- ✔️ Fitxer EXAMEN_FINAL_SEGURETAT.txt visible  
- ✔️ Captura demostrant inaccesibilitat quan el volum està desmuntat  

---

## 🖼️ 3. Evidències de la Tasca 2 (Hashing)

Incloure:
- ✔️ Hash SHA‑256 del fitxer original  
- ✔️ Hash SHA‑256 del fitxer modificat  
- ✔️ Comparació (han de ser totalment diferents)

---

## 🧾 4. Conclusió Final

Redactar una recomanació per Nexus:

### 🛡️ Protegir dades sensibles
- Xifrar dispositius extraïbles (USB, discos externs)
- Utilitzar contrasenyes robustes i úniques
- Guardar les contrasenyes de manera segura (gestors de contrasenyes)

### 🧬 Garantir la integritat documental
- Verificar hash de documents crítics (actes, contractes, exàmens)
- Publicar hash oficials dels fitxers compartits amb alumnes

---

# 📚 Material de Suport

🔗 **Manual VeraCrypt (Oficial):**  
https://veracrypt.io/en/Beginner's%20Tutorial.html  

📘 **Materials de Seguretat Informàtica — RA3** (Moodle)

