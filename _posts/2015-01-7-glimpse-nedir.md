---
layout: post
title: Glimpse Nedir
description: Eğer web projeleri ile çalışmışsanız mutlaka Firebug ve türevlerini kullanmışsınızdır.
category: araçlar
author: onuralp
tags: [sunum]
featureImg: glimpse/glimpsePanel.png
---
Eğer web projeleri ile çalışmışsanız mutlaka [Firebug](http://getfirebug.com/) ve türevlerini kullanmışsınızdır. Glimpse firebug’a çok benzer ancak büyük bir farkı vardır. Firebug size istemci taraflı aksiyonları sunarken glimpse sunucuda neler olduğunu gösterir. StackExchange’in [MiniProfiler](http://miniprofiler.com/)‘ını biliyorsanız onun gelişmiş ve genişletilebilir versiyonu olarak da düşünebilirsiniz.

![Glimpse Nedir?]({{ site.baseurl }}/images/glimpse/glimpselogo.png)

Glimpse açık kaynak kodlu bir projedir. Asp.Net için geliştirilmiştir ancak port edilmiş versiyonlarıda (Php gibi) vardır.

### Kurulum

<div style="background-color: #202020; border: 4px solid silver; border-radius: 5px; -moz-border-radius: 5px; -webkit-border-radius: 5px; box-shadow: 2px 2px 3px #6e6e6e; color: #e2e2e2; display: block; font: 1.5em 'andale mono', 'lucidaconsole', monospace; line-height: 1.5em; overflow: auto; padding: 15px;">PM> Install-Package Glimpse</div>

Glimpse’i nuget paket yöneticisi üzerinden pratik bir şekilde kurabilirsiniz. Eğer nuget paket yöneticinizde glimpse’i aratırsanız Glimpse.Mv5,Glimpse.Mv4,Glimpse.ASP.Net(webform için),.. gibi paketler göreceksiniz. Projenize uygun olanı kurabilirsiniz.

Glimpse’in mimarisi `HttpHandlers` ve `HttpModule` üzerine kuruludur. Dolayısıyla ilk kurulumda otomatik olarak web.config dosyamıza bazı eklemeler yapacaktır.

Glimpse ilk kurulumunda uzak bilgisayarlardan çalışmayacak şekilde gelir. Glimpse’i test.alanadiniz.com gibi bir test ortamınızdan çalıştırmak için web.config dosyanızdaki runtimePolicies’in altına

`<ignoredTypes>  
 <add type=”Glimpse.AspNet.Policy.LocalPolicy,Glimpse.AspNet”/>  
 </ignoredTypes>`

kodunu eklemelisiniz.

Glimpse’i kullanmaya başlamak için /glimpse.axd adresine gitmeniz yeterli. Sizi aşağıdaki gibi bir ekran karşılayacaktır.

![glimpse.axd]({{ site.baseurl }}/images/glimpse/glimpseDashboard.png)

Başlamak için “Turn Glimpse On” butonuna basmamız yeterli. Şimdi web uygulamamızın herhangi bir sayfasına dönebiliriz.

Her şey yolunda gitmişse sayfamızın sağ alt köşesinde HUD panelini görebilirsiniz.

### HUD Panel

Bu şık panel bize sayfa ile ilgili özet bilgi verir. İlgili sayfanın hazırlanması için geçen toplam süreyi ve bunun ne kadarın nerede harcandığını – DB queries 195 ms, wire 311 ms, gibi- gösterir. Ayrıca sağ alt tarafta da ajax request’leri görebilirsiniz. Glimpse’in güzel yanlarından birisi de socket teknolojisini kullandığı için sayfa yüklendikten sonra oluşan olaylar anlık panele düşmektedir.

![glimpse-hud-panel]({{ site.baseurl }}/images/glimpse/glimpsePanel.png)

Özellikle kompleks web uygulamalarında performansın sürekli gözlenmesi gerekmektedir. Bunun için çeşitli çözümler vardır. Gerek Newrelic, Appdynamics gibi APM araçları gerekse dotTrace, yourkit gibi uygulama profiler araçları. Saydığımız çözümler daha çok geliştirmesi tamamlanmış uygulamalara yönelik.

Glimpse geliştirme aşamasında uygulamanızın request başına maliyetini parça parça incelemenize olanak tanır. Her sunucu isteği için arka tarafta olan -db query’leri, session, .. – bütün aksiyonları görmemizi sağlar. Bu sayede yeni yazdığınız bir linq için ORM’nizin nasıl bir sql sorgusu ürettiğini, sorgunun ne kadar sürdüğünü ya da ilgili sayfanın hangi View dosyasından geldiğini hatta ilgili view dosyasınnı önbellek’ten mi geldiğini yoksa disk’ten mi okunduğunu görebilirsiniz.

### Glimpse Panel

Açmak için sağ alttaki Glimpse simgesine tıklamanız yeterli. Bu panel tarayıcı eklentisi değildir. Sayfanın içerisine iliştirilmiş javascript vs css ‘ten ibarettir. Glimpse’e herhangi bir eklenti kurmamışsanız aşağıdaki SQL sekmesi görünmeyecektir. Eklentilere sonra değineceğiz.

![glimpse-panel]({{ site.baseurl }}/images/glimpse/glimpsePanel2.png)

### Configuration

Bu sekmede uygulamanıza ait bütün ayarları bulabilirsiniz. Test ortamınızın uzakta olduğunu düşünün. O an uygulamanızın hangi database’e baktığını, hangi ayarların aktif olduğunu kontrol etmek için bilgisayara bağlanıp web.config dosyanıza bakmak yerine bu sekmeyi kullanabilirsiniz.

### Environment

Uygulamanızın çalıştığı bilgisayarın işletim sistemi versiyonu, Ram’i, IIS versiyonu, kullandığı kod kütüphaneleri, hatta bu kütüphanelerin GAC’ten mi geldiği bilgisine kadar her şey bu sekmede.

### Routes

Eğer Phil Haack’in [RouteDebugger](https://www.nuget.org/packages/routedebugger/)‘ını biliyorsanız çalışma mantıkları onunla aynı. Uygulamanın bütün Route kayıtlarını göstermekle birlikle ilgili request’in hangi route ile eşleştiğini gösterir. Binlerce Route’un tanımlandığı uygulamalarda şaşılır derecede faydası vardır.

### Trace

Bir kod bloğunun çalıştığını ya da hangi değerlerle çalıştığını görmek isteriz. Eğer unit test yazmıyorsak bu sorunu debug ile çözeriz ya da log atarız. Bu durumlarda Trace’i kullanabilirsiniz. Log’larınızı okumak için başka bir yere bakmanıza gerek olmadan sayfanızdan görebilirsiniz.

Trace yazmak için `System.Diagnostics.Trace` altındaki `Write,TraceInformation,TraceWarning,TraceError` metodlarını kullanabilirsiniz.

### Eklentiler

![glimpse-plugins]({{ site.baseurl }}/images/glimpse/glimpsePackages.png)

Glimpse’in en güzel tarafı hali hazırda bir çok [eklentisinin](http://getglimpse.com/Extensions/) olması diyebiliriz. Eklentileri yine nuget üzerinden kuruyoruz. Çoğunlukla eklentilerin aktif olması için kurmak yeterlidir. Ancak bazı eklentilerin -Linq2Sql, ElasticSearch, ..- çalışmaları için ufak geliştirmeler yapmak gerekir.

### Kendi Eklentinizi Yazın

> Eğer aradığınız eklenti henüz glimpse’te yoksa siz yazın.

Bizim böyle bir ihtiyacımız oldu ve bir tane yazdık. Koduna [buradan](https://github.com/onuralp/Glimpse.ElasticSearch), nuget paketinede aşağıdan erişebilirsiniz.

Eklenti basitçe uygulamanızın nasıl bir [ElasticSearch](http://www.elasticsearch.org/) sorgusu ürettiğini ve bu sorgunun ne kadar sürede çalıştığını görmenize yarıyor.

<div style="background-color: #202020; border: 4px solid silver; border-radius: 5px; -moz-border-radius: 5px; -webkit-border-radius: 5px; box-shadow: 2px 2px 3px #6e6e6e; color: #e2e2e2; display: block; font: 1.5em 'andale mono', 'lucidaconsole', monospace; line-height: 1.5em; overflow: auto; padding: 15px;">PM> Install-Package Glimpse.ElasticSearch</div>

### Güvenlik

Peki bu kadar bilgiyi paylaşmak güzel olduğu kadar korkunç değil mi? Kötü niyetli birisinin glimpse’e kesinlikle erişmemesi gerekiyor. Glimpse projeye kurulurken `GlimpseSecurityPolicy.cs` adında içi tamamen yoruma alınmış bir dosya ekler. Bu dosyayı ihtiyacınıza göre düzenleyerek glimpse’e kimlerin erişebileceğini ayarlayabilir ya da test ortamı dışında çalışmasını engelleyebilirsiniz.

Web.config dosyanızdaki “Glimpse.axd” geçen yerleri değiştirerek kendinize özel bir url elde edebilirsiniz. info.axd vs..
