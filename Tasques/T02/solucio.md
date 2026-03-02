# T02: Missió Apache: Desplegament Multidomini i segur

## 1. Instal·lació i configuració base

Propietats de la màquina

![Captura 1](T02/img/i1.png)

Comprovem l’ip.

![Captura 2](T02/img/i2.png)

Instal·lem el servei apache2

```
sudo apt install  apache2
```

![Captura 3](T02/img/i3.png)

Comprovem que apache funciona correctament amb la seguent comanda:

```
systemctl status apache2
```

![Captura 4](T02/img/i4.png)

Comrpovem que l’usuari i www-data s’han creat:

```
grep www-data /etc/passwd
```

![Captura 5](T02/img/i5.png)

Comprovem si la carpeta /var/www té permisos de lectura per tots els usuaris, excepte root.

```
ls -l /var
```

![Captura 6](T02/img/i6.png)


## 2. Desplegament de VirtualHosts

Editem l’arxiu hosts de la màquina client i afegim els dos dominis.

```
sudo nano /etc/hosts
```

![Captura 7](T02/img/i7.png)

Creem els directoris a /var/www per allotjar els 2 dominis.

```
sudo mkdir /var/www/projectenexus
sudo mkdir /var/www/academia
```

![Captura 8](T02/img/i8.png)

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

![Captura 9](T02/img/i9.png)


Carreguem els sites creats:

```
sudo a2ensite projectenexus.conf
sudo a2ensite academia.conf
```

![Captura 10](T02/img/i10.png)

Per aplicar els canvis, hem de recarregar el servei.

```
sudo systemctl reload apache2
```

![Captura 11](T02/img/i11.png)

Ara si provem a entrar a qualsevol de les pàgines, ens sortirà d’aquesta forma.

![Captura 12](T02/img/i12.png)
![Captura 13](T02/img/i13.png)

## 3. Personalització d'Errors

Per poder fer una pàgina d’errors personalitzada, fem el seguent:

```
sudo nano /var/www/projectenexus/404.html
sudo nano /var/www/academia/404.html
```




