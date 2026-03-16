# T07: TransLògic: Administració Avançada i Seguretat Corporativa

## 1. Polítiques de Seguretat i Contrasenyes (Seguretat Corporativa)

### 1.1 Directives de password

Per poder editar les GPO, anem a "Tools" i a Group Policy Management.

![Captura 1](T07/img/i1.png)

Per editar després les polítiques de les contrasenyes, entrem al editor de les GPO, despleguem Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Account Policies -> Password Policy.

![Captura 2](T07/img/i2.png)

Entrem a la configuració de password i habilitem la configuració de contrasenyes.

![Captura 3](T07/img/i3.png)

Definim un mínim de caràcters per la contrasenya dels usuaris. En el meu cas serà de 8.

![Captura 4](T07/img/i4.png)

Podem canviar configuracions varies de les contrasenyes, com els dies que es recorda la contrasenya, el temps màxim perquè la contrasenya es canvïi o el mínim de canvi de contrasenya.

![Captura 5](T07/img/i5.png)

### 1.2 Administradors locals

Movem les plantilles d'usuaris del nostre domini a la OU de gerencia. 

![Captura 6](T07/img/i6.png)

Creem una nova ou que s'anomena BCN. Dins d'aquesta Crearem una altre anomenada Computers i aplicarem una GPO anomenada "Contrasenyes".

![Captura 7](T07/img/i7.png)

Configurem la GPO del grup de Gerència per tal que el password caduqui cada 28 dies i tingui una allargada mínima de 18 caràcters. No activem complexitat.

![Captura 8](T07/img/i8.png)

## 2. Desplegament Automatitzat de Programari

Per fer la instal·lació desatesa de programes crearem una carpeta compartida on donarem permisos per llegir als usuaris.

![Captura 14](T07/img/i14.png)

### 2.1 Departament de Gestió (7zip)

Creem una carpeta on descarregarem el programari per la gestió de factures. Per això dins del nostre disc "DATA" crearem una carpeta anomenada "Programari" i la compartirem per xarxa.

![Captura 9](T07/img/i9.png)

Despleguem el programari 7zip en la nostra GPO de Gestió.

![Captura 10](T07/img/i10.png)

Seleccionem la opció avançada per configurar les opcions a desplegar el programari. 

![Captura 11](T07/img/i11.png)

A Deployment, seleccionem del tipus assigned. A les opcions marquem l'última i maximitzem les opcions d'interfaç.

### 2.2 Departament de Gerència (Firefox)

Creem una nova GPO anomenada Firefox per el departament de gerència. Afegirem el Firefox en el software de la GPO.

![Captura 12](T07/img/i12.png)

Al afegirla, indicarem que volem configurar-lo de forma avançada i posarem tipus de deployment published, deixem marcada la primera opció i maximitzarem les opcions d'interfaç.

![Captura 13](T07/img/i13.png)

Comprovem a la màquina client que Firefox està instal·lat.

![Captura 23](T07/img/i23.png)

### 2.3 Aplicar GPO a un grup

Anem a la GPO que hem creat -> security filtering i eliminem el filtratge als usuaris autenticats. 

![Captura 15](T07/img/i15.png)

Després, anem a delegation, pressionem "add" i afegim afegim "authenticated users".

![Captura 16](T07/img/i16.png)

Donem permisos perquè puguin llegir.

![Captura 17](T07/img/i17.png)

Ara. anem a "scope", anem a "add" i afegim el grup al que volem aplicar la GPO.

![Captura 18](T07/img/i18.png)

Fem el mateix amb tots els programes. Si comprovem a la màquina client, veurem com tenim el programa instal·lat.

![Captura 19](T07/img/i19.png)

### 2.4 Pregunta de Consultoria

**Com podem crear els nostres propis fitxers .msi si una aplicació només ve amb un .exe?**



## 3. Mobilitat d'Usuaris (Perfils Mòbils)

Creem una carpeta compartida amb el nom que volguem i apliquem permisos als usuaris del domini.

![Captura 20](T07/img/i20.png)

Editem la plantilla de la carpeta de profile i posem al final %USERNAME%

![Captura 21](T07/img/i21.png)

Iniciem sessió com a nou usuari i al anar a les carpetes hauríem de veure la nostra carpeta personal creada.

![Captura 22](T07/img/i22.png)

## 4. Seguretat de Dades (Redirecció de Carpetes)

Per la redirecció de carpetes, anem a "Default Domain Policy" i anem a editar.

![Captura 24](T07/img/i24.png)

Anem a la seguent ruta: User Configuration -> Windows Settings -> Folder Redirection i anem a les propietats de la carpeta Documents.

![Captura 25](T07/img/i25.png)

A les propietats, indiquem setting basic, i introduim el directori de la carpeta homes del domini.

![Captura 26](T07/img/i26.png)

Si iniciem sessió a la màquina client, podem veure la carpeta documents creada. 

![Captura 27](T07/img/i27.png)

## 5. Delegació de Funcions (Helpdesk)

