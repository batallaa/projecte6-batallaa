# T06: Projecte Nexus. Implantació de PKI i Signatura Digital Corporativa

## Fase 1: Preparació de l'entorn de laboratori

Instal·lem tres màquines. Un servidor ubuntu i dos màquines client windows 11. Configurarem les màquines amb adaptador de xarxa en mode pont per la connectivitat de les màquines.

![Captura 1](T06/img/i1.png)

Configurem IP estàtica a la màquina client. Seguim la següent estructura per l'IP del client:

- IP: 192.168.4.y
- Màscara: 255.255.255.0
- Porta d'enllaç: 192.168.4.254
- DNS: 8.8.8.8
    ###### y = número de llista

![Captura 2](T06/img/i2.png)

A la màquina servidor, canviem 

## Fase 2: Creació de l'Entitat de Certificació (CA)

Editem l'arxiu de configuració d'OpenSSL per poder configurar la CA amb la seguent comanda:

```bash
sudo nano /etc/ssl/openssl.cnf
```

Després, afegirem el següent text:

```bash
[ca]
default_ca = CA_default

[CA_default]
dir               = /etc/ssl/CA
certs             = $dir/certs
crl_dir           = $dir/crl
database          = $dir/index.txt
```

Creem l'estructura dels directoris per els fitxers:

```bash
sudo mkdir -p /etc/ssl/CA/{certs,crl,newcerts,private}
sudo touch /etc/ssl/CA/index.txt
sudo echo 001 > /etc/ssl/CA/serial
```

Generem la clau privada i el certificat:

```bash
sudo openssl req -new -x509 -keyout demoCA/private/cakey.pem -out demoCA/cacert.pem
```

### Fase 3: Generació de la clau i certificat d'usuari

En el servidor, generem una clau privada per l'usuari.

```bash
openssl req -new -keyout userkey.pem -out userreq.csr
```

Introduïm la següent comanda per signar la solicitud de la CA.

```bash 
openssl ca -in userreq.csr -out usercert.pem
```

Exportem el certificat en format PKCS#12 (.pfx):

```bash
openssl pkcs12 -export -out CertUser.pfx -inkey userkey.pem -in usercert.pem
```

Introduïm una contrasenya per exportar





