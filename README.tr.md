# Unity Android Türkçeleştirme ve Bütünlük Kontrolleri — Anonim Vaka İncelemesi

**Türkçe** | [English](README.md)

> Uygulamanın adı, geliştiricisi, paket kimliği, tam sürümü ve özel dosya yolları bilinçli olarak açıklanmamıştır.
>
> **Gözlemlenen sonuç:** Son Türkçeleştirilmiş derlemenin bir Android cihazında açıldığı ve çevrilmiş metinleri gösterdiği kullanıcı tarafından bildirildi. Bu, tek cihazda raporlanan bir sonuçtur; genel çözüm garantisi değildir.

## Sorun neydi?

Orijinal Unity uygulaması açılıyordu. Metinlerin çevrilip paketin yeniden imzalanmasıyla hazırlanan sürüm Google Play ile ilişkili bir uyarı gösterdi. Başlangıç kodundaki ilk deneysel değişiklik uygulamanın açılışta çökmesine yol açtı. Daha sınırlı bir başlangıç akışı değişikliğinden sonra Türkçeleştirilmiş sürümün açıldığı bildirildi.

Üç önemli ayrım:

- **Geçerli APK imzası**, orijinal geliştiricinin imzasına sahip olmak demek değildir.
- **Dağıtım ve bütünlük denetimleri**, kurulum kaynağını veya uygulamada değişiklik yapılıp yapılmadığını kontrol edebilir.
- **Başlatma bağımlılıkları**, APK yapısal testlerden geçse dahi çalışma sırasında sorun çıkarabilir.

Google'ın [otomatik bütünlük koruması belgelerinde](https://developer.android.com/security/fraud-prevention/environment) bu denetimlerin bazı durumlarda çevrimdışı çalışabildiği de açıklanır.

## İncelemeden çıkan bulgular

| Gözlem | Teknik ders |
| --- | --- |
| Orijinal sürüm açıldı, yeniden paketlenen sürüm Play uyarısı verdi | Yerel imza orijinal dağıtım kimliğini korumaz |
| Kaynak pakette ana APK ve işlemci mimarisine özgü parça vardı | Yalnızca ana APK'yı çıkarmak gerekli kütüphaneleri eksik bırakabilir |
| Çeviri metinleri Unity verisindeydi | Metin değişiklikleri çalıştırılabilir koddan ayrı izlenebilir |
| İlk açılış müdahalesi çökmeye neden oldu | Geniş kapsamlı başlatma değişiklikleri risklidir |
| Daha dar kapsamlı deney kullanıcı cihazında açıldı | Tek bir testten evrensel sonuç çıkarılamaz |
| İki son deneyde çeviri verileri aynıydı | Davranış farkı yeni bir çeviri düzenlemesinden kaynaklanmıyordu |

## Yetkili yazılımlarda işe yarayan hata ayıklama sırası

1. Sorunsuz çalışan orijinali koruyun ve aynı cihazda doğrulayın.
2. Ana APK, işlemciye özel parçalar ve kaynak paketlerini ayırın.
3. Çeviri dosyaları ile yürütülebilir kod değişikliklerini ayrı kaydedin.
4. APK bütünlüğünü ve imzasını doğrulayın; bunları resmî yayın onayı olarak yorumlamayın.
5. Kurulum hatası, Google Play uyarısı, Java hatası, yerel kütüphane çökmesi ve Unity açılış hatasını ayrı değerlendirin.
6. Yalnızca yetkili testlerde cihaz günlüklerini alın, kişisel verileri temizleyin.
7. Başarısız ve başarılı derlemeleri dosya düzeyinde karşılaştırın.
8. Gözlemlerin cihaz ve deneme koşullarıyla sınırlı olduğunu belirtin.

**Önemli:** Play Store'u silmek uygulama içi denetimleri kaldırmayabilir. XAPK'yı tek APK yapabilmek lisans denetimlerini kendiliğinden çözmez.

## Bilinçli paylaşım sınırları

Uygulama kimliği, APK/XAPK, telifli Unity dosyaları, çalıştırılabilir kod, imza anahtarları, doğrudan uygulanabilir yama baytları ve lisans denetimlerini aşmaya yönelik ayrıntılı yönergeler paylaşılmıyor.

Bu belge hukuki danışmanlık veya başkalarının yazılımlarını değiştirme/dağıtma izni değildir. Telif hakkı, lisans ve teknik koruma önlemlerine ilişkin kurallar geçerli olabilir. Herkese açık çeviri yayımlamadan önce gerekli izinleri alın.

Özgün açıklama metni [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) kapsamındadır; üçüncü taraf oyun ve uygulama dosyaları bu lisansa dahil değildir.

## Resmî kaynaklar

- [Android Developers — Automatic integrity protection](https://developer.android.com/security/fraud-prevention/environment)
- [Android Developers — Play App Signing](https://developer.android.com/guide/app-bundle/faq)
- [Android Developers — apksigner](https://developer.android.com/tools/apksigner)
- [Android Developers — Play Integrity API](https://developer.android.com/google/play/integrity/overview)

**Bağımsız topluluk belgesidir; Google, Unity veya herhangi bir uygulama geliştiricisiyle bağlantılı değildir.**
