# Born2beroot

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
→ Ana bilgisayar adını değiştirmek için "sudo hostnamectl set-hostname yenibilgisayaradı" komutu veya alternatif olarak "sudo vim /etc/hosts" dosya içerisinde 127.0.0.1 yanına yeni bilgisayar adı yazılır.<br>
→ Sanal disk bölümlerini görebilmek için "lsblk" komutu kullanılır. Buradaki ilk 4 disk birincil, geri kalan ise mantıksaldır.<br>
→ LVM (Logical Volume Menager) bir diski bölümlere ayırma işlemi yapar ve ayrılan disklerden birisi dolar ise diğer diskten belli bir kısmı otomatik olarak diğerine aktarır.<br>

## 5.SUDO
→ "sudo --version" veya "sudo dpkg -l | grep sudo" komutu ile sudonun sanal makineye yüklenip yüklenmediği kontrol edilebilir.<br>
→ "groups kullanıcıadı" ile kullanıcıadı kısmındaki kullanıcının grubunu gösterir. Alternatif olarak "cat /etc/group | grep sudo" ile grubunu görebiliriz.<br>
→ Sudo herhangi bir kullanıcının sisteme yönetici olarak bağlanmaları gerekmeden yönetici yetkisi gerektiren komutları uygulayabilmesini sağlayan bir programdır. Sudo yetkisi ile yapılan işlemleri kimin yaptığının takibi daha kolaydır.<br>
→ "sudo visudo" komutu ile sudonun katı kurallarının var olduğu doğrulanır.<br>
→ "cd /var/log/sudo" içerisinde "ls -l" yapar isek sudo klasörünün var olduğunu ve en az bir dosyaya sahip olduğunun kontrolünü sağlayabiliriz.<br>
→ sudo üzerinde bir kullanıcının şifresini "sudo passwd kullanıcıadı" şeklinde değiştirilir.<br>
→ Sudo log dosyasının değiştiğini doğrulamak için "sudo cat /var/log/sudo/sudo.log" şeklinde yazarak log komutlarına yeni log eklendiğini görebiliriz.<br>

## 6.UFW
→ "systemctl status ufw" komutu ile UFW'nin sisteme yüklendiğini ve aktif olduğunu kontrol edebiliriz.<br>
→ UFW (Uncomplicated Firewall) kısaltmasıdır. Ubuntu gibi bazı linux dağıtımlarında kullanılan bir güvenlik duvarı (firewall) aracıdır. Bu araç, Ağ trafiğini kontrol etmeyi ve belirli kurallara göre izin vermek veya engellemek için kullanılır. Örneğin, belirli bir bağlantı noktasına gelen girişleri engellemek veya belirli bir uygulamanın internete erişimini sınırlamak gibi kurallar oluşturabilirsiniz.<br>
→ "sudo ufw status numbered" komutu ile Ufw'deki aktif kuralları listeleyebiliriz.<br>
→ "sudo ufw allow 8080" komutu ile 8080 numaralı bağlantı noktası açabiliriz.<br>
→ "sudo ufw delete silineceksatırnumarası" komutu ile bağlantı noktalarını silebiliriz.<br>

## 7.SSH
→ "systemctl status ssh" komutu ile SSH'nin sisteme yüklendiğini ve aktif olduğunu kontrol edebiliriz.<br>
→ "vim /etc/ssh/sshd_config" dosyasında sadece 4242 portunda çalıştığını ve "PermitRootLogin no" kısmı ise ssh ile bağlanır iken root olarak bağlanmayı engeller.<br>
→ SSH (Secure Shell) kısaltmasıdır ve güvenli bir şekilde uzak bir bilgisayara erişim sağlamak için kullanılan bir ağ protokolüdür.<br>
→ "ssh root@localhost -p 4242" komutu ile root olarak bağlanmayı deneyerek bağlanmadığını görebiliriz. Aynı şekilde "kullanıcıadı@localhost -p 22" komutu ile 22 portundan bağlanmayı deneyerek bağlanmadığını görebiliriz. "ssh kullanıcıadı@localhost -p 4242" komutu ile 4242 portundan bağlanmayı deneyerek bağlandığını görebiliriz.<br>

