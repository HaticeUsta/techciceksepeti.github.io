---
layout: post
title: Elasticsearch
description: Elasticsearch java ile geliştirlmiş açık kaynakm kodlu Lucene tabanlı ölçeklenebilir full text arama motoru ve veri analiz aracıdır.
category: sunum
author: alibalci
tags: [sunum, nosql, elasticsearch, elastic, cap teoremi]
featureImg: elasticsearch.jpg
---
Elasticsearch java ile geliştirlmiş açık kaynak kodlu Lucene tabanlı ölçeklenebilir full text arama motoru ve veri analiz aracıdır.

Öncelikle Nosql'in ne olduğu konusuyla başlayalım.

## NOSQL

Nosql bir çeşit veritabanı yönetim sistemidir, fakat ilişkisel veritabanları sistemlerinin farklı kuralları var. Bu tip veritabanları Sql veritabanları yerine kullanılmaktan ziyade ilişkisel veritabanlarının yetersiz kaldığı yerlerde destek amacıyla kullanılabilir. Nosql ‘Not Only Sql’ olarak adlandırılır, Sql tipi sorgu cümlecikleri ile sorgulama yapmamızı sağlamaktadır.

Geleneksel veritabanlarında temel işlemler Read ve Write işlemleridir. Read işleminin performansı için veritabanlarının replikaları oluşturulup birden çok server üzerinden load-balancer gelen istekleri bölüştürerek daha performanslı hale getirebilir.Fakat bunun sonucunda Write işlemi olumsuz etkilenmekte bunun nedeni yazılan verinin diger replikalara aktarılması gerekmekte veri tutarlılığı açısından. Write işlemi için performans artışı saglamak için partitionlara bölme işlemi yapılabilir. Bu da Read işlemini olumsuz etkilemekte çünkü dağıtık veritabanlarında ‘Join’ işlemleri yavaş ve implementasyonu zordur. Ayrıca ‘ACID’ özelliği nedeniyle de veri tutarlılığı için veri kitlenebiliyor. Şöyle ki, iki kullanıcı aynı anda aynı veriyi değiştirme çalıştığında sadece bir kullanıcının değişiklik yapması için veri üzerindeki işlem bitene kadar kitlenmekte.

Bu limitler büyük bir sorun teşkil etmekte. Ayrıca bigdata ve social networking dünyanın heryerinde milyonlarca kullanıcıya dakikalar içerisinde binlerce okuma ve yazma isteği geleneksel RDBMS için başa çıkılmaz hale gelmiştir. Bu sistemlerin sadece ‘scale-up’ ile central kaynakları artırma işlemi yetersiz kalmakta. NoSql çözümler ‘scale-out’ özelliği ile daha fazla server devreye sokularak çözülmekte.

### Scale Up/Out

Bundan birkaç yıl önce yazılım performansı artırmak için 2 seçenek vardı.Bunların ilki donanım kaynaklarını artırmak ‘scale-up’ yada ‘vertical scale’ .Buda serverların ram, işlemci gücünü artırmak. Diğer seçenekte daha etkili ve daha hızlı çalışması için performance tunning yapılırdı. Günümüzde performans geliştirmesi için üçüncü bir seçenek ‘horizontal scale(scale-out)’ kavramı çıkmıştır.

‘Horizontal scale’ son yıllarda zorunluluk haline gelimiştir. Çünkü şirketlerin yazılımlarının tek server, tek veritabanı, tek datacenter ve birarada calıştırma fikri kabul görmemeye başladı. Bu tarz sorunları çözmek için dağıtık ortamlara geçmek gerekmekte. Dağıtık sistemlerde veriler birçok farklı client/nodes farklı lokasyonlarda olabilmekte. Herhangi bir node fail olması durumunda diğer nodelar sistem aksamadan devam edebilmekte.

#### Vertical Scale

Genel olarak sistemin ram ve işlemci gücünü atırmak.

**Pros**

*   Birden çok server harcadığı enerji yerine tek sunucu harcadıgı enerji maliyeti
*   Soğutma
*   İmplementasyon
*   Tek sunucu tek lisans anahtarı
*   Bazı durumlarda network trafiği daha az

**Cons**

*   Fiyat
*   Donanımsal küçük bir sorunun tüm sistemi etkilemesi ve sistemin durması

