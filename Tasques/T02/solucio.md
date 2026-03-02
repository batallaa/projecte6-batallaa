# T02: Missió Apache: Desplegament Multidomini i segur

## 1. Instal·lació i Configuració Base

Fem la configuració inicial.

![Captura 1](T02/img/i1.png)

Comprovem l'ip

```
ip a
```

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

![Ctura 5](T02/img/i5.png)

Comprovem si la carpeta /var/www té permisos de lectura per tots els usuaris, excepte root.

```
ls -l /var
```

## 2. Desplegament de VirtualHosts

