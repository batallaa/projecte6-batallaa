# T03: Missió Nginx: Migració d'Alt Rendiment i Arquitectura Lleugera

## 1. Instal·lació de nginx

### 1.1 Deshabilitar nginxs

Per començar amb Nginx, reutilitzarem la màquina de apache2. Per això, deshabilitem l'apache2 i instal·larem el nginx. Després, comprovem que el servei està deshabilitat.

```bash
sudo systemctl stop apache2
sudo systemctl disable apache2
```

![Captura 1](T03/img/i01.png)

### 1.2 Instal·lar nginx

Instal·lem el servei nginx.
 
```bash
sudo apt install nginx -y
```

![Captura 2](T03/img/i02.png)

### 1.3 Verificació

Verifiquem que el servei nginx funciona correctament.

```bash
sudo systemctl status nginx 
```

![Captura 3](T03/img/i03.png)

Perquè funcioni nginx, canviem l'arxiu de configuració per indicar la nova ruta de nginx (/usr/share/nginx/html)

```bash
sudo nano /etc/nginx/sites-available/default
```

![Captura 4](T03/img/i04.png)

Reiniciem el servei per aplicar els canvis al servidor.

```bash
sudo systemctl reload nginx
```

### 1.4 Prova de funcionalitat

![Captura 5](T03/img/i05.png)

Comprovem que la pàgina funciona correctament amb nginx. Entrem amb la màquina Zorin utilitzada a l'anterior tasca.

![Captura 6](T03/img/i06.png)

## 2. Configuració de Server Blocks (Multidomini)

### 2.1 Estructura 

En cas que haguem fet nginx en la mateixa màquina que apache, reutilitzarem les carpetes. Si no és així, les crearem.

```bash
sudo mkdir -p /var/www/nexus
sudo mkdir -p /var/www/academia
```

### 2.2 Permisos

Per els permisos, deixarem com a admin a www-data. Després, comprovem els permisos.

```bash
sudo chown -R www-data:www-data /var/www/nexus /var/www/academia

ls -ld www-data
```

![Captura 7](T03/img/i07.png)
![Captura 8](T03/img/i08.png)

### 2.3 Hosts

Si no hem afegit els hosts a la màquina client, entrarem a l'arxiu /etc/hosts i possarem l'ip del servidor juntament amb els dominis dels dos (projectenexus i academia).

```bash
sudo nano /etc/hosts
```

![Captura 9](T03/img/i09.png)

### 2.4 Server Block amb HTTP

Creem els fitxers següents i modifiquem el contingut:

```bash
sudo nano /etc/nginx/sites-available/projectenexus.test
sudo nano /etc/nginx/sites-available/academia.test
```

**Projectenexus**

```bash
server {
    listen 80;
    server_name projectenexus.test;

    root /var/www/nexus;
    index index.html;

    error_page 404 /404.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

![Captura 10](T03/img/i10.png)

**Academia**

```bash
server {

    server_name academia.test;
    listen 80;

    root /var/www/academia;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    error_page 404 /404.html;

}
```

![Captura 11](T03/img/i11.png)

### 2.5 Pàgina 404

Creem o reutilitzem l'estructura 404.html:

```bash
sudo nano /var/www/academia/404.html
sudo nano /var/www/projectenexus/404.html

```

**Exemple Academia:**

```bash
        }

        .container {
            max-width: 500px;
        }

        h1 {
            font-size: 100px;
            margin-bottom: 10px;
        }

        h2 {
            margin-bottom: 15px;
        }

        p {
            margin-bottom: 25px;
            font-size: 18px;
        }

        a {
            display: inline-block;
            padding: 10px 20px;
            background: #f59e0b;
            color: white;
            text-decoration: none;
            border-radius: 5px;
            font-weight: bold;
        }

        a:hover {
            background: #d97706;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>404</h1>
        <h2>Página no encontrada</h2>
        <p>Lo sentimos, la página que buscas no existe o ha sido movida.</p>
        <a href="index.html">Volver al inicio</a>
    </div>

</body>
</html>
```

![Captura 12](T03/img/i12.png)

**Exemple Projectenexus:**

```bash
            margin-bottom: 15px;
            font-weight: 500;
        }

        p {
            margin-bottom: 30px;
            color: #94a3b8;
        }

        .btn {
            display: inline-block;
            padding: 12px 25px;
            background: #38bdf8;
            color: #0f172a;
            text-decoration: none;
            font-weight: bold;
            border-radius: 6px;
            transition: 0.3s;
        }

        .btn:hover {
            background: #0ea5e9;
            transform: scale(1.05);
        }

        .logo {
            font-size: 22px;
            font-weight: bold;
            margin-bottom: 20px;
            letter-spacing: 2px;
            color: #38bdf8;
        }
    </style>
</head>
<body>

    <div class="container">
        <div class="logo">ProjectNexus</div>
        <h1>404</h1>
        <h2>Conexión perdida en el sistema</h2>
        <p>La página que intentas acceder no existe o ha sido movida dentro de la red.</p>
        <a href="index.html" class="btn">Volver al núcleo</a>
    </div>

</body>
</html>
```

![Captura 13](T03/img/i13.png)

### 2.7 Activar els sites i validar sintaxi

Activem les configuracions amb els enllaços simbòlics:

```bash
sudo ln -s /etc/nginx/sites-available/projectenexus.test /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/academia.test /etc/nginx/sites-enabled/
```

![Captura 14](T03/img/i14.png)

Comprovem sintaxi i reiniciem:

```bash
sudo nginx -t
sudo systemctl restart nginx
```

![Captura 15](T03/img/i15.png)

### 2.8 Comprovació

Anem a la màquina client i provem a entrar a la pàgina d'academia introduint malament el link. Ens hauria de sortir un missatge d'error 404.

![Captura 16](T03/img/i16.png)

## HTTPS + redirecció forçada

### 3.1 Certificats

Generem certificats amb la seguent comanda:

```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \ -keyout /etc/nginx/projectenexus/private/projectenexus.key \ -out /etc/nginx/projectenexus/cert/projectenexus.crt

sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \ -keyout /etc/nginx/academia/private/academia.key \ -out /etc/nginx/academia/cert/academia.crt
```

