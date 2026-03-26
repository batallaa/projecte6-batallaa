# P02: Presentació de la proposta al client

**SMX2B**  
Nezar Mghari, David Ballesteros i Biel Batalla  
25/03/2026  

![Logo](/Productes/P02/img/logo.png)

---

## Índex

1. Context i necessitats del client  
2. T04 — Duel de titans: Apache vs Nginx  
   - 2.1 Comparativa tècnica  
   - 2.2 Experiència real  
   - 2.3 Mètriques i dades  
   - 2.4 Decisió final (servidor web)  
3. T11 — Comparativa Moodle vs Canvas LMS  
   - 3.1 Comparativa funcional i tècnica  
   - 3.2 Experiència real  
   - 3.3 Mètriques i criteris  
   - 3.4 Decisió final (LMS)  
4. Integració de la solució  
5. Viabilitat tècnica i econòmica  
6. Qualitat, manteniment i sostenibilitat  
7. Conclusió i proposta final  

---

## 1. Context i necessitats del client

El Projecte Nexus neix amb la voluntat de crear una plataforma pròpia d’E-learning enfocada a la formació de tècnics informàtics.

L’objectiu no és només oferir cursos, sinó construir un entorn complet de formació digital que permeti gestionar continguts, alumnes i professors de manera eficient.

El client es troba davant d’una situació habitual en moltes petites i mitjanes empreses: vol digitalitzar els seus serveis, però necessita fer-ho amb recursos limitats i amb una infraestructura sostenible a llarg termini.

### Necessitats principals

- Garantir bon rendiment del sistema, fins i tot amb recursos limitats  
- Controlar costos inicials i de manteniment  
- Disposar d’un sistema fàcil de mantenir  
- Apostar per una solució sostenible  
- Tenir flexibilitat per créixer  

---

## 2. T04 — Duel de titans: Apache vs Nginx

### 2.1 Comparativa tècnica

| Apartat              | Apache                     | Nginx                          |
|---------------------|----------------------------|--------------------------------|
| Instal·lació        | Fàcil                      | Fàcil                          |
| Configuració        | Flexible                   | Centralitzada i simple         |
| Rendiment           | Bo en webs petites         | Molt alt en alta concurrència  |
| Consum de recursos  | Més alt                    | Molt baix i eficient           |
| Escalabilitat       | Limitada                   | Molt alta                      |
| Manteniment         | Més complex                | Més senzill                    |

**Apache**  
- Molt consolidat  
- Gran comunitat  
- Alta flexibilitat (.htaccess)  

**Nginx**  
- Més modern  
- Alt rendiment  
- Model eficient per gestionar connexions  

---

### 2.2 Experiència real

**Apache**
- Instal·lació i configuració senzilles  
- Bona documentació  
- Flexible i tolerant a errors  

**Nginx**
- Configuració més exigent  
- Problemes amb rutes i permisos  
- Menys tolerant a errors  

Conclusió:  
Apache és més accessible, però Nginx ofereix millor rendiment.

---

### 2.3 Mètriques i dades

- Apache consumeix més RAM  
- Nginx manté consum estable  
- Nginx té millor temps de resposta  
- Nginx requereix més configuració  

---

### 2.4 Decisió final (servidor web)

S’escull **Nginx** per:

- Menor consum de recursos  
- Millor rendiment  
- Alta escalabilitat  
- Major sostenibilitat  

---

## 3. T11 — Comparativa Moodle vs Canvas LMS

### 3.1 Comparativa funcional i tècnica

**Moodle**
- Codi obert  
- Molt configurable  
- Requereix més coneixement tècnic  

**Canvas**
- Interfície moderna  
- Fàcil d’utilitzar  
- Pot implicar costos i dependències  

---

### 3.2 Experiència real

**Moodle**
- Instal·lació més complexa  
- Gestió menys intuïtiva  

**Canvas**
- Fàcil des del primer moment  
- Navegació clara  
- Dependència de serveis externs  

---

### 3.3 Mètriques i criteris

- Moodle: més temps d’instal·lació  
- Canvas: més fàcil d’utilitzar  
- Moodle: més control i personalització  
- Canvas: possibles costos  

---

### 3.4 Decisió final (LMS)

S’escull **Moodle** perquè:

- És gratuït  
- Permet control total  
- S’adapta a infraestructura pròpia  
- Dona independència tecnològica  

---

## 4. Integració de la solució

**Arquitectura: Nginx + Moodle**

Funcionament:
1. L’usuari accedeix a la plataforma  
2. Nginx rep i gestiona la petició  
3. Moodle gestiona el contingut educatiu  

### Avantatges

- Separació de funcions  
- Sistema eficient  
- Escalable  
- Organitzat  

---

## 5. Viabilitat tècnica i econòmica

### Viabilitat tècnica

- Tecnologies estables  
- No requereix infraestructura complexa  
- Gestionable per un tècnic mitjà  

### Viabilitat econòmica

**Costos**
- Configuració inicial  
- VPS mensual  
- Manteniment  

**Avantatges**
- Sense llicències  
- Flexible  
- Sense maquinari  

Ideal per una PIME  

---

## 6. Qualitat, manteniment i sostenibilitat

### Qualitat

- Sistema estable  
- Basat en tecnologies fiables  

### Manteniment

- Actualitzacions  
- Revisió del servidor  
- Còpies de seguretat  

### Sostenibilitat

- Nginx redueix consum  
- VPS més eficient  
- Menys impacte energètic  

---

## 7. Conclusió i proposta final

### Proposta

**Nginx + Moodle + VPS**

### Per què?

- Bon rendiment  
- Econòmica  
- Escalable  
- Sostenible  

Solució equilibrada i aplicable en un entorn real.
