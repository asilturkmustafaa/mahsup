# Mahsup — Kurulum (yaklaşık 15 dakika, ücretsiz)

Uygulama tek bir dosyadır (`index.html`). Giriş ve ortak kayıt için Google'ın ücretsiz **Firebase** hizmetini kullanır. Bir kez kurulur; sonra linki herkese verirsiniz.

Firebase ayarı yapılmadan `index.html` açılırsa uygulama **önizleme modunda** çalışır (kayıtlar yalnızca o cihazda kalır).

---

## 1. Firebase projesi açın
1. https://console.firebase.google.com adresine Gmail hesabınızla girin.
2. **Proje oluştur** → ad: `mahsup` → Google Analytics'i kapatın → **Proje oluştur**.

## 2. Web uygulaması ekleyin ve ayar kodunu alın
1. Proje ana sayfasında **</>** (Web) simgesine tıklayın.
2. Takma ad: `mahsup` → **Uygulamayı kaydet** (Hosting kutusunu işaretlemeyin).
3. Ekranda `const firebaseConfig = { apiKey: "...", ... };` şeklinde bir kod çıkar. **Süslü parantez içini** kopyalayın.
4. `index.html` dosyasını Not Defteri ile açın. En üstteki satırı bulun:
   ```
   window.FIREBASE_CONFIG = null;
   ```
   `null` yerine kopyaladığınız bloğu yapıştırın. Örnek:
   ```
   window.FIREBASE_CONFIG = {
     apiKey: "AIza...",
     authDomain: "mahsup-xxxx.firebaseapp.com",
     projectId: "mahsup-xxxx",
     storageBucket: "mahsup-xxxx.appspot.com",
     messagingSenderId: "123...",
     appId: "1:123...:web:abc..."
   };
   ```
   Kaydedin. (Bu bilgiler gizli değildir; güvenliği 5. adımdaki kurallar sağlar.)

## 3. Giriş yöntemlerini açın
**Derleme (Build) → Authentication → Başlayın → Sign-in method**
- **Google** → Etkinleştir → destek e-postası seçin → Kaydet.
- **E-posta/Şifre** → Etkinleştir → Kaydet.

## 4. Veritabanını oluşturun
**Derleme → Firestore Database → Veritabanı oluştur**
- Konum: `eur3 (europe-west)` → **Üretim modunda başlat** → Oluştur.

## 5. Güvenlik kurallarını yapıştırın
Firestore Database → **Kurallar (Rules)** sekmesi → içini tamamen silin → `firestore.rules` dosyasının içeriğini yapıştırın → **Yayınla**.

Bu kurallar şunu garanti eder: bir grubun giderlerini yalnızca o grubun onaylı üyeleri görür; gideri yalnızca giren kişi veya yönetici siler; üye ekleme/çıkarma yalnızca yöneticidedir.

## 6. Uygulamayı internete koyun (link alma)
En kolayı **Netlify Drop** (hesap ücretsiz, sürükle-bırak):
1. https://app.netlify.com/drop adresine gidin, ücretsiz hesap açın.
2. Yalnızca `index.html` dosyasının bulunduğu bir klasörü sayfaya sürükleyin.
3. Size `https://xxxx.netlify.app` gibi bir adres verir. **Site settings → Change site name** ile `mahsup-ofis` gibi bir isim verebilirsiniz.
4. Firebase'e dönün: **Authentication → Settings → Authorized domains → Add domain** → `xxxx.netlify.app` adresini ekleyin. (Bunu yapmazsanız Google girişi "yetkili değil" hatası verir.)

İleride `index.html`'i değiştirirseniz Netlify'da **Deploys** sekmesine yeni klasörü sürükleyin; link aynı kalır.

## 7. Kullanım
1. Linki açın → Google ile giriş yapın → **+ Yeni grup kur** (ör. "Asiltürk Hukuk Ofisi", tür: Ofis).
2. Grup açılınca çıkan **davet kodunu** ya da **davet linkini** WhatsApp'tan paylaşın.
3. Gelenler giriş yapar; link kodu kendisi doldurur → **Katıl**.
4. "Yönetici onayı" açıksa katılım isteği **Grup** sekmesinde görünür → **Onayla**.
5. Herkes kendi giderini **+ Gider ekle** ile girer: tutar, ne için, kim ödedi, kimler arasında bölünecek.
6. **Giderler** sekmesinin en üstünde ay sonu "kim kime ne öder" listesi hazır durur. **Aylık raporu kopyala** ile WhatsApp'a atılır.

Aynı kişi birden fazla grupta olabilir (ofis, aile, doğum günü…). Her grubun kodu ve yöneticisi ayrıdır.

## Ücret
Firebase'in ücretsiz planı (Spark) bu kullanım için fazlasıyla yeter (günde 50.000 okuma). Kredi kartı istenmez.
