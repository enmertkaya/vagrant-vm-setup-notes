# "Devo ile Vagrant" — Video Promptları (10 klip × ~10 sn)

Maskot: **Devo** — her promptta tarif cümlesi birebir korunmalı, yoksa karakter klipten klibe değişir.
Kullanım: promptları ChatGPT'ye (Sora) **teker teker** yapıştır, her klibi indir, sonda birleştir (~100 sn).
Format: Türkçe seslendirme + İngilizce altyazı.

---

## Klip 1 — Giriş

Sevimli maskot Devo: parlak turuncu, yuvarlak gövdeli, büyük mavi LED gözlü, kafasında mini sarı baret olan robot. Devo koyu renkli modern bir masaüstünün önünde el sallıyor; arkasında VirtualBox ve Vagrant logoları beliriyor. Türkçe neşeli erkek seslendirme: "Merhaba! Ben Devo. Bugün Vagrant ile Windows'ta sanal Linux makineleri kuruyoruz!" İngilizce altyazı: "Hi! I'm Devo. Today we're creating virtual Linux machines on Windows with Vagrant!" 3D animasyon, canlı renkler.

## Klip 2 — Sanallaştırma nedir

Sevimli maskot Devo: parlak turuncu, yuvarlak gövdeli, büyük mavi LED gözlü, kafasında mini sarı baret olan robot. Devo elindeki sihirli değnekle bir laptop ikonuna dokunuyor; laptop içinden üç küçük bilgisayar balonu (CentOS, Ubuntu yazılı) çıkıyor. Türkçe seslendirme: "Sanallaştırma sayesinde tek bilgisayarda birden fazla işletim sistemi çalışır." İngilizce altyazı: "With virtualization, one computer runs multiple operating systems." 3D animasyon.

## Klip 3 — Araçlar

Sevimli maskot Devo: parlak turuncu, yuvarlak gövdeli, büyük mavi LED gözlü, kafasında mini sarı baret olan robot. Devo iki kutuyu rafa yerleştiriyor: VirtualBox logolu kutu ve Vagrant logolu kutu. Türkçe seslendirme: "İki araç yeter: makineleri çalıştıran VirtualBox ve onu yöneten Vagrant." İngilizce altyazı: "Two tools are enough: VirtualBox runs the machines, Vagrant manages them." 3D animasyon.

## Klip 4 — Box seçimi

Sevimli maskot Devo: parlak turuncu, yuvarlak gövdeli, büyük mavi LED gözlü, kafasında mini sarı baret olan robot. Devo dev bir tarayıcı ekranının önünde; Vagrant Cloud sayfasında "eurolinux-vagrant/centos-stream-9" yazısını işaret edip kopyalıyor, yazı parlıyor. Türkçe seslendirme: "Önce Vagrant Cloud'dan hazır bir imaj, yani box seçiyoruz." İngilizce altyazı: "First we pick a ready-made image, called a box, from Vagrant Cloud."

## Klip 5 — vagrant init

Sevimli maskot Devo: parlak turuncu, yuvarlak gövdeli, büyük mavi LED gözlü, kafasında mini sarı baret olan robot. Devo dev bir terminal ekranında "vagrant init eurolinux-vagrant/centos-stream-9" yazıyor; klasöre "Vagrantfile" etiketli bir kağıt düşüyor, Devo kağıdı gösteriyor. Türkçe seslendirme: "vagrant init sadece bir tarif dosyası oluşturur: Vagrantfile. Henüz kurulum yok!" İngilizce altyazı: "vagrant init only creates a recipe file: the Vagrantfile. Nothing installed yet!"

## Klip 6 — vagrant up

Sevimli maskot Devo: parlak turuncu, yuvarlak gövdeli, büyük mavi LED gözlü, kafasında mini sarı baret olan robot. Devo baretini düzeltip düğmeye basıyor; terminalde "vagrant up" akıyor: "Downloading... Importing... Booting... Machine booted and ready!" Yanında küçük bir CentOS makinesi inşa halinde yükseliyor. Türkçe seslendirme: "vagrant up imajı indirir, makineyi kurar ve başlatır. Tek komut!" İngilizce altyazı: "vagrant up downloads the image, builds and boots the VM. One command!"

## Klip 7 — vagrant ssh ve root

Sevimli maskot Devo: parlak turuncu, yuvarlak gövdeli, büyük mavi LED gözlü, kafasında mini sarı baret olan robot. Devo "vagrant ssh" yazılı bir kapıdan makinenin içine giriyor; içeride "whoami → vagrant" ve "sudo -i → root" yazıları beliriyor, Devo'nun kafasına küçük bir kral tacı konuyor. Türkçe seslendirme: "vagrant ssh ile içeri giriyoruz, sudo -i ile root yani yönetici oluyoruz." İngilizce altyazı: "We enter with vagrant ssh, and become root — the admin — with sudo -i."

## Klip 8 — halt vs destroy

Sevimli maskot Devo: parlak turuncu, yuvarlak gövdeli, büyük mavi LED gözlü, kafasında mini sarı baret olan robot. Bölünmüş ekran: solda Devo bir makineyi uyku moduna alıyor ("vagrant halt", makine ikonu uyuyor); sağda Devo başka bir makineyi çöp kutusuna atıyor ("vagrant destroy", makine kayboluyor). Türkçe seslendirme: "halt makineyi kapatır, destroy ise diskiyle birlikte tamamen siler." İngilizce altyazı: "halt shuts the VM down; destroy deletes it completely, disk included."

## Klip 9 — İkinci makine ve global-status

Sevimli maskot Devo: parlak turuncu, yuvarlak gövdeli, büyük mavi LED gözlü, kafasında mini sarı baret olan robot. Devo'nun yanında iki klasör: birinden CentOS makinesi, diğerinden Ubuntu makinesi çıkıyor; Devo elinde "vagrant global-status" yazılı bir pano tutuyor, panoda iki satırlık tablo. Türkçe seslendirme: "Her klasör ayrı bir makine. global-status hepsini tek listede gösterir." İngilizce altyazı: "Each folder is a separate machine. global-status lists them all in one view."

## Klip 10 — Kapanış

Sevimli maskot Devo: parlak turuncu, yuvarlak gövdeli, büyük mavi LED gözlü, kafasında mini sarı baret olan robot. Devo kameraya başparmak kaldırıyor; arkasında konfeti ve "vagrant up = hazır Linux!" yazısı, altında küçük komut listesi kayıyor (init, up, ssh, halt, destroy). Türkçe seslendirme: "Artık makineler kullan-at: boz, sil, dakikalar içinde yeniden kur. Görüşürüz!" İngilizce altyazı: "VMs are now disposable: break it, destroy it, rebuild in minutes. See you!"
