# Google-Play-Store-Veri-Temizleme-ve-On-Isleme-Projesi
Google Play Store uygulama verileri üzerinde detaylı bir veri temizleme ve ön işleme projesi. Metin halindeki büyüklük (Size), inceleme (Reviews) ve yükleme (Installs) verilerini analiz edilebilir sayısal formata dönüştürdüm, hatalı kayıtları çıkardım ve tarih değişkenlerinden yeni öznitelikler türettim.

Bu projede, Google Play Store'daki uygulamalara ait verileri içeren karmaşık bir veri setini (17-googleplaystore.csv) analiz edilebilir ve modellemeye uygun bir formata dönüştürmeyi amaçladım. Veri setindeki en büyük zorluk, sayısal olması gereken sütunların (Büyüklük, Yüklemeler, Fiyat) metin formatında, karmaşık ve düzensiz karakterler içermesiydi.

1. Veri Temizleme Amacım ve Yaklaşımım

Amacım, ham veriyi güvenilir içgörüler elde etmek için standart bir yapıya kavuşturmaktı. İzlediğim ana adımlar şunlardır:

Hatalı Kayıtları Ayıklama: Veri setindeki yanlış yapılandırılmış, sayısal bir alanda metin içeren tekil aykırı kayıtları (outlier) tespit edip çıkardım.

Karmaşık Metinleri Dönüştürme: Büyüklük, İncelemeler, Yüklemeler ve Fiyat gibi değişkenleri analize uygun sayısal (integer/float) veri tiplerine çevirdim.

Tarihsel Öznitelik Mühendisliği: "Last Updated" (Son Güncelleme) sütununu kullanarak yeni zaman tabanlı özellikler türettim.

2. İzlediğim Adımlar ve Uygulanan Teknikler

Veri Kalite Kontrolü ve Aykırı Kayıt Temizliği:

İlk olarak eksik değerlerin genel oranını kontrol ettim.

Reviews (İncelemeler) sütununda sayısal olmayan, hatalı girilmiş bir satır tespit ettim (indeks 10472). Bu tekil hatalı kaydı veri setinden çıkardım ve Reviews sütununu tam sayı (int) tipine dönüştürdüm.

Büyüklük (Size) Sütunu Dönüşümü:

Size sütunu 'M' (Megabayt), 'k' (Kilobayt) ve 'Varies with device' (Cihaza göre değişir) gibi değerler içeriyordu.

Öncelikle M ve k karakterlerini temizledim.

Ardından 'Varies with device' değerlerini, analizi zorlaştırmaması için NaN (boş değer) olarak değiştirdim.

Son olarak Size sütununu ondalıklı sayı (float) tipine çevirdim. Bu, farklı birimlerdeki verileri analitik olarak birleştirmek için önemli bir adımdı.

Yüklemeler (Installs) ve Fiyat (Price) Sütunu Temizliği:

Installs sütunu "+" ve "," gibi karakterler; Price sütunu ise "$" simgesi içeriyordu.

Bu iki sütundaki tüm bu gereksiz karakterleri temizlemek için bir döngü kullandım.

Temizliğin ardından, Price sütununu ondalıklı sayı (float), Installs sütununu ise tam sayı (int) tipine dönüştürdüm.

Tarihsel Özellik Mühendisliği (Feature Engineering):

Last Updated (Son Güncelleme) sütununu datetime tipine çevirdim.

Bu tarihten hareketle Gün, Ay ve Yıl olmak üzere üç yeni sayısal öznitelik türettim. Bu, uygulamaların popülerlik veya güncelleme sıklığı gibi zaman serisi analizleri yapmama olanak sağlayacak.

Veri Tipi Ayırma ve Görselleştirme:

Veri setindeki tüm öznitelikleri sayısal ve kategorik olarak iki gruba ayırdım.

Tüm sayısal özelliklerin dağılımlarını KDE (Kernel Density Estimation) grafikleri ile görselleştirdim.

Son olarak, Category bazında Installs toplamlarını gruplayarak hangi uygulama kategorilerinin en çok yüklendiğini inceledim.

Android Sürüm Düzeltmesi:

Android Ver sütununda aralık belirten "-" içeren hatalı veya karmaşık kayıtları temizleyerek veri setinin bütünlüğünü korudum.

3. Sonuç

Tüm bu adımların sonunda, karmaşık metinsel ve hatalı formattaki uygulama verilerini, istatistiksel analizler ve makine öğrenmesi modelleri için hazır, sayısal ve standart bir yapıya dönüştürdüm.

Kullanılan Teknolojiler: Python, Pandas, NumPy, Seaborn, Matplotlib.
