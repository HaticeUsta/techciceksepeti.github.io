---
layout: post
title: OSI Referans Modeli ve Katmanları
description: Modelin amacı, temel olarak ağ üzerindeki iki bilgisayarın iletişiminin nasıl olacağını belirtir.
category: sunum
author: mgunes
tags: [sunum, osi, iso, osi referans modeli]
---
**OSI (Open System Interconnection)** Referans Modeli ilk kez 1978 yılında ortaya çıkmış olup 1984 yılında Uluslararası Standartlar Örgütü (**ISO**) tarafından yeni düzenlemeyle geliştirilmiştir. Modelin amacı, temel olarak ağ üzerindeki iki bilgisayarın iletişiminin nasıl olacağını belirtir. 

**OSI** modelinden önceki dönemde bilgisayar ağları ile haberleşecek cihazların aynı firmanın ürünü olması gerekiyordu. Bir bilgisayar sistemi satın aldığınızda kablosundan ağ kartına, sürücülerinden ağ işletim sistemine kadar her şey o üretici firmaya özel olarak yapılıyordu. Bu sebeple farklı firmaların ürettiği farklı donanım ve işletim sistemine sahip olan cihazların birbirleri ile iletişimi çok zordu. Ayrıca işletmelerce kullanılan ticari ağların çoğunluğu belirli bir işletme tarafından belirli standartlara _oturtulmamış_ teknolojiyle oluşturulmaktaydı. Bu ağların özellikleri, çoğunlukla yalnızca o üreticinin donanımının kullanılmasına izin verecek (ya da en azından başka ürünlerin bağlanmasını zorlaştıracak) biçimde tanımlanmıştı. Bu ortamdan dolayı iletişimin daha global olması adına **OSI** referans modeli, çeşitli üreticilerin ürünlerinin bağlanabileceği bir ağ için, bir sektörü etkinliği olarak ortaya çıkmıştır. Dolayısı ile **Open System Interconnection** diye adlandırılmasının sebebi budur.

**OSI** modeli 7 katmandan oluşmaktadır. İletişim kurallarını belirleyen Protokoller bu katmanların içerisindedir. Her bir katman kendine özgü içerdiği protokolleri kullanır. Dolayısıyla **OSI** modeline protokoller yığını diye biliriz.

*   Application Layer
*   Presentation Layer
*   Session Layer
*   Transport Layer
*   Network Layer
*   Data Link Layer
*   Physical Layer

Bilgi hedef cihazdan kaynak cihaza doğru iletilirken 7\. Katman olan Application Katmanından 1.Katman (Physical Layer) yönünde hareket eder. Kısaca katmanlardan bahsedecek olursak;

**Application Layer;** Kullanıcıya en yakın olan katman olup uygulamaların internet üzerinde çalışmasını sağlayan katmandır.

**Presentation Layer;** Yollanan verinin karşı bilgisayar tarafından anlaşılır formatta olmasını sağlar.

**Session Layer;**Uygulamalar arasındaki bağlantıları kurar, yönetir ve sonlandırır.

**Transport Layer;** TCP ve UDP protokollerini kullanarak veri hata kontrolü ve güvenli ulaşımından sorumlu olan katmandır.

**Network Layer;** IP protokolünü kullanarak ağ üzerindeki bağlantıyı sağlar ve yönlendirir.

**Data Link Layer;** Donanım katmanına erişmek ve kullanmak ile ilgili kuralları belirler.

**Physical Layer;** Verinin kablo üzerinde fiziksel yapıyı tanımlar.

Sunumda Katmanlardan ve kullandığı protokollerden özetle bahsedilmektedir.

<iframe src="//www.slideshare.net/slideshow/embed_code/40758216" width="720" height="540" frameborder="0" marginwidth="0" marginheight="0" scrolling="no"></iframe>