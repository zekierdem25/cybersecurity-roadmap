# Connection Types and their Function

*Kaynaklar:*
- [NordVPN: Network Connection Types](https://nordvpn.com/tr/blog/network-connection-types/)
- [TechTarget: Ethernet](https://www.techtarget.com/it-infrastructure/definition/Ethernet)
- [HowStuffWorks: Wireless Network](https://computer.howstuffworks.com/wireless-network.htm)
- [HowStuffWorks: Bluetooth](https://electronics.howstuffworks.com/bluetooth.htm)

## 1. Summary (Theory)

### Temel Kavramlar (Core Concepts)
* **Kablolu Bağlantılar (Ethernet):** Yerel (LAN) ve Geniş Alan Ağlarında (WAN) cihazları fiziksel kablolarla (Cat5/6 veya Fiber optik) bağlar. Veriyi iletmek için ağ arayüz kartına (NIC) ihtiyaç vardır. Trafik, yönlendirme cihazları olan Hub'lar (eski ve tüm portlara veri kopyalayan) veya Switch'ler (veriyi akıllıca sadece hedefe ileten) üzerinden akar.
* **Kablosuz Ağlar (Wi-Fi):** Radyo dalgalarını (genellikle 2.4 GHz ve 5 GHz frekansları) kullanarak yönlendiriciler (Router) üzerinden cihazları ağa bağlar. 802.11 (a/b/g/n/ac/ax/be) standartlarıyla sürekli daha hızlı ve eşzamanlı cihaz kapasitesi yüksek hale gelmektedir.
* **Kısa Mesafe ve Kişisel Ağlar (Bluetooth):** Doğrudan cihazdan cihaza (noktadan noktaya) iletişim kuran teknolojidir. Kişisel Alan Ağları (PAN) oluşturur. Düşük enerji tüketimi (Bluetooth LE) ve klasik versiyonları vardır.
* **Diğer Ağlar ve Tüneller:** Kırsal bölgeler için uydu (Starlink vb.) ve mobil cihazlar için hücresel (3G/4G/5G) ağlar kullanılır. VPN (Sanal Özel Ağ) ise bu altyapıların üzerinde trafiği şifreleyerek güvenli bir tünel oluşturur.

### Siber Güvenlikteki Önemi (Cybersecurity Perspective)
Saldırganlar veriyi ele geçirmek için verinin iletildiği "ortamın" zafiyetlerini kullanırlar:
* **Ethernet (Kablolu) Zafiyetleri:** Fiziksel erişim gerektirdiği için Wi-Fi'a göre çok daha güvenlidir. Ancak ağda Switch yerine eski tip Hub kullanılıyorsa, veri ağdaki tüm cihazlara kopyalandığı için araya sızan bir saldırgan özel araçlarla (Packet Sniffer) tüm trafiği kolayca dinleyebilir.
* **Wi-Fi Zafiyetleri:** Radyo dalgaları havadan yayıldığı için menzil içindeki herkes tarafından dinlenebilir. WEP ve ilk WPA gibi eski şifreleme protokolleri saniyeler içinde kırılabilir (Kaba kuvvet saldırıları). Güvenlik için en az AES şifrelemeli WPA2 veya WPA3 kullanılmalıdır. WPS özelliği donanımsal bir arka kapı yarattığı için her zaman kapalı tutulmalıdır. MAC filtreleme bir önlemdir ancak MAC Spoofing ile kolayca aşılabilir.
* **Bluetooth Zafiyetleri:** Eşleştirme (Pairing) süreci kritik bir güvenlik aşamasıdır. Eğer Bluetooth gereksiz yere açık ve "Keşfedilebilir" (Discoverable) durumdaysa, yetkisiz eşleşme ve veri hırsızlığı riskleri doğar. Modern Bluetooth teknolojisi, kullanıcıların takip edilmesini engellemek için MAC adreslerini sürekli değiştirir (randomization).

## 2. Commands (Cheatsheet)

Aşağıdaki komutları kullanarak ağ bağlantılarını ve arayüz durumlarını analiz edebilirsiniz:

```bash
# Windows: Cihazın Ağ Arayüz Kartlarını (NIC), fiziksel MAC adreslerini ve IP adreslerini görmek için kullanılır.
ipconfig /all

# Linux: Cihazın Ağ Arayüz Kartlarını, fiziksel MAC adreslerini ve IP adreslerini görmek için kullanılır.
ip a

# Linux: Wi-Fi arayüzlerinin durumunu, frekans bandını (2.4 veya 5 GHz) ve sinyal gücünü analiz eder.
iwconfig

# Windows / Linux: Ağdaki cihazların IP ve MAC adreslerinin tutulduğu tabloyu listeler (MAC Spoofing saldırılarını tespit etmek için kritiktir).
arp -a

# Linux: Sistemdeki Bluetooth adaptörlerini yönetmek, durumunu görmek ve "keşfedilebilir" modları analiz etmek için kullanılır.
hciconfig
```

## 3. Lab Output (Proof)

### 1. `ipconfig /all` Çıktısı (Ağ Bağdaştırıcıları ve Fiziksel Adresler)
![IP Config All Output](lab_ipconfig_all.png)

### 2. `arp -a` Çıktısı (ARP Tablosu - IP ve MAC Eşleşmeleri)
*Not: Bu tablo, ağdaki diğer cihazları keşfetmek ve potansiyel MAC Spoofing (ARP Zehirlenmesi) saldırılarını analiz etmek için kullanılır.*
![ARP Table Output](lab_arp_a.png)
