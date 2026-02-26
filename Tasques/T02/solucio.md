# T02: Missió Apache: Desplegament Multidomini i segur

## 1. Instal·lació i Configuració Base

Fem la configuració inicial.

![Captura 1](T02/img/i1.png)

Per instal·lar el servei Apache, farem la seguent comanda:

```
apt install apache2
```

![Captura 2](T02/img/i2.png)

Podem comprovar que es crea un usuari i grup www-data.

```
grep www-data /etc/passwd
```

![Captura 3](T02/img/i3.png)

Creem les carpetes de cada domini dins la carpeta /var/www/

```
mkdir /var/www/site1
mkdir /var/www/site2
```

També, s'hauria d'haver creat un arxiu html.

![Captura 4](T02/img/i4.png)

---

## 2. Desplegament de VirtualHosts (Multidomini)

Fem una còpia del arxiu 000-default.conf per tenir els nostres propis dos arxius de configuració del site.

```
cp 000-default.conf site1.conf
cp 000-default.conf site2.conf
```

![Captura 5](T02/img/i5.png)

Obrim en mode edició els dos arxius de configuració (site1 i site2) i modifiquem el nom del servidor per posar el nostre.

````
sudo nano site1.conf
sudo nano site2.conf
````

![Captura 6](T02/img/i6.png)
![Captura 7](T02/img/i7.png)

Per aplicar els canvis, fem:

```
a2ensite site1.conf
a2ensite site2.conf
```

Després, reiniciem el servei.

```
systemctl reload apache2
```

Modifiquem l'arxiu de hosts i anyadim les dos línies mostrades a continuació:

```
sudo nano /etc/hosts
```

![Captura 8](T02/img/i8.png)

---

## 3. Personalització d'Errors

