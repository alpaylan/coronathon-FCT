# Fact Checker's Tool

# Problem

Teknolojinin gelişimiyle birlikte yaşanan gelişmeler kötü niyetli kullanıcılar tarafından suistimal edilmeye devam ediliyor. 

Şu günlerde yaşadığımız Covid-19 Salgını esnasında ortaya çıkan sahte haberlerin insanlar üzerindeki etkisi ise karantinanın getirdiği psikolojik problemler ve paranoyayla birlikte çok daha artmış vaziyette. 

Haber doğrulama organizasyonları bu sahte haberlerle savaşmak için yüksek miktarda efor sarf etseler de sahte haberlerin yayılması çok kısa sürerken bir haberin doğrulanması neredeyse 1 gün sürüyor.

# Çözüm

Twitter, sahip olduğu çok miktarda bot hesabın yanında bilinçsiz ve kötü niyetli kullanıcıların da etkisiyle pek çok sahte haberin yayılmasına katkıda bulunan bir sosyal mecra. 

Biz FCT ile twitter üzerinden elde ettiğimiz verileri kullanarak haber doğrulama organizasyonlarına 3 adet imkan sunuyoruz.

- Yanlış haberlerin ortaya çıkması durumunda organizasyona alarm verilmesi.
- Organizasyonun ortaya çıkan bir haberle ilgili güvenilirlik ve kaynak sorgulaması yapması.
- Organizasyonun ortaya çıkan haberin kaynağıyla ilgili sorgulama yapabilmesi, kaynağın kendi güvenilirliğinin test edilebilmesi.


Aynı şekilde sorgulayan, doğruyu öğrenmek isteyen bireylerimize de 2 farklı imkan sunuyoruz.

- Ortaya çıkan yeni doğrulanmış veya yalanlanmış haberlerle ilgili anlık bilgi sahibi olabilme şansı.
- Merak ettikleri haberleri sorgulayabilme, doğruluklarıyla ilgili bilgi alabilme şansı.


# Nasıl

Çözümümüzün çalışma mantığı aşağıdaki gibi:

Twitter hesaplarının attıkları tweetlerin teyit.org makaleleri ve sağlık bakanlığı açıklamalarıyla paralleliklerini inceleyip, yalan haber(makalelere/açıklamalara zıt) yayan hesapların güvenilirlik puanlarının düşürülmesi, doğru haberleri yayan hesapların güvenilirlik puanlarının yükselmesine dayalı bir sistem. Sonrasında twitter hesaplarının kendi iç dinamiklerine(follow/retweet), hesapların özelliklerine(açılma tarihi, tweet sıklığı) ve geleceğe yönelik tweetlerinin yine teyit edilmiş haberlerle olan korelasyonuna göre hesapların puanlarını dinamik bir şekilde günden güne güncelliyoruz. 

Düşük puanlı hesaplar arasında yayılmaya başlayan haberlerin yalan olma ihtimalini göz önüne alıp bunları müşterimiz olan haber doğrulama sistemlerine bildiriyoruz. Aynı şekilde sorgulanan haberle veya twitter profiliyle ilgili yorum yapabiliyoruz.

Sistemimiz HITS(Hubs and Authorities) Algoritması ile çeşitli NLP Algoritmaları üzerinden işliyor.

HITS Algoritmasında Twitter hesaplarını güvendiğimiz kaynaklar(authorities) ve diğerleri(hubs) olarak 2'ye ayırıyoruz. 

Otoriteler Covid-19 kapsamında bizim için: Sağlık Bakanlığı, WHO, Teyit.Org, İl Sağlık Müdürlükleri...

Diğer hesapların attıkları tweetlerin bu otoritelerin açıklamalarıyla olan paralleliklerini-zıtlıklarını ölçmek için bazı doğal dil işleme yöntemleri kullanıyoruz.

Sistem aşağıdaki gibi işliyor:

Teyit.Org Makalesi --> Makale Özeti --> Makale Duruşu

İlk geçiş için metin özetleyici(text summarization), ikinci geçiş içinse duruş çıkarımı(stance detection) kullanıyoruz. 

Aynı şekilde;

Kişinin Tweeti --> Tweetin Duruşu

Tweetin Duruşu ile makalenin duruşu karşılaştırıldıktan sonra bu iki metnin korelasyon ölçümleri yapılıyor.

Metinlerde pozitif korelasyon => Kişinin Güvenilirlik Puanı Artar
Metinlerde negatif korelasyon => Kişinin Güvenilirlik Puanı Azalır

Kişilerin güvenilirlik puanları ilk başta diğer faktörlerle birlikte(hesabın açılma tarihi, tweet sıklığı) hesaplandıktan sonra yalan haberlerle ilişkilendirildikçe düşer, doğru haberlerle ilişkilendirildikçe yükselir, sistem parametrik olarak istikrara dayalı çalışır.

## Yanlış Haber Alarmı Verme

Güvenilmeyen hesaplar arasında yeni bir haber ortaya çıkmaya başladığında sistem haber doğrulayıcılara ve abone kullanıcılara haber verir.

## Haber Sorgulama

Sistemde bir haber sorgulandığında, sistem o haberle ilgili tweetleri inceler, eğer otoritelerden gelen bir tweet varsa kesin bir sonuç vermekle birlikte diğer şartlarda ihtimallerle yanıt verir, şeffaf bir şekilde bu sonuçların sebeplerini güvenilirlik kıstasları üzerinden açıklar.

## Kaynak Sorgulama

Haber doğrulayıcılar, bir haberin kaynağını sistem üzerinden sorgulayabilir. Twitterda haberin ilk nerede, ne zaman ortaya çıktığı, bu hesaplar arasında bir bağlantı(güvenilirlik, lokasyon...) olup olmadığını öğrenebilir.

## Kişi Güvenilirlik Sorgulama

Haber doğrulayıcılar kendi buldukları kaynakların doğruluklarını sistem üzerinden sorgulayabilirler, sistem şeffaf bir şekilde bu sonuçların sebeplerini güvenilirlik kıstasları üzerinden açıklar.