# WPLearn
Projeto criado para praticar docker, subindo imagem wordpress e conectando com uma imagem mysql.

#Atenção:
Ao subir o container do mysql, criar o usuário do Wordpress no mysql e dar grant.

docker exec -it <nome do container mysql> mysql -u root -p

mysql> create user '<variavel WORDPRESS_DB_USER>' identified by '<WORDPRESS_DB_PASSWORD>';

mysql> create database '<WORDPRESS_DB_USER>';
mysql> grant all privileges on <WORDPRESS_DB_USER>.* to '<WORDPRESS_DB_PASSWORD>';
mysql> flush privileges;

#Subindo container na mão
1. container do mysql 
sudo docker run -d --name mysql101 -e "MYSQL_ROOT_PASSWORD=asterisco" -e "MYSQL_DATABASE=wordpress" -e "MYSQL_USER=wordpress" -e "MYSQL_PASSWORD=wordpress" -v "/home/andrelsa/Documentos/estudoDocker/WPLearn/MySqlData:/var/lib/mysql" mysql:5.7



2. container do wordpress
sudo docker run -d --name wp101 --link mysql101:mysql -p 8080:80 -v "/home/andrelsa/Documentos/estudoDocker/WPLearn/wordpress_data:/var/www/html" wordpress