## 8.Script Monitoring
→ "vim usr/local/bin/monitoring.sh" dosyasını açarak monitoring.sh dosya içeriğine ulaşabiliriz.<br>
→ "arc=$(uname -a)" Bu komut, sistemdeki mimari, işletim sistemi türü ve diğer bilgileri almak için uname -a komutunu kullanıyor. Bu bilgileri "arc" değişkenine atıyor.<br>
→ "pcpu=$(grep "physical id" /proc/cpuinfo | sort | uniq | wc -l)" Bu komut, CPU'ların fiziksel ID'lerini alıyor. CPU'ların fiziksel sayısını pcpu değişkenine atıyor.<br>
→ "vcpu=$(grep "^processor" /proc/cpuinfo | wc -l)" Sanal CPU sayısını alır ve vcpu değişkenine atar.<br>
→ "fram=$(free -m | grep Mem: | awk '{print $2}')" Toplam RAM miktarını MB cinsinden alır ve fram değişkenine atar.<br>
→ "uram=$(free -m | grep Mem: | awk '{print $3}')" Kullanılan RAM miktarını MB cinsinden alır ve uram değişkenine atar.<br>
→ "pram=$(free | grep Mem: | awk '{printf("%.2f"), $3/$2*100}')" Kullanılan RAM'ın yüzdesini hesaplar ve pram değişkenine atar.<br>
→ "fdisk=$(df -Bg | grep '^/dev/' | grep -v '/boot$' | awk '{ft += $2} END {print ft}')" Toplam disk kapasitesini GB cinsinden alır ve fdisk değişkenine atar.<br>
→ "udisk=$(df -Bm | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} END {print ut}')" Kullanılan disk alanını MB cinsinden alır ve udisk değişkenine atar.<br>
→ "pdisk=$(df -Bm | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} {ft+= $2} END {printf("%d"), ut/ft*100}')" Disk doluluk oranını yüzde cinsinden hesaplar ve pdisk değişkenine atar.<br>
→ "cpul=$(top -bn1 | grep '^%Cpu' | cut -c 9- | xargs | awk '{printf("%.1f%%"), $1 + $3}')" CPU kullanımını yüzde cinsinden hesaplar ve cpul değişkenine atar.<br>
→ "lb=$(who -b | awk '$1 == "system" {print $3 " " $4}')" Sistemin ne zaman başlatıldığını alır ve lb değişkenine atar.<br>
→ "lvmt=$(lsblk -o TYPE | grep "lvm" | wc -l)" LVM (Logical Volume Manager) var mı yok mu kontrol eder.<br>
→ "lvmu=$(if[$lvmt -eq 0 ]; then echo no; else echo yes; fi)" LVM'nin var olup olmadığına göre bir mesaj döndürür.<br>
→ "ctcp=$(cat /proc/net/tcp | wc -l | awk '{print $1-1}' | tr '' ' ')" Açık olan TCP bağlantılarının sayısını alır.<br>
→ "ulog=$(users | wc -w)" Sisteme kaç kullanıcının bağlı olduğunu sayar.<br>
→ "ip=$(hostname -I)" Sistemin IP adresini alır.<br>
→ "mac=$(ip link show | awk '$1 == "link/ether" {print $2}')" Sistemin MAC adresini alır.<br>
→ "cmds=$(journalctl _COMM=sudo | grep COMMAND | wc -l)" Bu komut, journalctl komutuyla sistem günlüklerinde "sudo" komutlarının kullanımını arar. grep COMMAND ile "COMMAND" kelimesini arar ve ardından wc -l ile bu satır sayısını bulur. Yani, cmds değişkenine toplamda kaç "sudo" komutunun kullanıldığını kaydeder.<br>
→ wall "...$cmds cmd": wall komutu, metin duvarına (Wall) bir mesaj gönderir. Bu mesaj, değişkenler içeren bir metin içerir ve birleştirilmiş sistem bilgilerini içerir. Metin içinde kullanılan değişkenler, önceki komutlarla alınan sistem bilgilerini içerir. Örneğin:<br>
      $arc: Sistem mimarisi bilgisini içerir.<br>
      $pcpu: Fiziksel CPU sayısını içerir.<br>
      $vcpu: Sanal CPU sayısını içerir.<br>
      $ uram , ${fram} , $pram: Kullanılan ve toplam RAM miktarını ve yüzdesini içerir.<br>
      $ udisk , ${fdisk} , $pdisk: Kullanılan ve toplam disk alanını ve yüzdesini içerir.<br>
      $cpul: CPU yükünü içerir.<br>
      $lb: Son başlatma zamanını içerir.<br>
      $lvmu: LVM kullanılıp kullanılmadığını içerir.<br>
      $ctcp: TCP bağlantı sayısını içerir.<br>
      $ulog: Giriş yapan kullanıcı sayısını içerir.<br>
      $ip, $mac: IP adresi ve MAC adresini içerir.<br>
      $cmds: Sudo komutu sayısını içerir.<br>

#### Cron nedir ?
→ Cron, Unix benzeri işletim sistemlerinde belirli görevleri belirli aralıklarla otomatik olarak çalıştırmak için kullanılan bir zamanlanmış görev yöneticisidir. Genellikle sistemdeki işlerin zamanlamasını ve planlanmasını yapmak için kullanılır. Cron, kullanıcıların belirlediği komutları veya betikleri, belirli bir zaman diliminde veya belirli aralıklarla çalıştırabilir.<br>
→ **/***** bash /usr/local/sbin/monitoring.sh  (*dakika)(*saat)(*ayın günü)(*ay)(*haftanın günü) ——> bu işlemi gerçekleştir.<br>
→ Komut dosyasının çalışmasını durdurmak için "sudo systemctl stop cron" komutu yazılır. Fakat reboot sonrası tekrar aktif hale gelir. Reboot sonrası aktif olmasını istemiyorsak "sudo systemctl disable cron" şeklinde yazarak daha sonrasında reboot atarak deaktif hale getirebiliriz.<br>
→ ***/etc dosyası: sistem ile ilgili bütün konfigürasyon dosyaları bulunur.***<br>
