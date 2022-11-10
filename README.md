# Network-And-Security


<img src="https://user-images.githubusercontent.com/62428397/201099693-69f2c7e2-b55b-4d0c-994b-86c98a936f9a.png">
<br>

<a>Yukarıda ki resimde de görüldüğü üzere senaryo; </a><br>

<a>1.Omurga IPv4 ve IPv6 dual stack calisicak.</a><br>
<a>2.Dynamic Routing OSPF ile gerceklenicek.</a><br>
<a>3.Hem IPv4 hemde IPv6 omurga ACL ile sadece servis portlarindan hizmet verecek.</a><br>
<a>4.Diğer tüm portlar kapali olucak</a><br>

<h3>Öncelikle Ipv4 üzerinden gideceğiz ve onun ip atamalarını yapacağız.</h3><br>


<img src="https://user-images.githubusercontent.com/62428397/201100915-0187f6a2-85e8-4de3-932f-90d8bd1582a8.png"><br>
<a>Yukarıda ki örnekte de görüldüğü üzere ilk önce 'End Device' ları kendi üzerinden direk ipv4 adreslerini veriyoruz.</a>
<br>

<a>Sonrasında en üstteki switchten başlayarak ipv4 atamalarını gerçekleştiriyoruz.</a><br>

<img src="https://user-images.githubusercontent.com/62428397/201103873-860d6baf-48f9-44cc-94a7-8ce6ac4288f9.png"><br>
<a>Yukarıdaki resimde de görüldüğü üzere Switch - Router arasındaki fa0/0 interface'ne giriyoruz ve 192.168.1.1 255.255.255.0 (/24 olduğu için subnetmask bu şekilde girilmektedir) atamasını gerçekleştiriyoruz.</a><br>
<a>Router 0 Command Line üzerindeki komutlar sırasıyla; en -> conf t -> int fa0/0 -> ip add 192.168.1.1 255.255.255.0 -> no sh (bu komutla bağlantıyı açıyoruz) </a>
<br>

<img src="https://user-images.githubusercontent.com/62428397/201105023-89651c98-0639-4f78-b1eb-b29038b06091.png"><br>
<a>Devam ettiğimizde yukarıda görüldüğü üzere Router 0 ve Router 1 arasında ki ipv4 atamalarını yapıyoruz ve subnetmask ataması /30 olduğu için 255.255.255.252 olarak atıyoruz. Router 0 üzerinde de görüldüğü üzere Clock rate Router 0 da olduğu için komutları girdiğimizde onun limitini de belirliyoruz.</a><br>



<img src="https://user-images.githubusercontent.com/62428397/201106217-0e48aa85-ec8c-44c9-ae94-340a89cd6a4f.png">
<a>Devam edersek Router0 ve Router2 arasındaki ipv4 atamasını da gerçekleştiriyoruz. </a> <br>
<br>


<img src="https://user-images.githubusercontent.com/62428397/201106958-9283b687-2a86-42f6-86d6-5cbed014c1f8.png"><br>
<a>Router 1 ve Switch arasındaki ipv4 atamasını yapıyoruz.</a><br>


<img src="https://user-images.githubusercontent.com/62428397/201107346-23656b7e-6f12-41d9-9293-745170bddcc6.png"><br>
<a>Router 2 ve Switch arasındaki ipv4 atamasını yapıyoruz.</a><br>


<img src="https://user-images.githubusercontent.com/62428397/201108390-3aa0d2eb-bba3-4b2d-bfd4-320c89f49b2c.png"><br>
<a>Yukarıdaki resimde de görüldüğü üzere kendi içinde router arasında ki bağlantımızda problem görülmemektedir. Fakat dışarıdaki bir router ile bağlantı kurmaya çalıştığımızda 'Destination host unreachable' hatası almaktayız. Bu hata ping atılan o cihaz içerisindeki router üzerindeki ayarın yapılmadığını bize anlatmaktadır. </a><br>
<br>
<h3>Şimdi routerlar arası bağlantıyı kuracağız ve bu bağlantı ospf üzerinden olacaktır. Bu bağlantı yine ipv4 üzerinden olacaktır.</h3><br>

<br>
<br>


<img src="https://user-images.githubusercontent.com/62428397/201111055-ddefb40f-6dfc-4dc9-97e0-a228519a153f.png">
<br>
<a>Router ospf bağlantısı wilcard mask kullanmaktadır. O yüzden bağlantıları yazarken subnet maskın tersini yazmaktayız. Yukarıda resim de de görüldüğü gibi 255.255.255.252 -> 0.0.0.3 ve 255.255.255.0 -> 0.0.0.255 dir. </a><br>
<a>Router 0 ayarlamasını yaparken ' network 13.0.0.0 0.0.0.3 area 0 ' de yazdığımızı farketmişsinizdir. Bunun nedeni Router 0'ın bu yola da sahip olmasından kaynaklanmaktadır. Yani ospf ayarlaması yapılandırırken router ospf 1 -> network 192.168.1.0 0.0.0.255 şeklinde sahip olduğumuz yolları işlemekteyiz. </a>

