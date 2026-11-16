ÖDEV 3 - Python'a Giriş ve Temel Programlama Notları

Ad Soyad: Efekemal Çalık

Öğrenci No: 24014036

BÖLÜM 2.1: Python Diline Giriş ve Temel Konular

1. Data Types (Veri Tipleri)

Nesne türüdür.

int: Tam sayıları ifade eder (Örn: 10, -5, 24014036).

float: Ondalıklı, kesirli sayıları ifade eder (Örn: 3.14, 9.81).

str: Metin ifadelerini tutar, tırnak içinde yazılır (Örn: "Efekemal", "YODA IHA").

bool: Mantıksal değerlerdir; sadece True (Doğru) veya False (Yanlış) değerini alır.

list: Birden fazla veriyi sıra numarasıyla (index) tutabildiğimiz, değiştirilebilir koleksiyonlardır (Örn: [1, 2, 3, "IHA"]).

tuple: Listelere benzer ancak oluşturulduktan sonra elemanları değiştirilemeyen (değişmez/immutable) yapılardır (Örn: (0, 0, 100)).

dict: Anahtar-değer (key-value) mantığıyla çalışan, verileri etiketleriyle sakladığımız yapılardır (Örn: {"isim": "Efekemal", "no": 24014036}).

2. Conditionals (if-elif-else)

Durumlara göre karar vermemize yarar.

Nasıl kullanılır?

pil = 18
if pil < 20:
    print("DİKKAT: Kritik batarya seviyesi.")
elif pil < 50:
    print("Uyarı: Batarya yarıdan az")
else:
    print("Batarya durumu okey")


3. Loops (Döngüler: for ve while)

# FOR DÖNGÜSÜ
alisveris_listesi = ["Elma", "Ekmek", "Süt"]

for urun in alisveris_listesi:
    print("Sepete eklendi:", urun)

# WHILE DÖNGÜSÜ
cuzdan_para = 50

while cuzdan_para > 10:
    print(f"Cüzdanda {cuzdan_para} TL var, harcamaya devam.")
    cuzdan_para -= 15 
    
print("Para 10 TL'nin altına düştü, durduruldu!")


4. Functions (Fonksiyonlar)

def iki_sayiyi_topla(sayi1, sayi2):
    return sayi1 + sayi2

sonuc = iki_sayiyi_topla(10, 25)
print("Toplam:", sonuc)


5. Class (Sınıflar)

class Araba:
    def __init__(self, marka, renk):
        self.marka = marka
        self.renk = renk

    def calistir(self):
        print(f"{self.marka} marka {self.renk} araba çalıştırıldı.")

arac = Araba("Toyota", "Beyaz")
arac.calistir()


BÖLÜM 2.2: Uygulama Projeleri

1. Kelime Sayacı Programı

def kelime_analizi_yap():
    metin = input("Metin giriniz: ")
    metin_kucuk = metin.lower()
    kelimeler = metin_kucuk.split()
    toplam_kelime = len(kelimeler)
    toplam_karakter = len(metin)
    en_uzun_kelime_boyu = 0
    if toplam_kelime > 0:
        en_uzun_kelime_boyu = max(len(k) for k in kelimeler)
        
    kelime_sayimlari = {}
    for kelime in kelimeler:
        if kelime in kelime_sayimlari:
            kelime_sayimlari[kelime] += 1
        else:
            kelime_sayimlari[kelime] = 1
            
    print("\n--- METİN ANALİZ RAPORU ---")
    print(f"Toplam Kelime Sayısı: {toplam_kelime}")
    print(f"Toplam Karakter Sayısı (Boşluk Dahil): {toplam_karakter}")
    print(f"En Uzun Kelimenin Karakter Uzunluğu: {en_uzun_kelime_boyu}")
    print("\nKelime Tekrar Sayıları:")
    for kelime, sayi in kelime_sayimlari.items():
        print(f"'{kelime}': {sayi} kez geçiyor")

if __name__ == "__main__":
    kelime_analizi_yap()


2. Basit Banka Hesap Yönetimi Programı

class Hesap:
    def __init__(self, ad_soyad, hesap_no, baslangic_bakiyesi=0.0):
        self.ad_soyad = ad_soyad
        self.hesap_no = hesap_no
        self.bakiye = baslangic_bakiyesi

    def bakiye_goruntule(self):
        print(f"\n[Bakiye Bilgisi] {self.ad_soyad}, Hesap No: {self.hesap_no}")
        print(f"Güncel Bakiyeniz: {self.bakiye:.2f} TL")

    def para_yatir(self, miktar):
        if miktar > 0:
            self.bakiye += miktar
            print(f"\n[Başarılı] {miktar:.2f} TL hesaba yatırıldı.")
            self.bakiye_goruntule()
        else:
            print("\n[Hata] Yatırılacak tutar 0'dan büyük olmalıdır!")

    def para_cek(self, miktar):
        if miktar > 0:
            if self.bakiye >= miktar:
                self.bakiye -= miktar
                print(f"\n[Başarılı] {miktar:.2f} TL hesaptan çekildi.")
                self.bakiye_goruntule()
            else:
                print(f"\n[Hata] Yetersiz bakiye! Mevcut bakiyeniz: {self.bakiye:.2f} TL")
        else:
            print("\n[Hata] Çekilecek tutar 0'dan büyük olmalıdır!")

if __name__ == "__main__":
    print("--- YODA BANK HESAP YÖNETİMİ ---")
    kullanici_adi = input("Hesap Sahibi Adı Soyadı: ")
    kullanici_no = input("Hesap Numarası: ")
    aktif_hesap = Hesap(kullanici_adi, kullanici_no, baslangic_bakiyesi=500.0)
    
    while True:
        print("\n--- İŞLEM MENÜSÜ ---")
        print("1 - Bakiye Görüntüle")
        print("2 - Para Yatır")
        print("3 - Para Çek")
        print("4 - Çıkış")
        secim = input("Yapmak istediğiniz işlemin numarasını giriniz (1-4): ") 
        if secim == "1":
            aktif_hesap.bakiye_goruntule()
        elif secim == "2":
            tutar = float(input("Yatırılacak miktar (TL): "))
            aktif_hesap.para_yatir(tutar)
        elif secim == "3":
            tutar = float(input("Çekilecek miktar (TL): "))
            aktif_hesap.para_cek(tutar)
        elif secim == "4":
            print("\nSistemden çıkılıyor. İyi günler dileriz!")
            break
        else:
            print("\n[Hata] Geçersiz seçim yaptınız, lütfen 1 ile 4 arasında bir değer giriniz.")
