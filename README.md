# Monitoring_hw_02
Система мониторинга Zabbix

sudo su          
apt install zabbix-server-pgsql        
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb           
dpkg -i zabbix-release_6.0-4+debian11_all.deb            
apt update           
apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent          
su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD '\'123456789\'';"'          
su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"'           
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix           
sed -i 's/# DBPassword=/DBPassword=123456789/g' /etc/zabbix/zabbix_server.conf           
sudo systemctl restart zabbix-server apache2             
sudo systemctl enable zabbix-server apache2           
  
