---
layout: post
title: Design Patterns & Unit of Work
description: Tasarım kalıpları yazılım dünyasının olmazsa olmazları arasında yer almaktadır.
category: sunum
author: kaancelebi
tags: [sunum, design patterns, gang of four, unit of work, repository, dbcontext]
---
Tasarım kalıpları yazılım dünyasının olmazsa olmazları arasında yer almaktadır. Platform bağımsız olan bu tasarımları projelerinizde yapacağınız işlere göre uygulayabilirsiniz. Tasarım kalıpları projelerimizdeki sorunlara karşı çözüm sunar, tekrardan kullanılabilir yapı elde etmemizi sağlar ve nesneye yönelik programlamada nesneler arası iletişimi gerçekleştirir.

Tasarım kalıpları denince akla “Gang of Four” gelmektedir. Yazılım adına önemli adımlar atmış bu kişiler kimilerine göre gereksiz olsa da hayatımızı kolaylaştıracak işler yapmışlardır. “Gang of Four” tarafından yaklaşık olarak 23 tane tasarım kalıbı sunuldu. Bunları Creational (oluşumsal) , Structural (yapılsal) ve Behavioral (davranışsal) olarak üç gruba ayırdılar. Kategorilere ayırmalarında ki amaç ise nesnelerin oluşturulması, yapılarına ve davranışlarına göre tasarım kalıpları sunmaktı. Örnek vermek gerekirse en yaygın tasarım deseni olan Singleton tasarım kalıbı Oluşumsal (creational) tasarım kalıplarına girmektedir. Adından da anlaşılacağı üzere nesnemizin tek bir örneğini alarak bir tane daha oluşmamasını sağlamaktadır.

“Gang of Four” tasarım kalıplarının haricinde başka kalıplarda vardır. Unit of Work ‘te bir tasarım deseni olup Martin Fowler ‘in PoEAA kitabında yer almaktadır.

Bu tasarım kalıbı yazılım dünyasında çok basit gibi gözüken bir sorunu ortadan kaldırsa da çok büyük bir amaca hizmet etmektedir. Bu tasarım kalıbını kullanması oldukça basittir.

Unit of Work veri tabanı ile yapılacak bütün işlemleri tek bir kanaldan yürütme ve bir yerde hafızada tutmayı kendine amaç olarak edinmiştir. Unit of Work sınıfı yaptığı işten anlaşılacağı üzere veri tabanı işlemlerini yönettiğimiz Data Access Layer katmanında yapmaktadır. Unit of Work yapılan işlemlerin bir birim üzerinden ele alıp, bu olayları saklayan daha sonra ise toplu halde kaydedilmesi, bir hata ile karşılaşıldığında geri alınması ve ya iptal edilmesini sağlamaktır.

Yazılım projelerinde birden fazla tasarım kalıbı kullanılabilmektedir. Unit of Work tasarım kalıbı da isterseniz Repository, Identy Map veya tek başına da kullanabilirsiniz. Unit of Work kalıbını uygulayabilmek için elimizde veri işlemlerinin yapıldığı bir nesne olmalıdır. Bu Reposityory, Generic Reposityory kalıbı ya da CRUD (create, read, upldate, delete) işlemlerinin yapıldığı bir sınıf olabilir. Unit of Work sınıfımızda ORM kullanıyorsak bir DBContext ‘i Repository sınıflarımıza verirsek Unit of Work tasarım kalıbını neredeyse uygulamış oluruz.

Temel olarak şu şekilde yazabiliriz:

1. CRUD işlemleri yapılan sınıflara Unit of Work sınıfı içerisinden DBContext verilmeli

2. CRUD işlemini yapan sınıf kaydetme işlemlerini DBContext ‘in SubmitChanges() metodunu çağırmamalı onun yerine işlemler Unit of Work sınıfına yazılmış Save() metodu çağırmalı

3. İşlemleri veri tabanına aktarma sırasında hata ile karşılaşıldığında Rollback işlemleri için metot yazılmalı

Genelde olarak Unit of Work kalıbı örnekleri Repository tasarım kalıbı ile verilmekte ama CRUD işlemlerini yapan sınıf ile de Unit of Work tasarım kalıbını kullanabiliriz.

Unit of Work kalıbını projeye uygulaması oldukça basittir. Unit of Work için oluşturulan sınıf içerisinde CRUD işlemlerini yapan sınıflar birer Property olarak tutulurlar. Bu Property’lerin her birine DBContext gönderilir. Property olarak oluşturduğumuz her sınıf içinde değişmiş tüm veriyi saklar. Unit of Work sınıfı içerisine Save() metodu olmaldır. Ayrıca Rollback, Dispose() ve ya Log() metotları da yazılabilir. Sınıftaki Save() metodu çağırıldığında Property’ler üzerindeki veriler tek bir kanaldan veri tabanına aktarılır. Eğer kayıt işlemleri sırasında hata ile karşılaşırsak Log() metodunu çağırarak hatanın neden kaynaklandığını kaydedip ve veri tabanının yapısı bozulmaması içinde Rollback() metodunu çağırabilir böylece veri korumada avantaj sağlamış oluruz.

Sonuç olarak Unit of Work kullanımı tahmin etmediğiniz kadar basit olmakla birlikte isterseniz Repository, Generic Repository ya da kendi CRUD sınıfınızla kullanılabilirsiniz. Tek yapılması gereken DBContext’i işlem yapan sınıflara yollamanız ve kaydetme işlemini Unit of Work üzerinden yapılmasıdır. Eğer yapınızda birden fazla servis kullanıyorsanız tek bir Unit of Work yazmak yerine birden fazlada Unit of Work sınıfı yaratıp kullanabilirsiniz.  

<iframe src="//slides.com/kaancelebi/unit-of-work/embed" width="720" height="528" frameborder="0" scrolling="no" allowfullscreen="allowfullscreen"></iframe>