# 🌐 user-company-gateway-v1

Gateway ini merupakan pintu masuk utama ke seluruh service microservice `user-company-*`.  
Dibangun menggunakan **Spring Cloud Gateway**, dengan integrasi ke **Eureka**.

---

## 🚀 Fitur

- Routing otomatis ke service yang terdaftar di Eureka
- Predikat path: `/users/**`, `/companies/**`, `/members/**`
- Load balancing dengan `lb://` (via Eureka)
- Port default: `8080`

---

## 📦 Dependency

- Spring Boot 3.5.3
- Spring Cloud Gateway
- Eureka Client (Netflix)
- Java 21

---

## ⚙️ Konfigurasi `application.yml`

```yaml
server:
  port: 8080

spring:
  application:
    name: user-company-gateway-v1

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka

spring:
  cloud:
    gateway:
      routes:
        - id: user-company-web-v1
          uri: lb://user-company-web-v1
          predicates:
            - Path=/users/**, /companies/**, /members/**, /subscriptions/**
```

---

## 🛠 Cara Menjalankan

```bash
mvn clean install
mvn spring-boot:run
```

Akses melalui:
```
http://localhost:8080/users
http://localhost:8080/companies
```

---

## 🧱 Struktur

```
src/main/java/com/company/gateway/
└── UserCompanyGatewayV1Application.java
```

---

## 🔗 Integrasi Service

Service `web-v1` harus memiliki konfigurasi seperti berikut:

```yaml
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka
```

Dan memiliki `application.name=user-company-web-v1`.

---

## 👨‍💻 Maintainer

[@dwiaribowokj](https://github.com/dwiaribowokj)