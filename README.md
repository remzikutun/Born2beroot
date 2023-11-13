# Bern2beroot

#### 1.Projeye Genel Bakış
##### Sanal makine nasıl çalışır ?
• Fiziksel bir bilgisayarın üzerinde çalışan ve kendi işletim sistemine sahip gibi davranan bir yazılım uygulamasıdır.<br>

##### İşletim sistemi tercihleri
• Oyun ve uygulama uyumluluğu açısından windows, güvenlik ve maliyet açısından linux ve macOS seçilmelidir.<br>
• NOT:Bu projede bizden Rocky ve Debian işletim sistemlerinden herhangi birini tercih etmemiz istenmiş.<br>

##### Rocky ve Debian arasındaki temel farklar nelerdir.
• Rocky kurumsal kullanıcıları hedefleyen bir dağıtım, Debian özgür yazılım ideallerine odaklanan bir topluluk tarafından geliştirilmektedir.<br>
• Rocky RPM (Red Hat Packege Menager) tabanlı, Debian ise APT (Advanced Package Tool) yaygın olarak kullanılan bir paket yöneticisidir.<br>
• Rocky genellikle 64-bit mimarisi için yaygın, Debian ise x86, x86_64, ARM, MIPS, PowerPC gibi birçok mimariyi destekler.<br>

##### Sanal makinelerin amacı nedir ?
• İzolasyon ve güvenlik açısından önemlidir. Dosya ve uygulamalar arasında bir çeşit duvar oluşturur.<br>
• Çoklu işletim sistemlerini aynı anda çalıştırabilmek.<br>
• Esneklik ve taşınabilirlik.<br>
• Kolay yedeklenebilir ve kurtarılabilir.<br>

##### Aptitude ve Apt arasındaki fark ve AppArmor nedir ?
• Aptitude bir kullanıcı arayüzüne sahip, apt ise basit bir komut satırı aracıdır.<br>
• Aptitude kullanılmayan eski paketleri otomatik olarak temizler, apt temizlemek için ekstra seçeneklere sahiptir.<br>
• AppArmor linux işletim sistemi üzerinde çalışan uygulamaların ve süreçlerin güvenlik politikalarını uygulamak için kullanılan bir güvenlik çerçevesidir.<br>

#### 2.Basit Kurulum
• SSH ile bağlanırken root ile bağlanmaması istenmiş. Bunu test için Terminal açıp "ssh root@localhost -p 4242" komutunu yazarak bağlanıp bağlanmadığı kontrol edilir.<br>
• Seçilen şifre "chage -l kullanıcıadı" komutu ile kontrol edilir.<br>
• UFW hizmetinin başlatıldığı (aktif olduğu) "systemctl status ufw" komutu ile kontrol edilir.<br>
• SSH hizmetinin başlatıldığı (aktif olduğu) "systemctl status ssh" komutu ile kontrol edilir.<br>
• Seçilen işletim sisteminin Debian mı Rocky mi olduğunu "uname -a" komutu ile kontrol edilir.<br>

#### 3.Kullanıcı
• Oturum açma bilgilerini "id" kodu ile kontrol edilir.<br>
• Kullanıcının hangi gruba ait olduğunu öğrenmek için "id kullanıcıadı", "groups", "cat /etc/group | grep kullanıcıadı" ve "cat /etc/group | grep sudo" komutlarından birisi kullanılabilir.<br>
• Kullanıcı oluşturmak için "sudo adduser kullanıcıadı" veya "sudo useradd kullanıcıadı" komutu ile kontrol edilir. Bu iki komuttaki "adduser useradı" ve "useradd useradı" arasındaki tek fark adduser ile ekleme yapıldığında bilgiler ister ve girildikten sonra oluşturur, useradd ile ekleme yapıldığında bilgi istemeden kullanıcıyı oluşturur.<br>
• Grup oluşturmak için "addgroup grupadı" komutu ile oluşturulur.<br>
• Oluşturulan gruba kullanıcıyı eklemek için "usermod -aG groupadı useradı" komutu ile eklenir.<br>
