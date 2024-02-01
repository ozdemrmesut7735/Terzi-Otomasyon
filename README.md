
#include <iostream>
#include <cstring>

using namespace std;

const int MAX_SIPARIS_SAYISI = 100;

struct SiparisDetayi {
    char urunAdi[100];
    int adet;
    float fiyat;
};

struct Siparis {
    char musteriAdi[100];
    char musteriSoyadi[100];
    char telefon[20];
    SiparisDetayi detay;
};

Siparis siparisler[MAX_SIPARIS_SAYISI];
int siparisSayisi = 0;

void SiparisAl() {
    if (siparisSayisi < MAX_SIPARIS_SAYISI) {
        Siparis yeniSiparis;
        cout << "Musteri Adi: ";
        cin >> yeniSiparis.musteriAdi;
        cout << "Musteri Soyadi: ";
        cin >> yeniSiparis.musteriSoyadi;
        cout << "Telefon: ";
        cin >> yeniSiparis.telefon;
        cout << "Urun Adi: ";
        cin >> yeniSiparis.detay.urunAdi;
        cout << "Adet: ";
        cin >> yeniSiparis.detay.adet;
        cout << "Fiyat: ";
        cin >> yeniSiparis.detay.fiyat;

        siparisler[siparisSayisi] = yeniSiparis;
        siparisSayisi++;

        cout << "Siparis alindi." << endl;
    } else {
        cout << "Maksimum siparis sayisina ulasildi." << endl;
    }
}

void SiparisListele() {
    if (siparisSayisi > 0) {
        for (int i = 0; i < siparisSayisi; ++i) {
            cout << "Musteri Adi: " << siparisler[i].musteriAdi << " " << siparisler[i].musteriSoyadi << endl;
            cout << "Telefon: " << siparisler[i].telefon << endl;
            cout << "Urun Adi: " << siparisler[i].detay.urunAdi << endl;
            cout << "Adet: " << siparisler[i].detay.adet << endl;
            cout << "Fiyat: " << siparisler[i].detay.fiyat << endl;
            cout << "-----------------------" << endl;
        }
    } else {
        cout << "Siparis bulunamadi." << endl;
    }
}

void SiparisSil() {
    char silinecekAd[100];
    char silinecekSoyad[100];
    
    cout << "Silinecek musteri adini girin: ";
    cin >> silinecekAd;
    cout << "Silinecek musteri soyadini girin: ";
    cin >> silinecekSoyad;

    bool bulundu = false;

    for (int i = 0; i < siparisSayisi; ++i) {
        if (strcmp(siparisler[i].musteriAdi, silinecekAd) == 0 && strcmp(siparisler[i].musteriSoyadi, silinecekSoyad) == 0) {
            // Silinecek siparisi listeden çıkar
            for (int j = i; j < siparisSayisi - 1; ++j) {
                siparisler[j] = siparisler[j + 1];
            }
            siparisSayisi--;
            bulundu = true;
            cout << "Siparis silindi." << endl;
            break;
        }
    }

    if (!bulundu) {
        cout << "Siparis bulunamadi." << endl;
    }
}


int main() {
    char secim;
    do {
        cout << "1. Siparis al" << endl;
        cout << "2. Siparisleri listele" << endl;
        cout << "3. Siparis sil" << endl;
        cout << "4. Cikis" << endl;
        cout << "Seciminizi yapin: ";
        cin >> secim;

        switch (secim) {
            case '1':
                SiparisAl();
                break;
            case '2':
                SiparisListele();
                break;
            case '3':
                SiparisSil();
                break;
            case '4':
                cout << "Programdan cikiliyor..." << endl;
                break;
            default:
                cout << "Gecersiz secim. Tekrar deneyin." << endl;
        }
    } while (secim != '4');

    return 0;
}

