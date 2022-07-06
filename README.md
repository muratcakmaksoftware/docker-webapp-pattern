# Monolithic Architecture

## Installation & Run
```
docker-compose up -d
```

## Default Config

- PHP
- Postgresql
- Redis
- RabbitMQ
- MongoDB


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