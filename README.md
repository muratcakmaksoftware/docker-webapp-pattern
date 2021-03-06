# Monolithic | Microservices Architecture

## Installation & Run
```
docker-compose up -d
```

## About
Sıfırdan projeye başlarken veya mevcut projeye hızlı ayarları aktarabileceğimiz alt yapı ayarlamaktadır.\
Projenin içerisinde Dockerfile dosyaları açık şekilde yapılandırılmıştır.\
Bunun sebebi geliştirme sırasında değişikleri build alınıp en son production ortamı için o çıktıların kullanması içindir. Bu yöntem geliştirme sırasında kolaylık sağlamaktadır.

## Default Config

- PHP
- NGINX
- Postgresql (Relational Database Management System (RDBMS))
- Redis (Cache Disk & Memory)
- Memcached (Cache Memory Alternative)
- RabbitMQ (Message Queue)
- MongoDB (NoSql) & Mongo Express (isteğe bağlı) Veya yerine Studio 3T & MongoDB Compass
- ELK Stack\
  **Elasticsearch (Full Text Search Engine)** (Indexing & Storage) **Verileri indeksler ve saklar.**\
  **Logstash** (Data Aggregation & Processing) **Verileri toplar ve işler. İstenilen veritabanlarına dağıtır.**\
  **Kibana** (Analysis & visualization) **Analiz edilen verileri panel üzerinden görselleştirme sağlar.**

### Docker
```
Elasticsearch için gereklidir
1)bootstrap check failure [1] of [2]: max virtual memory areas vm.max_map_count [65530] is too low,increase to at least [262144]
//For Windows
wsl -d docker-desktop
echo "vm.max_map_count = 262144"> /etc/sysctl.d/999-docker-desktop-conf
sysctl -w vm.max_map_count=262144

//For Linux
sudo sysctl -w vm.max_map_count=262144
Ve bu ayarda kalıcılık sağlamak için:
sudo echo 'vm.max_map_count=262144' >> /etc/sysctl.conf

2)bootstrap check failure [2] of [2]: Transport SSL must be enabled if security is enabled. 
Please set [xpack.security.transport.ssl.enabled] to [true] or disable security by setting [xpack.security.enabled] to [false]

v6.8.0 dan itibaren elasticsearch basic security free olarak vermiştir.
**xpack.security.enabled=true**

//Farklı güvenlik olarak Search Guard bakılabilir:
https://medium.com/devopsturkiye/open-source-olarak-kullanılan-elk-yapısında-güvenlik-nasıl-sağlanır-d9586148c82 

Elasticsearch hata log burada cluster adınız altında bilgisi tutulur: 
/usr/share/elasticsearch/logs/es-myapp-cluster.log
```
### Postgresql
#### Auth
Mevcut ayarlarda postgresql DEFAULT bilgileri .env'de mevcuttur.

### Redis
#### Auth
Default'da redis de şifre yoktur.\
Redis dışardan erişim açıyorsanız şifre koruması eklenmelidir.\
Mevcut ayarlarda redis DEFAULT şifresi .env'de mevcuttur.
```
//Manuel Redis şifre belirlemek için
//Redis terminal den redis cli erişilir.
redis-cli

//Şifre ataması
CONFIG SET requirepass "<password>"

//Redis'e giriş yapma
AUTH <password>

//Ek olarak redis 6 ve üstü sürümlerinde ACL gelmiştir.
ACL ile username ve password şeklinde geniş bir yetkilendirme sağlanabilir.
```
#### GUI Clients
- [Another Redis Desktop Manager](https://github.com/qishibo/AnotherRedisDesktopManager)
- [Redis GUI](https://github.com/ekvedaras/redis-gui)

### Memcached
Client için telnet kullanılmaktadır verileri görüntülemek veya manuel olarak işlem yapmak istersek:
```
telnet <ip_address> <port>
telnet localhost 11211
```

### RabbitMQ
Web Panel: http://localhost:15672
```
Management
Default Admin: guest
Default Password: guest
```

### MongoDB
#### Auth
İlk çalıştırmada mongodb'de belirtilen kullanıcı adı ve şifre otomatik olarak tanımlanır.\
Bu şekilde istersek kendimizde kullanıcı tanımlayabiliriz.
```
//Container MongoDB Terminal Bağlanılır.
//mongo'ya local bağlantı sağlanır.
mongo --port 27017

//admin veritabanına geçiş sağlanır.
use admin

//Veritabanına user eklenir.
db.createUser({ user: "mongoadmin" , pwd: "mongoadmin", roles: ["userAdminAnyDatabase", "dbAdminAnyDatabase", "readWriteAnyDatabase"]})
```

#### GUI Clients
- [Studio 3T](https://studio3t.com/download/)
- [MongoDB Compass](https://www.mongodb.com/try/download/compass)
- [NoSQLBooster](https://nosqlbooster.com/downloads)
- **Mango Express** Web Panel: **http://localhost:8081**

### Elasticsearch
#### Auth
Web Panel: http://localhost:5601 \
**Dikkat bağlanamazsanız:** elasticsearch-setup bittiğinden emin olunuz.
```
Default Admin: elastic
Default Password: elastic123456
```