# Zabbix

## Instalar Zabbix

1º Introducir el siguiente código

```bash
  wget wget https://repo.zabbix.com/zabbix/4.2/ubuntu/pool/main/z/zabbix-release/zabbix-release_4.2-1+bionic_all.deb
```

Aparecera algo asi

![1](./imagenes/1.png)

2º Instalar el paquete

```bash
	sudo dpkg -i zabbix-release_4.2-1+bionic_all.deb
```

Aparecera algo asi

![1](./imagenes/2.png)


3º Instalamos otro de los paquetes necesarios para Zabbix

```bash
	sudo apt install -y zabbix-server-mysql zabbix-frontend-php zabbix-agent
```

Aparecera algo asi

![1](./imagenes/3.png)

4º Entramos en sql para configurarlo

```bash
	mysql -uroot -p
```

Aparecera algo asi

![1](./imagenes/4.png)


5º Creamos la base de datos de nuesto servicio de monitarización:

```ini
	create database zabbix character set utf8 collate utf8_bin;
```

Aparecera algo asi

![1](./imagenes/5.png)

6º Ponemos el siguiente comando , en el cual ponemos el usuario y la contraseña:

```ini
	grant all privileges on zabbix.* to zabbix@localhost identified by 'password';
```

Aparecera algo asi

![1](./imagenes/6.png)

7º Salimos de MariaDB

```bash
	quit
```

Aparecera algo asi

![1](./imagenes/7.png)


8º

```bash
	sudo zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -uzabbix -p zabbix
```

Aparecera algo asi

![1](./imagenes/8.png)

9º Editamos el archivo /etc/zabbix/zabbix_server.conf y modificamos las siguientes propiedades

```ini
	DBUser=zabbix
	DBPassword=password
```

10º

```ini-- 
	<IfModule mod_php5.c>
    php_value max_execution_time 300
    php_value memory_limit 128M
    php_value post_max_size 16M
    php_value upload_max_filesize 2M
    php_value max_input_time 300
    php_value max_input_vars 10000
    php_value always_populate_raw_post_data -1
    php_value date.timezone Europe/London			<--- Añadimos esta línea(Aparecera como comentario)
</IfModule>
<IfModule mod_php7.c>
    php_value max_execution_time 300
    php_value memory_limit 128M
    php_value post_max_size 16M
    php_value upload_max_filesize 2M
    php_value max_input_time 300
    php_value max_input_vars 10000
    php_value always_populate_raw_post_data -1
    php_value date.timezone Europe/London			<--- Añadimos esta línea(Aparecera como comentario)
</IfModule>
```

![1](./imagenes/9.png)

11º

```bash
	sudo systemctl restart zabbix-server zabbix-agent apache2
```

![1](./imagenes/10.png)

12º

```bash
	sudo systemctl enable zabbix-server zabbix-agent apache2
```
![1](./imagenes/11.png)

13º

14º

16º

17º

18º

