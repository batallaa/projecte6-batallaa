# T05: Top Secret, protegint els secrets

## Tasca 1: Protecció de dades en repòs (Xifratge Simètric)

Creem un volum VHD per simular un pendrive.

![Captura 1](/Tasques/T05/img/i1.png)
![Captura 2](/Tasques/T05/img/i2.png)

Instal·lem [veracrypt](https://veracrypt.io/en/Downloads.html)

Un cop dins, creem un nou volum.

![Captura 3](/Tasques/T05/img/i3.png)

Elegim la segona opció ja que volem xifrar una partició del nostre propi ordinador.

![Captura 4](/Tasques/T05/img/i4.png)

Escollim la versió comúna.

![Captura 5](/Tasques/T05/img/i5.png)

Escollim que volem xifrar el nostre volum VHD.

![Captura 6](/Tasques/T05/img/i6.png)

Escollim conservar les dades si tenim les nostres dades dins del pendrive.

![Captura 7](/Tasques/T05/img/i7.png)

Elegim el seguent sistema de xifrat:

![Captura 8](/Tasques/T05/img/i8.png)

Ara introduïm una contrasenya complexa per al pendrive. Podem utilitzar una generada per ia.

![Captura 9](/Tasques/T05/img/i9.png)

Esperem en aquest pas i continuem.

![Captura 10](/Tasques/T05/img/i10.png)

Deixem el mode d'esborrar per defecte.

![Captura 11](/Tasques/T05/img/i11.png)

Xifrem el volum.

![Captura 12](/Tasques/T05/img/i12.png)

Creem un fitxer amb preguntes. Després, montem el pen al veracrypt on posa "seleccionar dispositivo".

![Captura 13](/Tasques/T05/img/i13.png)

Ens demanarà la contrasenya.

![Captura 14](/Tasques/T05/img/i14.png)

Un cop dins del disc afegim les preguntes.

![Captura 15](/Tasques/T05/img/i15.png)

Per demostrar que no podem accedir al pen sense contrasenya, anem a veracrypt i pressionem el botó que diu "Desmontar todo".

![Captura 16](/Tasques/T05/img/i16.png)

I veiem com no deixa.

![Captura 17](/Tasques/T05/img/i17.png)

## Tasca 2: Verificació d'Integritat (Hashing)

Creem un document de text que es digui "nota_final_curs.txt" amb el text: "L'alumne ha aprovat amb un 5"

![Captura 18](/Tasques/T05/img/i18.png)

Amb la seguent comanda comprovem si el fitxer és el mateix:

```bash
Certutil -hashfile "C:\Users\marcm\Desktop\Nueva carpeta\nota_final_curs.txt"
```

![Captura 20](/Tasques/T05/img/i20.png)

Modifiquem el fitxer

![Captura 19](/Tasques/T05/img/i19.png)

Ara si tornem a fer la comanda, el hash haurà canviat.

![Captura 21](/Tasques/T05/img/i21.png)