<br><br>

<a>Router 0 ve Router 1 ayarlamalarını yaptığımızda burada Router 0 da zaten network 13.0.0.0 eklediğimiz için sadece Router 2 ayarlaması kalmıştır. O da aşağıdaki resimde de görüldüğü üzeredir. </a><br>

<img src="https://user-images.githubusercontent.com/62428397/201113011-9b89d5ec-8585-4d01-bfa7-1f6a5e012af9.png"><br>
<br><br>


<img src="https://user-images.githubusercontent.com/62428397/201113420-ace7238c-a88e-4fbc-9764-00c65c784bba.png"><br>
<a>Yukarı da da görüldüğü üzere rastgele seçtiğimiz bir cihazda ping denemelerinin başarılı bir şekilde çalıştığınız görüyoruz.</a>
br><br>

<h3>Şimdi ipv4 ile son yapmamız gereken dns ayarlamasını yapmamız ve acl ile portları kapatmak olacaktır.</h3><br>
br><br>
<img src="https://user-images.githubusercontent.com/62428397/201114026-e944a498-d69f-461b-8d02-aa8192824a8c.png"><br>
<a>Öncelikle bütün cihazlara resimde görülen dns serverın ip atamalarını elle yapıyoruz.</a><br>


<img src="https://user-images.githubusercontent.com/62428397/201114465-7eff7c4b-444a-4e30-b95e-f4c2acb976c0.png"><br>
<a>Sonrasında dns servera girip service ayarları altında dns'in içine girip aktif ediyoruz ve web yolunu resimdeki gibi tanımlıyoruz ve add tuşuna basıyoruz.</a><br>


<img src="https://user-images.githubusercontent.com/62428397/201114917-19cb6c3d-b3da-4641-b4ea-f071f769023d.png"><br>
<a>Rastgele bir cihazda tarayıcı üzerinden denediğinizde dns serverin çalıştığını göreceksiniz.</a><br>
<br>
<br>
<h3>Şimdi son olarak Acess List ile diğer portları kapatıyoruz.</h3><br><br>

<img src="https://user-images.githubusercontent.com/62428397/201116279-03937c6d-c75c-4836-9473-8240e680e7fe.png"><br>
<a>Dns ve Server Router 0 üzerinde bağlı olduğu için ayarlamayı oradan yapmaktayız. </a><br>
<a>Öncelikle access list ayarlarken sırasıyla en-> conf t -> ip access-list extended WEBACL şeklinde giriyoruz. Bu kısımda WEBACL şeklinde yazdığımız yere başka birşey yazabiliriz.</a><br>
<a>Sonrasında permit udp any host 192.168.1.2 eq 53 şeklinde komut giriyoruz. Burada any herhangi bir yerden gelen anlamındadır oraya istersek 192.168.2.0 0.0.0.255 şeklinde de bir ifade yapabilirdik ama böylelikle sadece 192.168.2.0 dan gelen istekler kabul edilirdi yada sadece bir cihaza izin verseydik host 192.168.2.2 şeklinde izin vermiş olacaktık. Yani: permit udp 192.168.2.0 0.0.0.255 host 192.168.1.2 eq 53 veya permit udp host 192.168.2.2 host 192.168.1.2 eq 53 </a><br>
<a>Sonrasında int fa0/0 komutunu yazıyoruz. Bunun nedeni istekler dışarıdan geleceği için routerdan sonra filtreleme yaparak 'ip access-group WEBACL out' şeklinde out ile yani dışarıdan gelen istekleri filtreliyoruz. </a><br>
<a>Örnek olarak baktığımızda;</a><br>


<img src="https://user-images.githubusercontent.com/62428397/201118393-043ced24-1492-40df-9768-4204eaeaa431.png"><br>
<a>Sağdaki laptop üzerinden ping attığımızda resimde de görüldüğü üzere router 0 üzerinden istek durdurulmaktadır.</a><br>
<img src="https://user-images.githubusercontent.com/62428397/201118642-90fb51b3-1a40-4d6f-90a0-f2a97bed69ac.png"><br>
<a>Tarayıcıdan girmeye çalıştığımzda da daha önce tanımdalığımız yere girebilmekteyiz. Yani diğer portlar kapanmış oldu.</a>

<br>
<br>

<h3>Şimdi Ipv6 üzerinden gideceğiz ve onun ip atamalarını yapacağız.</h3><br>



