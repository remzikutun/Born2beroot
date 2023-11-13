# Bern2beroot

## 1.Projeye Genel Bakış
#### Sanal makine nasıl çalışır ?
→ Fiziksel bir bilgisayarın üzerinde çalışan ve kendi işletim sistemine sahip gibi davranan bir yazılım uygulamasıdır.<br>

#### İşletim sistemi tercihleri
→ Oyun ve uygulama uyumluluğu açısından windows, güvenlik ve maliyet açısından linux ve macOS seçilmelidir.<br>
→ NOT:Bu projede bizden Rocky ve Debian işletim sistemlerinden herhangi birini tercih etmemiz istenmiş.<br>

#### Rocky ve Debian arasındaki temel farklar nelerdir.
→ Rocky kurumsal kullanıcıları hedefleyen bir dağıtım, Debian özgür yazılım ideallerine odaklanan bir topluluk tarafından geliştirilmektedir.<br>
→ Rocky RPM (Red Hat Packege Menager) tabanlı, Debian ise APT (Advanced Package Tool) yaygın olarak kullanılan bir paket yöneticisidir.<br>
→ Rocky genellikle 64-bit mimarisi için yaygın, Debian ise x86, x86_64, ARM, MIPS, PowerPC gibi birçok mimariyi destekler.<br>

#### Sanal makinelerin amacı nedir ?
→ İzolasyon ve güvenlik açısından önemlidir. Dosya ve uygulamalar arasında bir çeşit duvar oluşturur.<br>
→ Çoklu işletim sistemlerini aynı anda çalıştırabilmek.<br>
→ Esneklik ve taşınabilirlik.<br>
→ Kolay yedeklenebilir ve kurtarılabilir.<br>

#### Aptitude ve Apt arasındaki fark ve AppArmor nedir ?
→ Aptitude bir kullanıcı arayüzüne sahip, apt ise basit bir komut satırı aracıdır.<br>
→ Aptitude kullanılmayan eski paketleri otomatik olarak temizler, apt temizlemek için ekstra seçeneklere sahiptir.<br>
→ AppArmor linux işletim sistemi üzerinde çalışan uygulamaların ve süreçlerin güvenlik politikalarını uygulamak için kullanılan bir güvenlik çerçevesidir.<br>

## 2.Basit Kurulum
→ SSH ile bağlanırken root ile bağlanmaması istenmiş. Bunu test için Terminal açıp "ssh root@localhost -p 4242" komutunu yazarak bağlanıp bağlanmadığı kontrol edilir.<br>
→ Seçilen şifre "chage -l kullanıcıadı" komutu ile kontrol edilir.<br>
→ UFW hizmetinin başlatıldığı (aktif olduğu) "systemctl status ufw" komutu ile kontrol edilir.<br>
→ SSH hizmetinin başlatıldığı (aktif olduğu) "systemctl status ssh" komutu ile kontrol edilir.<br>
→ Seçilen işletim sisteminin Debian mı Rocky mi olduğunu "uname -a" komutu ile kontrol edilir.<br>

## 3.Kullanıcı
→ Oturum açma bilgilerini "id" kodu ile kontrol edilir.<br>
→ Kullanıcının hangi gruba ait olduğunu öğrenmek için "id kullanıcıadı", "groups", "cat /etc/group | grep kullanıcıadı" ve "cat /etc/group | grep sudo" komutlarından birisi kullanılabilir.<br>
→ Kullanıcı oluşturmak için "sudo adduser kullanıcıadı" veya "sudo useradd kullanıcıadı" komutu ile kontrol edilir. Bu iki komuttaki "adduser useradı" ve "useradd useradı" arasındaki tek fark adduser ile ekleme yapıldığında bilgiler ister ve girildikten sonra oluşturur, useradd ile ekleme yapıldığında bilgi istemeden kullanıcıyı oluşturur.<br>
→ Eğer kullanıcı "useradd" komutu ile oluşturulur ise şifre atama yapılmaz. Şifre atamak için "passwd rezo" komutu yazıp sonra yeni paralo girilebilir.<br>
→ "sudo chage -l kullanıcıadı" komutu ile şifrenin kurallara uyup uymadığı kontrol edilebilir.<br>
→ Kuralları değiştirmek için "sudo vim /etc/login.defs" dizininin içinde Max days (parolanın oluşturulduktan sonra maksimum kullanılacak gün sayısı), Min days (parolanın oluşturulduktan sonra minimum geçen gün sayısı), Warm (Parolanın süresi dolmasına kaç gün kala verilecek uyarı örneğin değer 3 olur ise parolanın süresinin dolmasına 3 gün kala parola değiştirme uyarısı gelir) ayarları değiştirilerek yapılır.<br>
→ Şifre kurallarını değiştirmek için "sudo vim /etc/pam.d/common-password" dosyasının içerisindeki değerler değiştirilir.<br>
→ "password requisite pam_pwquality.so retry=3" komutu kullanıcıların parolalarını değiştirirken, bu modülü kullan ve değişiklik için en fazla 3 kez yeniden dene anlamını taşır. "pam_pwquality.so modülü" parola kalitesi kontrollerini yapmak için kullanılır.(bu modülün içerisinde kurallar vardır onları uygular).<br>
→ "dcredit=-1" komutu parolalarda küçük harf dâhil olmak üzere en az bir rakam (digit) bulunmalıdır. -1 değeri, bu gereksinimin zorunlu olduğunu belirtir.<br>
→ "difok=7" komutu parolada değişiklik yapıldığında, önceki paroladan en az 7 karakter farklı olmalıdır. Bu, kullanıcıların sık sık aynı parolayı kullanmasını önler.<br>
→ "enforce_for_root" komutu bu kurallar sadece root (kök) kullanıcısı için zorunlu kılınır. (Yani normal kullanıcı için geçerli olan şifre seçeneklerini root içinde geçerli kılar.<br>
→ "lcredit=-1" komutu parolalarda küçük harf bulunmalıdır. -1 değeri, bu gereksinimin zorunlu olduğunu belirtir.<br>
→ "maxrepeat=3" komutu parolada aynı karakterin en fazla 3 kez tekrarlanmasına izin verir. Bu, parolada aynı karakterin çok fazla tekrarını önler.<br>
→ "ucredit=-1" komutu parolalarda büyük harf bulunmalıdır. -1 değeri, bu gereksinimin zorunlu olduğunu belirtir.<br>
→ "usercheck=1" komutu parola değişikliklerinde kullanıcı adının parolada yer almamasını zorunlu kılar. Yani, parolada kullanıcı adı geçemez.<br>
→ "minlen=10" komutu parolanın en az 10 karakter uzunluğunda olması gerekmektedir. Bu, güçlü ve daha güvenli parolaların kullanılmasını sağlar.<br>

## 4.Ana bilgisayar adı ve bölümleri
→ "hostname" kodu bilgisayar adı ve bölümlerini gösterir.<br>
→ Ana bilgisayar adını değiştirmek için "sudo hostnamectl set-hostname yenibilgisayaradı" komutu,
