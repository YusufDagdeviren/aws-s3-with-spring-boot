# Spring Boot ve AWS S3 Örnek Proje

Bu proje, Amazon Simple Storage Service (S3) ve Spring Boot kullanılarak geliştirilmiş basit bir örnektir. Bu projede, dosya yükleme ve indirme işlemleri için AWS S3 bulut depolama servisi kullanılmıştır.

## Başlangıç

Projenin yerel ortamınızda çalıştırılabilmesi için aşağıdaki adımları takip edin.

### Gereksinimler

- Java 17
- Maven 3.9.6
- AWS hesabı ve S3 depolama alanı
- Docker compose

### AWS S3 Konfigürasyonu

1. AWS Management Console'a giriş yapın.
2. S3 servisine gidin ve yeni bir depolama alanı oluşturun.
3. IAM (Identity and Access Management) servisine gidin ve proje için bir kullanıcı oluşturun. Bu kullanıcıya S3 erişim izinlerini verin.
4. Kullanıcı için bir erişim anahtarı oluşturun ve bu anahtarı güvenli bir şekilde saklayın.
### Docker Compose ile Uygulamayı Başlatma

1. Terminal veya komut istemcisini açın ve proje dizinine gidin.
2. Aşağıdaki komutu kullanarak Docker Compose'u başlatın:

    ```bash
    docker-compose up -d
    ```
3. customer adında veritabanı oluşturun
### Uygulama Konfigürasyonu

`application.yml` dosyasını açın ve aşağıdaki bilgileri güncelleyin:

```properties
server:
  port: 8080
  error:
    include-message: always

cors:
  allowed-origins: "*"
  allowed-methods: "*"
  allowed-headers: "*"
  exposed-headers: "*"


aws:
  region: YOUR_AWS_REGION
  s3:
    buckets:
      customer: YOUR_BUCKET_NAME

management:
  endpoints:
    web:
      exposure:
        include: "health,info"

spring:
  datasource:
    url: jdbc:postgresql://localhost:5332/customer
    username: YOUR_USER_NAME
    password: YOUR_PASSWORD
  jpa:
    hibernate:
      ddl-auto: validate
    properties:
      hibernate:
        dialect: org.hibernate.dialect.PostgreSQLDialect
        format_sql: true
    show-sql: true
  main:
    web-application-type: servlet
  servlet:
    multipart:
      max-file-size: 10MB
      max-request-size: 10MB
  codec:
    max-in-memory-size: 10MB
```

Bu alanlara kendi AWS bilgilerinizi ve oluşturduğunuz S3 depolama alanının adını ekleyin.  
## Kaynaklar
[AWS S3 Credentials Dosyası Oluşturma](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials-temporary.html)  
[AWS S3 Credentials Dosyasını Ortam Değişkenlerine Tanıtma](https://docs.aws.amazon.com/sdkref/latest/guide/file-location.html)  
[I Learned With Youtube Video of Amigoscode](https://www.youtube.com/watch?v=9i1gQ7w2V24&list=LL&index=4&t=4842s)