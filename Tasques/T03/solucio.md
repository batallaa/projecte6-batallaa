# T03: Missió Nginx: Migració d'Alt Rendiment i Arquitectura Lleugera

## 1. Instal·lació de nginx

Especificacions de les màquines:

**Màquina servidor**

![Captura 1](/Tasques/T03/img/i1.png)

**Màquina client**

![Captura 2](/Tasques/T03/img/i2.png)

Comprovem ip del servidor:

![Captura 3](/Tasques/T03/img/i3.png)

### 1.1 Deshabilitar nginxs

Per començar amb Nginx, reutilitzarem la màquina de apache2. Per això, deshabilitem l'apache2 i instal·larem el nginx. Després, comprovem que el servei està deshabilitat.

```bash
sudo systemctl stop apache2
sudo systemctl disable apache2
```

### 1.2 Instal·lar nginx

Instal·lem el servei nginx.
 
```bash
sudo apt install nginx -y
```

![Captura 4](/Tasques/T03/img/i4.png)

### 1.3 Verificació

Verifiquem que el servei nginx funciona correctament.

```bash
sudo systemctl status nginx 
```

![Captura 5](/Tasques/T03/img/i5.png)

## 2. Server Blocks

### 2.1 Configuracions

Copiem l'arxiu default del servidor per crear configuracions noves.

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/projectenexus
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/academia
```

![Captura 6](/Tasques/T03/img/i6.png)

Ara, editem.

```bash
sudo nano /etc/nginx/sites-available/projectenexus
sudo nano /etc/nginx/sites-available/academia
```

![Captura 7](/Tasques/T03/img/i7.png)
![Captura 8](/Tasques/T03/img/i8.png)

### 2.2 Enllaços simbòlics

Creem els enllaços simbòlics per als dos llocs web.

```bash
sudo ln -s /etc/nginx/sites-available/projectenexus /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/academia /etc/nginx/sites-enabled/
```

![Captura 9](/Tasques/T03/img/i9.png)

Modifiquem l'arxiu següent per treballar amb diferents noms de domini (treiem el #)

```bash
sudo nano /etc/nginx/nginx.conf
```

![Captura 10](/Tasques/T03/img/i10.png)

Comprovem errors sintàctics:

```bash
sudo nginx -t
```

Reiniciem el servei:

```bash
sudo systemctl restart nginx
```

![Captura 11](/Tasques/T03/img/i11.png)

**Projecte Nexus**

![Captura 12](/Tasques/T03/img/i12.png)

**Academia**

![Captura 13](/Tasques/T03/img/i13.png)

## 3. Pàgina error 404

Per personalitzar la pàgina d'error, anem a la seguent ruta:

```bash
sudo nano /etc/nginx/sites-available/projectenexus
sudo nano /etc/nginx/sites-available/academia
```

![Captura 14](/Tasques/T03/img/i14.png)
![Captura 15](/Tasques/T03/img/i15.png)

Comprovem errors sintàctics:

```bash
sudo nginx -t
```

Reiniciem el servei:

```bash
sudo systemctl restart nginx
```

![Captura 16](/Tasques/T03/img/i16.png)

**Pàgina error Projectenexus:**

![Captura 17](/Tasques/T03/img/i17.png)

**Pàgina error Academia:**

![Captura 18](/Tasques/T03/img/i18.png)

## 4. SSL (HTTPS)

Copiem els arxius de configuració i els afegim .tls

```bash
cd /etc/nginx/sites-available/

sudo cp projectenexus projectenexus.tls
sudo cp academia academia.tls
```

![Captura 19](/Tasques/T03/img/i19.png)

Editem els arxius i els modifiquem:

```bash
sudo nano /etc/nginx/sites-available/projectenexus.tls
sudo nano /etc/nginx/sites-available/academia.tls
```

![Captura 20](/Tasques/T03/img/i20.png)
![Captura 21](/Tasques/T03/img/i21.png)

Creem els enllaços simbòlics per habilitar els sites:

```bash
sudo ln -s /etc/nginx/sites-available/projectenexus.tls /etc/nginx/sites-enabled/projectenexus.tls
sudo ln -s /etc/nginx/sites-available/academia.tls /etc/nginx/sites-enabled/academia.tls
``` 

![Captura 22](/Tasques/T03/img/i22.png)

Comprovem errors sintàctics:

```bash
sudo nginx -t
```

Reiniciem el servei:

```bash
sudo systemctl restart nginx
```

## 5. Protecció de carpetes
Protegim la carpeta private, anem als arxius de configuració:

```bash
sudo nano /etc/nginx/sites-available/projectenexus.tls
sudo nano /etc/nginx/sites-available/academia.tls
```

![Captura 23](/Tasques/T03/img/i23.png)
![Captura 24](/Tasques/T03/img/i24.png)

Forçem la redirecció perquè faci servir https. 

```bash
sudo nano /etc/nginx/sites-enables/projectenexus
sudo nano /etc/nginx/sites-enables/academia
```

**Projecte nexus**

![Captura 25](/Tasques/T03/img/i25.png)

**Academia**

![Captura 26](/Tasques/T03/img/i26.png)

Fem la comprovació de funcionament:

```bash
curl http://www.projectenexus.test
```

### 5.2 Optimització amb HTTP/2

Habilitem el protocol HTTP/2

Anyadim el paràmetre http2 a l'arxiu de config .tls.

```bash
sudo nano /etc/nginx/sites-enabled/projectenexus.tls
sudo nano /etc/nginx/sites-enabled/academia.tls
```

![Captura 27](/Tasques/T03/img/i27.png)

Reiniciem el servei i fem comprovacions.

```bash
curl  -I -k --http2 https://www.projectenexus.test
```
