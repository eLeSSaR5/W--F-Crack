# WiFiCrack

WiFiCrack, WPA(2) ağlarıyla ilişkili bazı güvenlik açıklarını basit ve verimli bir şekilde kırmayı göstererek ortaya koyuyor. WPA(2) el sıkışmalarıyla ilişkili gerekli Wi-Fi paketlerini yakalar ve ardından karma parolayı çıkarmaya çalışmak için [hashcat](https://github.com/hashcat/hashcat) kullanır. Senaryo eğitim amaçlıdır ve kötüye kullanılmamalıdır.


## Önkoşullar

[Xcode](https://itunes.apple.com/us/app/xcode/id497799835?l=tr&mt=12) yüklü olmalıdır. Bekleyen diğer gereksinimleri yüklemeniz gerekecek:

| Command | Installation |
| --- | --- |
| `hashcat` | Manuel kurulum: `brew install hashcat`| komutunu çalıştırarak [brew](https://brew.sh) aracılığıyla yükleyin.
| `mergecap` | Manuel kurulum: [Wireshark](https://www.wireshark.org) uygulaması (v2.6.12) ile birlikte gelir |
| `./hashcat-utils/src/cap2hccapx.bin` | Komut dosyası çalıştırıldığında otomatik yükleme seçeneği |

**Not:** Ayrıca hashcat için bir kelime listesi sağlamanız gerekecektir.

**Not:** Komut dosyası, "bash" kabuğunu kullanırken macOS Catlaina ile başarıyla test edilmiştir. "zsh" bazı sorunlara neden olabilir

## Kullanım

#Şununla indir:
```
git clone https://github.com/phenotypic/WiFiCrack.git
```

Aynı dizinden şununla çalıştırın:
```
bash WiFiCrack.sh
```

TKomut dosyasının kullanımı oldukça kolaydır, yukarıdaki komutu kullanarak çalıştırın ve istendiğinde 'sudo' şifrenizi girin. İşte ekleyebileceğiniz bazı bayraklar:

| Flag | Başlık |
| --- | --- |
| `-h` | Yardım: Mevcut tüm bayrakları göster |
| `-k` | Sakla: Yakalanan tüm paket dosyalarını sakla (varsayılan olarak oturumun sonunda silinir) |
| `-a` | Uyarı: Başarılı crack uyarısını kapatın |
| `-w <wordlist>` | Kelime listesi: Bir kelime listesi yolunu manuel olarak tanımlayın (komut dosyası size aksini sorar) |
| `-i <interface>` | Arayüz: Wi-Fi arayüzünü manuel olarak ayarlayın (komut dosyası normalde doğru arayüzü otomatik olarak algılamalıdır) |
| `-d <device>` | Cihaz: Hashcat için 'cihazları' manuel olarak tanımlayın |

Komut dosyasını çalıştırdıktan sonra, kırılacak bir ağ seçmeniz istenecektir.

Bir ağ seçiminin ardından, hedef ağda bir el sıkışma gerçekleşene kadar (yani bir cihazın ağa (yeniden) bağlanması için) bir süre beklemeniz gerekebilir, ancak bu, bir [yetki doğrulama saldırısı] gerçekleştirilerek hızlandırılabilir. (https://en.wikipedia.org/wiki/Wi-Fi_deauthentication_attack).

Bir el sıkışma yakalandığında, WiFiCrack, Wi-Fi şifresini çıkarmak için "hashcat"i başlatır. Bu adım, işlem gücünüz de dahil olmak üzere bir dizi faktöre bağlı olarak biraz zaman alabilir. Başarılı olursa, size parola sunulacaktır, aksi takdirde, ele geçirmeye karşı başka bir tür saldırı gerçekleştirmek isterseniz WiFiCrack el sıkışmayı dizininde tutacaktır.

## Yapılacak Listesi

- [ ] Kimlik doğrulama saldırısını ana komut dosyasına entegre edin
- [ ] Daha fazla "hashcat" saldırı seçeneği sağlayın (ör. kaba kuvvet)
