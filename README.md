# Monolithic | Microservices Architecture

## Installation & Run
```
docker-compose up -d
```

## Default Config

- PHP
- NGINX
- Postgresql (Relational Database Management System (RDBMS))
- Redis (Cache Disk & Memory)
- RabbitMQ (Message Queue)
- MongoDB (NoSql) & Mongo Express (isteğe bağlı) Veya yerine Studio 3T & MongoDB Compass
- ELK Stack\
  **Elasticsearch (Full Text Search Engine)** (Indexing & Storage) **Verileri indeksler ve saklar.**\
  **Logstash** (Data Aggregation & Processing) **Verileri toplar ve işler. İstenilen veritabanlarına dağıtır.**\
  **Kibana** (Analysis & visualization) **Analiz edilen verileri panel üzerinden görselleştirme sağlar.**

### Redis
#### Auth
Default'da redis de şifre yoktur.\
Redis dışardan erişim açıyorsanız şifre koruması eklenmelidir.\
Mevcut ayarlarda redis default şifresi .env'de belirlidir.
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

### RabbitMQ
```
Management
Web bağlantısı: localhost:15672
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
- **Mango Express** web bağlantısı: **localhost:8081**