#### Horizontal Scale

Genel olarak daha az işlemcili ve ramli bir makinanın sisteme eklenmesi. Daha ucuz ve teorik olarak sonsuz ölçeklenebilir.

**Pros**

*   Vertical scale göre ucuz
*   Fault -tolerance (bir node çökmesi sistemin durması engellemez)
*   Upgrade

**Cons**

*   Lisans maliyeti
*   Daha fazla server daha fazla elektrik ve sogutma maliyeti
*   Daha fazla Network cihazları

### CAP TEOREMİ

Scaling stratejileri sonucunda complexity ek olarak sistemde bazı penaltılar oluşmakta.Bu devre de Cap Teoremine değinmek gerekmete.

**Cap teoremi,** ilk olarak 1998 yılında California üniversitesinde bilgisayar bilimcisi Eric Brewer tarafından ortaya atılmıştır.Bu teoriye göre dağıtık sistemler 3 koşuldan (Consistency, Availability, Partition Tolerance) ikisi sağlar ve garanti eder. Consistency (tutarlılık) dağıtık sistemdeki tüm veriler aynı ve tutarlı olmalı.Eğer consistency seçersek bir node tutaln verilerin diğer nodelardaki verilerle tutarlı olması gerekmektedir.Tutarlılık için node lar arası veriler aktarılmalı. Bu da anlık olarak veritabanlarının unavailable olması demektir. Senkronizyon maliyeti.

*   BASE, data modellinde consistency den fedakarlık yapılarak availbility üzerine odaklanmıştır. CAP teoreminde AP tipi veritabanları için geçerlidir. (Eventual Consistency)

*   ACID, Base modelin tam tersi olarak consistency üzerine odaklanmıştır.Bu transaction desteği sunmakta.

*   Atomicity, Transaction içindeki her bir atomik işlemi ifade etmekte.Bu işlemlerden biri fail olursa tüm transaction roll back yapılır.
*   Consistency, transaction içindeki verilerin veritabanındaki karşılığı valid olup olmaması, ya da aynı anda 2 transaction aynı veriye erişmek istediğinde ilk transaction öncelik verip ikinci transaction için veriyi kitleyip ikinci transaction bekletmesi.
*   Isolation, transactionlar kendi içerisinde izole başka transaction diğer transactionlara mudahale edemez.
*   Durability, transaction commit edildikten sonra her şekilde veritabanına yazılır. Herhangi bir hata yada elektrik kesintisi gibi durumlarda veri kaybı ölemek için non-volatile memory kayıt edilir.

### NOSQL Database Tipleri

*   Key-Value: Complex yapı olarak en basit yapıya sahip.Bu veritabanında tüm data ilişkili key bağlıdır. Veri sorgulama bu key üzerinden yapılır.

*   Wide-Column: Key value tipi veritabanlara benzemekte.

*   Document Base: Veriler yapısal bir doküman şekilinde tutulmakta.

*   Graph Database: Bu veritabanı graph teoresine göre yapılmıstır.Veritabanıda kayıtlar graph selkilde birbiri ile ilişki olabilmekte.

## ELASTICSEARCH

Elasticsearch java ile geliştirlmiş açık kaynak kodlu Lucene tabanlı ölçeklenebilir full text arama motoru ve veri analiz aracıdır. Gerçek zamanlı ve dağıtık oluşu en önemli artılarıdır.Elasticsearch bir önemli özelliğide restfull api göre uyarlanmış Http üzerinden json kullanılarak gerçekleştirmekte. Elasticsearch verileri inverted index olarak indekslemektedir.

**Pros**

*   Full-text Search: Sadece spesifik bir keyword aramasından ziyade aranan keywordu içeren tüm kayıtların gelmesi sql deki like cümleciği gibi

*   Clustering: Dağıtık nodelar üzerinden load balancing

*   Horizontal scaling: gerekli görüldüğünde cluster capacity artırmak için extra node açmak

*   Read -Write Effiency: Okuma ve yazma işlemleri cok hızlı ve etkili yapması.

*   Fault Tolerance: Herhangi bir node fail olduğu zaman sistem çalışması aksamadan devam eder.

<iframe src="//slides.com/alibalci/nosql-elasticsearch/embed" width="720" height="498" frameborder="0" scrolling="no" allowfullscreen="allowfullscreen"></iframe>