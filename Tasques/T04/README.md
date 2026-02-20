# ⚔️ T04: Duel de Titans — Apache vs Nginx

## 📝 Breu descripció

### 🌐 Introducció
Fins ara heu configurat dos servidors web diferents:

- 🧱 **Apache** — robust, modular i molt utilitzat.
- ⚡ **Nginx** — lleuger, orientat a esdeveniments i altament escalable.

Tots dos serveixen el mateix contingut, però... **es comporten igual sota pressió?**  
En aquesta pràctica adoptareu el rol d’**Auditors de Sistemes** i dureu a terme proves d’estrès (*Benchmarking*) per comparar el rendiment real d’ambdós servidors.

L'objectiu és determinar quin servidor pot oferir millors prestacions al client durant la campanya de llançament de Projecte Nexus.

---

## 🧪 Descripció de l'activitat

Cada alumne haurà de tenir:

- La màquina virtual amb **Apache i Nginx instal·lats**.
- Un entorn web més professional (imatges, estils, disseny corporatiu).  
  👉 Podeu generar-lo amb IA.
- Al client Zorin OS, cal instal·lar:

```
sudo apt install apache2-utils
```

Un de vosaltres provarà **Apache**, l’altre **Nginx**.  
Després intercanviareu resultats.

---

## 🧵 Proves a realitzar

---

# 1️⃣ Prova de càrrega lleugera

🎯 Objectiu: simular trànsit normal  
👥 10 usuaris concurrents  
📨 1000 peticions totals

### 🔧 Sintaxi de la comanda

```
ab -n 1000 -c 10 http://[IP_SERVIDOR]/
```

### 📊 Dades a recollir

- **Time taken for tests** (temps total)
- **Transfer Rate**
- **Requests per second (RPS)** — *com més alt, millor*
- **Time per request (mean)** — *com més baix, millor*
- **Completed requests**
- **Failed requests**

---

# 2️⃣ Prova d’estrès 🧨

🎯 Objectiu: portar el servidor al límit  
👥 100 usuaris concurrents  
📨 10.000 peticions

### 🔧 Comanda

```
ab -n 10000 -c 100 http://[IP_SERVIDOR]/
```

⚠️ *Si el servidor falla, dóna error o retorna “Connection timed out”, ho heu d’anotar. Això també és un resultat important.*

---

## 📤 Què cal lliurar

Heu de crear una **taula comparativa** amb els resultats obtinguts per cada servidor i cada prova:

### 📊 Taula de resultats

| **Mètrica** | **Apache — Prova lleugera** | **Nginx — Prova lleugera** | **Apache — Prova d’estrès** | **Nginx — Prova d’estrès** |
|-------------|------------------------------|------------------------------|------------------------------|------------------------------|
| Time taken for tests | | | | |
| Transfer rate | | | | |
| Requests per second (RPS) | | | | |
| Time per request | | | | |
| Completed requests | | | | |
| Failed requests | | | | |

---

## 📚 Material de suport

🔗 J.D. Muñoz – **El comando ab (Apache Benchmark)**  
https://serviciosgs.readthedocs.io/es/latest/rendimiento/ab.html
