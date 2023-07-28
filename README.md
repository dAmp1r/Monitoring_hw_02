# Monitoring_hw_02
Система мониторинга Zabbix

Задание 1.          

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
![Авторизация](https://github.com/dAmp1r/Monitoring_hw_02/blob/main/zabbix.png)


Задание 2.       

wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb        
dpkg -i zabbix-release_6.0-4+debian11_all.deb        
apt update        
apt install zabbix-agent              
nano /etc/zabbix/zabbix_agentd.conf #вносим изменения в строке Server          
systemctl restart zabbix-agent.service             
systemctl enable zabbix-agent         
![Host](https://github.com/dAmp1r/Monitoring_hw_02/blob/main/host.png)
![Log](https://github.com/dAmp1r/Monitoring_hw_02/blob/main/log_agent.png)
![Latest date](https://github.com/dAmp1r/Monitoring_hw_02/blob/main/lates_date.png)
