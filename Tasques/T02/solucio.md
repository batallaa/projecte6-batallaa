# T02: Missió Apache: Desplegament Multidomini i segur

## 1. Instal·lació i configuració base

Propietats de la màquina

![Captura 1](/Tasques/T02/img/i1.png)

Comprovem l’ip.

![Captura 2](/Tasques/T02/img/i2.png)

Instal·lem el servei apache2

```
sudo apt install  apache2
```

![Captura 3](/Tasques/T02/img/i3.png)

Comprovem que apache funciona correctament amb la seguent comanda:

```
systemctl status apache2
```

![Captura 4](/Tasques/T02/img/i4.png)

Comrpovem que l’usuari i www-data s’han creat:

```
grep www-data /etc/passwd
```

![Captura 5](/Tasques/T02/img/i5.png)

Comprovem si la carpeta /var/www té permisos de lectura per tots els usuaris, excepte root.

```
ls -l /var
```

![Captura 6](/Tasques/T02/img/i6.png)


## 2. Desplegament de VirtualHosts

Editem l’arxiu hosts de la màquina client i afegim els dos dominis.

```
sudo nano /etc/hosts
```

![Captura 7](/Tasques/T02/img/i7.png)

Creem els directoris a /var/www per allotjar els 2 dominis.

```
sudo mkdir /var/www/projectenexus
sudo mkdir /var/www/academia
```

![Captura 8](/Tasques/T02/img/i8.png)

Copiem l’arxiu de configuració per poder configurar els dos virtualhosts.

```
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/projectenexus.conf

sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/academia.conf
```

Després, els obrim i editem els arxius introduint el seguent:

```
sudo nano /etc/apache2/sites-available/projectenexus.conf
sudo nano /etc/apache2/sites-available/academia.conf
```

![Captura 9](/Tasques/T02/img/i9.png)
![Captura 10](/Tasques/T02/img/i10.png)

Carreguem els sites creats:

```
sudo a2ensite projectenexus.conf
sudo a2ensite academia.conf
```

![Captura 11](/Tasques/T02/img/i11.png)

Per aplicar els canvis, hem de recarregar el servei.

```
sudo systemctl reload apache2
```

![Captura 12](/Tasques/T02/img/i12.png)

Ara si provem a entrar a qualsevol de les pàgines, ens sortirà d’aquesta forma.

![Captura 13](/Tasques/T02/img/i13.png)
![Captura 14](/Tasques/T02/img/i14.png)

## 3. Personalització d'Errors

Per poder fer una pàgina d’errors personalitzada, fem el seguent:

```
sudo nano /var/www/projectenexus/404.html
sudo nano /var/www/academia/404.html
```
Allà personalitzarem el index i el missatge d'error 404. Utilitzem ssh des de la terminal de windows per a poder fer la pàgina.

**Projecte Nexus:**

![Captura 15](/Tasques/T02/img/i15.png)

**Academia:**

![Captura 16](/Tasques/T02/img/i16.png)

Si entrem a qualsevol de les dos pàgines, ens sortirà l’estructura que hem creat.

**Projecte Nexus:**

![Captura 17](/Tasques/T02/img/i17.png)

Academia:

![Captura 18](/Tasques/T02/img/i18.png)

Per personalitzar el error 404, farem una estructura en html que ens mostri l’error.

**Projecte Nexus:**

![Captura 19](/Tasques/T02/img/i19.png)

Academia:

![Captura 20](/Tasques/T02/img/i20.png)

Perquè es carregui l’arxiu creat, haurem de canviar una configuració del nostre arxiu de config.

```
sudo nano /etc/apache2/sites-available/projectenexus.conf
sudo nano /etc/apache2/sites-available/academia.conf
```

**Projecte Nexus:**

![Captura 21](/Tasques/T02/img/i21.png)

Academia:

![Captura 22](/Tasques/T02/img/i22.png)

***Resultat de missatge d’error 404:***

**Projecte Nexus:

![Captura 23](/Tasques/T02/img/i23.png)

Academia:

![Captura 24](/Tasques/T02/img/i24.png)

## 4. Seguretat i Certificats (HTTPS)

Per implementar seguretat a les nostres pàgines, copiem l’arxiu per defecte TLS a cadascún dels dos dominis.

```
sudo cp /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/projectenexus-ssl.conf

sudo cp /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/academia-ssl.conf
```

Creem les carpetes on guardarem les claus de seguretat:

```
sudo mkdir /var/www/projectenexus/cert && sudo mkdir /var/www/projectenexus/private
sudo mkdir /var/www/academia/cert && sudo mkdir /var/www/academia/private
```

Tot el seguent s’ha de fer en els dos, però a continuació només ensenyaré els pasos en projectenexus.

Utilitzem OpenSSL. El certificat ha de tenir una durada de 365 dies i una clau RSA de 2048 bits. Aquest procés d’ha d’efectuar en els dos.

```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /var/www/projectenexus/private/projectenexus.key -out /var/www/projectenexus/cert/projectenexus.crt
```

![Captura 25](/Tasques/T02/img/i25.png)

Editem l’arxiu projectenexus-ssl.conf

```
sudo nano /etc/apache2/sites-available/projectenexus-ssl.conf
```

![Captura 26](/Tasques/T02/img/i26.png)


Habilitem el protocol HTTP:

```
sudo a2enmod ssl
sudo a2ensite projectenexus-ssl.conf
sudo systemctl restart apache2
```

![Captura 27](/Tasques/T02/img/i27.png)

Configurem el servidor per qualsevol petició HTTP sigui HTTPS.

```
sudo nano /etc/apache2/sites-available/projectenexus.conf
```

![Captura 28](/Tasques/T02/img/i28.png)

Recarreguem l’apache2:

```
sudo systemctl reload apache2
```

Ara si intentem anar a www.projectenexus.test anirà per connexió segura.

![Captura 29](/Tasques/T02/img/i29.png)

Igual que amb www.academia.test

![Captura 30](/Tasques/T02/img/i30.png)

Bloquejem la carpeta private per evitar que qualsevol persona consegueixi la clau privada. Editem l’arxiu projectenexus-ssl.conf.

```
sudo nano /etc/apache2/sites-available/projectenexus-ssl.conf
```

![Captura 31](/Tasques/T02/img/i31.png)

Com veiem, quan intentem entrar no ens deixa.

![Captura 32](/Tasques/T02/img/i32.png)

A l’academia tampoc ens deixa.

![Captura 33](/Tasques/T02/img/i33.png)

## 5. Optimització amb HTTP/2

Habilitem HTTP/2:

```
sudo a2enmod http2
sudo systemctl restart apache2
```

![Captura 34](/Tasques/T02/img/i34.png)

Afegim la seguent línia a projectenexus-ssl.conf.

![Captura 35](T/Tasques/02/img/i35.png)

Recarreguem apache2.

```
sudo systemctl reload apache2
```

Comprovem que http2 funciona:

```
curl -I -k -http2 https://10.0.2.3
```

![Captura 36](/Tasques/T02/img/i36.png)
