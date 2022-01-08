# LEMP-7.4-for-magento-2.4.2-on-UBUNTU-20.04
**VERY FIRST**

	 1. `sudo apt update`
	 2. `sudo apt install -y curl`
	 3. `sudo apt -y install software-properties-common dirmngr apt-transport-https`
		 
**DEPENDENCY**
 1. **Nginx 1.8**
	 -  `sudo apt-get -y install nginx=1.8`
	 - `sudo systemctl enable nginx`

 2. **PHP 7.4**
	 - `sudo apt -y install php7.4 php7.4-cli php7.4-fpm php7.4-json php7.4-common php7.4-mysql php7.4-zip php7.4-gd php7.4-mbstring php7.4-curl php7.4-xml php7.4-pear php7.4-bcmath php7.4-redis php7.4-intl`
	 - `sudo systemctl enable php-fpm`
	 
 3. **Composer 2.x**
	- `sudo curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --2`

 4. **MariaDB 10.4** 
	- *Install MariaDB 10.4* 
		 -  `sudo apt-key adv --fetch-keys '[https://mariadb.org/mariadb_release_signing_key.asc](https://mariadb.org/mariadb_release_signing_key.asc)'`
		 - `sudo add-apt-repository 'deb [arch=amd64,arm64,ppc64el,s390x] [https://mirrors.bkns.vn/mariadb/repo/10.4/ubuntu](https://mirrors.bkns.vn/mariadb/repo/10.4/ubuntu) $(lsb_release -cs) main'`
		 - `sudo apt update`
		 - `sudo apt install mariadb-server mariadb-client`
		 - You will be prompted to provide MariaDB root password, type the password to set.![password](https://github.com/beobungbu/LEMP-7.4-for-magento-2.4.2/raw/b6d2a143be3eb218999e636389b4e5816ef0b56a/mariadb-10-4-installing-asking-for-root-password.png)
		 - Confirm password:
		 ![confirm password](https://github.com/beobungbu/LEMP-7.4-for-magento-2.4.2/raw/main/mariadb-10-4-installing-confirm-for-root-password.png)
	 - *Config MariaDB*
		 - `sudo mysql_secure_installation`
		 - enter or set root password.
		 - **Switch to unix_socket authentication [Y/n]**: **y**
		 - **Change the root password? [Y/n]**: if you have enter new root password before, then type down **n**, otherwise, type **y**.
		 - **Remove anonymous users? [Y/n]**: **y**
		 - **Disallow root login remotely? [Y/n]**: **y**
		 - **Remove test database and access to it? [Y/n]**: **y**
		 - **Reload privilege tables now? [Y/n]**: **y**
		 - `sudo systemctl enable mysql`
		 - `sudo systemctl restart mysql`
 5. **ElasticSearch 7.9.3** 
	 - **Install ElasticSearch**
	   - `curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -`
	   - `echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list`
	   - `sudo apt update && sudo apt install elasticsearch=7.9.3`
	  -  **Configuring Elasticsearch**
		  -		  The  `elasticsearch.yml`  file provides configuration options for
				 your cluster, node, paths, memory, network, discovery, and gateway.
				 Most of these options are preconfigured in the file but you can change
				 them according to your needs. For the purposes of our demonstration of
				 a single-server configuration, we will only adjust the settings for
				 the network host.
				 
				 Elasticsearch listens for traffic from everywhere on port  `9200`. You
				 will want to restrict outside access to your Elasticsearch instance to
				 prevent outsiders from reading your data or shutting down your
				 Elasticsearch cluster through its  [REST
				 API](https://en.wikipedia.org/wiki/Representational_state_transfer).
				 To restrict access and therefore increase security, find the line that
				 specifies  `network.host`, uncomment it, and replace its value with 
				 `localhost`  so it reads like this:
			- ![elasticSearchLocalhostConfig](https://github.com/beobungbu/LEMP-7.4-for-magento-2.4.2/raw/main/elasticsearch.PNG)
			- `sudo nano /etc/elasticsearch/elasticsearch.yml`

