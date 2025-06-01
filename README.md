print("Merhaba GitHub!")
import os
import datetime

NOTLAR_DOSYASI = "notlar.txt"

def menu_goster():
    print("\n NOT DEFTERİ UYGULAMASI")
    print("----------------------------")
    print("1. Notları Listele")
    print("2. Yeni Not Ekle")
    print("3. Not Sil")
    print("4. Çıkış")
    print("----------------------------")

def notlari_yukle():
    if not os.path.exists(NOTLAR_DOSYASI):
        return []
    with open(NOTLAR_DOSYASI, "r", encoding="utf-8") as dosya:
        return [satir.strip() for satir in dosya.readlines()]

def notlari_kaydet(notlar):
    with open(NOTLAR_DOSYASI, "w", encoding="utf-8") as dosya:
        for not_ in notlar:
            dosya.write(not_ + "\n")

def notlari_listele(notlar):
    print("\n KAYITLI NOTLAR:")
    if not notlar:
        print("Hiç not yok.")
    for i, not_ in enumerate(notlar, start=1):
        print(f"{i}. {not_}")

def yeni_not_ekle(notlar):
    icerik = input(" Not içeriğini gir: ")
    tarih = datetime.datetime.now().strftime("%Y-%m-%d %H:%M")
    not_ = f"{icerik} (eklenme tarihi: {tarih})"
    notlar.append(not_)
    notlari_kaydet(notlar)
    print(" Not başarıyla eklendi.")

def not_sil(notlar):
    notlari_listele(notlar)
    try:
        silinecek = int(input(" Silmek istediğin notun numarası: "))
        if 1 <= silinecek <= len(notlar):
            silinen = notlar.pop(silinecek - 1)
            notlari_kaydet(notlar)
            print(f" '{silinen}' silindi.")
        else:
            print(" Geçersiz not numarası.")
    except ValueError:
        print(" Lütfen sayı gir.")

def main():
    notlar = notlari_yukle()
    while True:
        menu_goster()
        secim = input(" Seçiminiz (1-4): ")
        if secim == "1":
            notlari_listele(notlar)
        elif secim == "2":
            yeni_not_ekle(notlar)
        elif secim == "3":
            not_sil(notlar)
        elif secim == "4":
            print(" Görüşmek üzere!")
            break
        else:
            print(" Geçersiz seçim, tekrar dene.")

if __name__ == "__main__":
    main()


