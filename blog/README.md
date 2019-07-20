Blog de Exemplo
==================================================

Este exemplo é baseado em "Hello World" desenvolvido em Zend 3 e demontra:

  * Integração do site com a biblioteca Doctrine
  * Usando EntityManager
  * Criando entidades
  * Criando e parametrizando propriedades
  * Definindo relacionamento entre entidades
  * Criando repositórios

## Instalação

### Requisitos

- php >= 7.*
- php-cli instalando (verificar php -v)
- composer instalado (verificar composer -v)
- mysql >= 5.6
- (opcional) phpmnyadmin
- (opciona)) mysql-client (verificar mysql -v)

### Baixando

```
mkdir projeto-base
git clone git clone https://github.com/alfa-eduardobona/using-zf3-book-samples.git projeto-base
cd projeto-base/blog
```

### Instalando

```
composer install
php -S localhost:9001 -t public
```

Adjust permissions for `data` directory:

```
sudo chown -R www-data:www-data data
sudo chmod -R 775 data
```

Create `config/autoload/local.php` config file by copying its distrib version:

```
cp config/autoload/local.php.dist config/autoload/local.php
```

Edit `config/autoload/local.php` and set database password parameter.

Login to MySQL client:

```
mysql -u root -p
```

Create database:

```
CREATE DATABASE blog;
GRANT ALL PRIVILEGES ON blog.* TO blog@localhost identified by '<your_password>';
quit
```

Create tables and import data to database:

```
mysql -u root -p blog < data/schema.mysql.sql
```

Alternatively, you can run database migrations:

```
./vendor/bin/doctrine-module migrations:migrate
```

## Development Mode

The command above will install the dependencies (Zend Framework and Doctrine).

Enable development mode:

```
composer development-enable
```

## Zend Developer Tools

Adicione no término do array de módulos do zend o módulo ZendDeveloperTools

```
// config/modules.config.php
<?php

return [
    ...
    ...
    ...
    'Application',
    'ZendDeveloperTools'
];

```

Then create an Apache virtual host. It should look like below:

```
<VirtualHost *:80>
    DocumentRoot /path/to/blog/public
    
	<Directory /path/to/blog/public/>
        DirectoryIndex index.php
        AllowOverride All
        Require all granted
    </Directory>

</VirtualHost>
```
After creating the virtual host, restart Apache.

Now you should be able to see the Blog website by visiting the link "http://localhost/". 
 
## License

This code is provided under the [BSD-like license](https://en.wikipedia.org/wiki/BSD_licenses). 

## Contributing

If you found a mistake or a bug, please report it using the [Issues](https://github.com/olegkrivtsov/using-zf3-book-samples/issues) page. Your feedback is highly appreciated.
