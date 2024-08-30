# (Server-01 ) Install MySQL on DataBase Server on RHEL 9.4

```
yum update -y
yum install wget git -y
wget https://dev.mysql.com/get/mysql84-community-release-el9-1.noarch.rpm
rpm -i mysql84-community-release-el9-1.noarch.rpm 
dnf install -y mysql-community-server
systemctl start mysqld && systemctl enable mysqld
cat /var/log/mysqld.log | grep "password"  # get the Password 
mysql_secure_installation # Reset the Password here 
```

# Create a DB and table
```
mysql -u root -p <your pass>
```

# Create a Database
```
create database anand;
use anand;
```

# Create a Table
```
CREATE TABLE accounts (
    id int NOT NULL AUTO_INCREMENT,
    username varchar(255) NOT NULL,
    fullname varchar(255) NOT NULL,
    password varchar(255) NOT NULL,
    email varchar(255),
    designation varchar(255) NOT NULL,
    about_yourself varchar(255) NOT NULL,
    PRIMARY KEY (id)
);
```

## Create a User and assign specific permissions
```
CREATE USER 'root'@'%' IDENTIFIED BY 'Anand@123';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';
FLUSH PRIVILEGES;
```

# ( Server -02 ) Python Installation on RHEL 9.4
-----------------------------------------------
# pre-required softwares
```
yum install wget,git -y

```

# Other Pre-requirements
```
yum -y install gcc gcc-c++ kernel-devel
yum -y install mysql-devel openssl-devel
yum -y install python3-devel
```

# Get the code from GitHub
```
cd /opt
git clone https://github.com/lazy-anand/python-login-page.git
cd python-login-page
```

# Chnage the DB details in main.py file 
```
app.config['MYSQL_HOST'] = '<your DB IP>'
app.config['MYSQL_USER'] = 'root'
app.config['MYSQL_PASSWORD'] = '<your DB password>'
app.config['MYSQL_DB'] = '<Your DB>'
```

## Create a Vertual ENV
```
python3.9 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

## Run the Application in Baground mode
```
nohup ./run &
```

## Access the Application
```
Login Page : http://IP:5000/pythonlogin/
Registartion Page : http://IP:5000/pythonlogin/register
```
