# Monolithic | Microservices Architecture

## Installation & Run
```
docker-compose up -d
```

## Default Config

- PHP
- NGINX
- Postgresql (Relational Database Management System (RDBMS))
- Elasticsearch (Full Text Search Engine)
- Redis (Cache Disk & Memory)
- RabbitMQ (Message Queue)
- MongoDB (NoSql)


### MongoDB Auth
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