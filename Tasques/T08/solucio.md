# T08: Vigilància i auditoria de sistemes

## 1. Monitorització de Recursos

Per obrir l'administrador de tasques, podem fer click dret a la barra de tasques i obrir-lo, o podem fer la seguent comanda: **CNTRL+SHIFT+ESC**

![Captura 1](/Tasques/T08/img/i1.png)

L'administrador de tasques ens mostra les aplicacions en execució actuals. Ens indica el consum de CPU i RAM en les barres laterals de la dreta.

![Captura 2](/Tasques/T08/img/i2.png)

Si anem a details podem explorar la llista completa de processos amb informació extra.

![Captura 3](/Tasques/T08/img/i3.png)

També tenim informació del hardware. Com per exemple, CPU, RAM, xarxa...

![Captura 4](/Tasques/T08/img/i4.png)

Podem veure els serveis actuals i el seu estat.

![Captura 5](/Tasques/T08/img/i5.png)

**El servidor està saturat o treballa sense estrès?**

El consum dels processos en els diferents components de hardware és baixa. La CPU i la Memòria no estàn consumint molts recursos. El servidor treballa sense estrès.

## 2. Configuració d'Auditoria de Seguretat

Per activar l'auditori de seguretat, anem al gestor de GPOs, anem a editarles, i seguim la seguent ruta: Computer configuration -> policies -> windows settings -> security settings -> local policies -> audit policy.

![Captura 6](/Tasques/T08/img/i6.png)

Entrem a audit object access properties i activem les opcions disponibles.

![Captura 7](/Tasques/T08/img/i7.png)

## 3. Simulació d'Incidents (Hacking Ètic)

Per comprovar si funciona, iniciarem sessió amb una contrasenya errónea, i veurem què passa. Repetim el mateix 3 o 4 vegades.

![Captura 8](/Tasques/T08/img/i8.png)

## 4. Anàlisi Forense (Event Viewer)

Obrim l'Event Viewer. 

![Captura 9](/Tasques/T08/img/i9.png)

Per això, haurem d'anar a editar les GPO i activarem l'audit file system i l'audit handle manipulation 

![Captura 10](/Tasques/T08/img/i10.png)
![Captura 11](/Tasques/T08/img/i11.png)

Habilitem l'auditoria en els usuaris.

![Captura 12](/Tasques/T08/img/i12.png)
![Captura 13](/Tasques/T08/img/i13.png)

Ara si anem al visor d'events i a l'apartat de seguretat, aquest programa ens permet veure dades de l'usuari o especificacions com a quina hora ha intentat l'inici de sessió i l'hora que ho ha fet.

![Captura 14](/Tasques/T08/img/i14.png)

ID: 4701





