# DevOps İçeriği — Bölüm 1: VM Setup (Vagrant & VirtualBox)

Bu repo,**VM Setup** bölümünde yapılanların uygulamalı özetidir.
Tüm komutlar Windows 11 üzerinde Git Bash ile gerçekten çalıştırılmış, çıktılar bu dokümana birebir eklenmiştir.

> **Ortam:** Windows 11 Pro · VirtualBox 7.2.6 · Vagrant 2.4.9 · Git Bash

---

## İçindekiler

1. [Kurulan Araçlar](#1-kurulan-araçlar)
2. [Vagrant Nedir?](#2-vagrant-nedir)
3. [İlk Sanal Makine: CentOS Stream 9](#3-ilk-sanal-makine-centos-stream-9)
4. [Makine İçinde: SSH, root, kapatma](#4-makine-i̇çinde-ssh-root-kapatma)
5. [Yok Etme ve Yeniden Kurma](#5-yok-etme-ve-yeniden-kurma)
6. [İkinci Makine: Ubuntu 22.04](#6-i̇kinci-makine-ubuntu-2204)
7. [Tüm Makineleri Yönetme](#7-tüm-makineleri-yönetme)
8. [Mac M1/M2/M3 Notu](#8-mac-m1m2m3-notu)
9. [Komut Özeti (Cheat Sheet)](#9-komut-özeti-cheat-sheet)

---

## 1. Kurulan Araçlar

| Araç | Sürüm | Görevi |
|---|---|---|
| **Oracle VirtualBox** | 7.2.6 | Hypervisor — sanal makineleri gerçekten çalıştıran program |
| **Vagrant** | 2.4.9 | VirtualBox'ı komut satırından yöneten otomasyon aracı |
| **Git Bash** | 2.55 | Windows'ta Linux benzeri terminal |

**Windows ön koşulu (VMPrerequisite):** BIOS'ta sanallaştırma (VTx / SVM) açık olmalı.
Sanal makineler sorunsuz çalıştığına göre bu koşul sağlanmış durumda.

---

## 2. Vagrant Nedir?

Sanal makineyi VirtualBox arayüzünden elle kurmak yerine (ISO indir, next-next-finish, kullanıcı oluştur...),
Vagrant ile makine **tek bir metin dosyasından** (`Vagrantfile`) otomatik kurulur:

- **Box** = hazır işletim sistemi imajı. [Vagrant Cloud](https://portal.cloud.hashicorp.com/vagrant/discover)'dan seçilir (ör. `eurolinux-vagrant/centos-stream-9`).
- **Vagrantfile** = makinenin tarifi: hangi box, ne kadar RAM, hangi IP, kurulumda hangi komutlar çalışsın.
- Makine bozulursa `vagrant destroy` + `vagrant up` ile dakikalar içinde aynısı yeniden kurulur.
  **"Kullan-at" (disposable) altyapı** mantığı — Infrastructure as Code'un ilk adımı.

---

## 3. İlk Sanal Makine: CentOS Stream 9

### 3.1 Proje klasörü ve `vagrant init`

```bash
mkdir -p ~/Desktop/vagrant-vms/centos
cd ~/Desktop/vagrant-vms/centos
vagrant init eurolinux-vagrant/centos-stream-9
```

Çıktı:

```text
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
```

`vagrant init` **hiçbir şey indirmez/kurmaz** — klasöre sadece bir `Vagrantfile` koyar.
Dosyadaki tek aktif satır:

```ruby
config.vm.box = "eurolinux-vagrant/centos-stream-9"
```

### 3.2 `vagrant up` — makineyi başlat

```bash
vagrant up
```

İlk çalıştırmada box imajı (~1 GB) indirilir, sonra makine kurulup açılır:

```text
==> default: Importing base box 'eurolinux-vagrant/centos-stream-9'...
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
==> default: Machine booted and ready!
```

- `22 => 2222`: makinenin SSH portu, ana makinenin 2222 portuna yönlendirilir.
- "No guest additions" uyarısı görürsen: hata değildir, yok sayılabilir.

---

## 4. Makine İçinde: SSH, root, kapatma

```bash
vagrant ssh          # makineye bağlan
```

Makine içinde:

```bash
whoami               # -> vagrant   (normal kullanıcı)
pwd                  # -> /home/vagrant
sudo -i              # root'a geç (Vagrant'ta şifresiz sudo)
whoami               # -> root
exit                 # root'tan çık
exit                 # SSH'tan çık, Windows'a dön
```

Gerçek çıktı:

```text
vagrant
/home/vagrant
root
```

Kapatma ve durum:

```bash
vagrant halt         # düzgün kapatma (graceful shutdown)
vagrant status
```

```text
==> default: Attempting graceful shutdown of VM...
Current machine states:

default                   poweroff (virtualbox)
```

VirtualBox Manager açılırsa makine orada **Powered Off** görünür —
Vagrant, VirtualBox'ı arka planda bizim yerimize yönetir.

---

## 5. Yok Etme ve Yeniden Kurma

```bash
vagrant destroy      # onay ister; -f ile onaysız
```

```text
==> default: Forcing shutdown of VM...
==> default: Destroying VM and associated drives...
```

| | `vagrant halt` | `vagrant destroy` |
|---|---|---|
| Makine | Kapanır | **Diskiyle birlikte silinir** |
| Veriler | Korunur | Kaybolur |
| Geri dönüş | `vagrant up` (saniyeler) | `vagrant up` (sıfırdan kurulum) |

`destroy` sonrası `vagrant status` → `not created`. Ama **Vagrantfile durur**;
`vagrant up` aynı makineyi sıfırdan aynı şekilde kurar. Vagrant'ın asıl gücü budur.

İndirilen imajlar silinmez, tekrar kullanılır:

```bash
vagrant box list
```

```text
eurolinux-vagrant/centos-stream-9 (virtualbox, 9.0.48, (amd64))
ubuntu/jammy64                    (virtualbox, 20241002.0.0)
```

---

## 6. İkinci Makine: Ubuntu 22.04

Her makine **kendi klasöründe**, kendi Vagrantfile'ı ile yaşar:

```bash
cd ~/Desktop/vagrant-vms/ubuntu
vagrant init ubuntu/jammy64
vagrant up
vagrant ssh
```

Makine içinde doğrulama:

```text
vagrant
PRETTY_NAME="Ubuntu 22.04.5 LTS"
ubuntu-jammy
```

Artık aynı bilgisayarda **hem CentOS hem Ubuntu** var — ikisi de birer klasör + birer dosyadan ibaret.

---

## 7. Tüm Makineleri Yönetme

Klasör gezmeden bilgisayardaki bütün Vagrant makinelerini görmek:

```bash
vagrant global-status
```

```text
id       name    provider   state    directory
-------------------------------------------------------------------------------
807d21c  default virtualbox running  C:/Users/dynob/Desktop/vagrant-vms/centos
9cb02b4  default virtualbox poweroff C:/Users/dynob/Desktop/vagrant-vms/ubuntu
```

`id` ile herhangi bir klasörden makine yönetilebilir:

```bash
vagrant halt 807d21c
vagrant destroy 9cb02b4
```

---

## 8. Mac M1/M2/M3 Notu

Kursun "VM on MacOS M1 chip" dersi **sadece Apple Silicon Mac** içindir:
Rosetta + Homebrew ile Vagrant + VMware Fusion + ARM box'ları (`spox/ubuntu-arm` vb.).
Windows veya Intel Mac kullanıyorsanız bu ders atlanır — VirtualBox + normal (amd64) box'lar yeterlidir.

---

## 9. Komut Özeti (Cheat Sheet)

| Komut | İşlevi |
|---|---|
| `vagrant init <box>` | Klasöre Vagrantfile koyar (kurulum yapmaz) |
| `vagrant up` | Makineyi kurar/başlatır (box yoksa indirir) |
| `vagrant ssh` | Makinenin içine bağlanır |
| `vagrant status` | Bu klasördeki makinenin durumu |
| `vagrant halt` | Makineyi düzgünce kapatır |
| `vagrant destroy [-f]` | Makineyi diskiyle birlikte siler |
| `vagrant reload` | Yeniden başlatır (Vagrantfile değişikliğini uygular) |
| `vagrant box list` | İndirilen imajları listeler |
| `vagrant global-status` | Bilgisayardaki tüm makineleri listeler |
| `sudo -i` | (VM içinde) root kullanıcısına geçer |
| `history` | Terminalde geçmiş komutları listeler |
