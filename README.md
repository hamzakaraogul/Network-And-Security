# Network-And-Security IPv4 & Ipv6 & ACL
https://youtu.be/tBJsrqxxje4 -> Youtube Anlatım
<br>
<br>
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
<h3>Şimdi son olarak Access List ile diğer portları kapatıyoruz.</h3><br><br>

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


<img src="https://user-images.githubusercontent.com/62428397/201119577-d4f8db8b-1b09-4a7e-9500-178062311163.png"><br>
<a>Resimde de görüldüğü üzere önce cihazlara manuel olarak ipv6 adreslerini ekliyoruz.</a><br>

<img src="https://user-images.githubusercontent.com/62428397/201120480-2c1249ce-ee68-46d7-a24d-6f1814908a07.png"><br>
<a>Tekrardan yukarıdan başlayarak Router 0 ve Multilayer Switch arasındaki ipv6 atamasını gerçekleştiriyoruz.</a><br>
<br>



<img src="https://user-images.githubusercontent.com/62428397/201145277-8035afbe-c644-4ea0-8f3c-0048fba4e0e6.png"><br>
<a>Router 0 ve Router 1 arasındaki ipv6 atamasını gerçekleştiyoruz. Her zamanki gibi Router 0 da clock olduğu için clock rate giriyoruz. Cihaz arası bağlantılar açık olduğu için 'no sh' yazmamıza gerek kalmıyor.</a><br>
<br>

<img src="https://user-images.githubusercontent.com/62428397/201124119-55b84940-89bc-4e82-8394-fc58928d6ac1.png"><br>
<a>Router 0 ve Router 2 arasındaki ipv6 atamalarını gerçekleştiriyoruz.</a><br>
<br>


<img src="https://user-images.githubusercontent.com/62428397/201137412-bd371d82-1bf0-4cbc-90d3-5c0b49324c02.png"><br>
<a>Router 1 ve Switch arasındaki ipv6 atamasını yapıyoruz.</a><br>
<br>


<img src="https://user-images.githubusercontent.com/62428397/201137841-2651d963-4f61-45d8-a9bb-6499ff7c4eaf.png"><br>
<a>Router 2 ve Switch arasındaki ipv6 atamasını yapıyoruz.</a><br>
<br>

<img src="https://user-images.githubusercontent.com/62428397/201124780-510ece2a-cc7d-449b-910d-c914dc6277f4.png">
<br><a>Resimde de görüldüğü üzere routerlar arası da ipv6 bağlantılarımız yaptıktan sonra cihazlar arası iletişimi kurmak için ipv6 routing ospfimize de başlıyoruz.</a><br>
<br>

<img src="https://user-images.githubusercontent.com/62428397/201126437-5b043a4e-03f9-41f7-b141-4065328be186.png"><br>
<a>Resimde de görüldüğü üzere ipv6 routinge başlarken Ipv6 routing not enabled hatası almaktayız. Bunun önüne geçmek için 'ipv6 unicast-routing' yazarak ipv6 routing'i etkinleştiriyoruz</a><br>
<br>


<img src="https://user-images.githubusercontent.com/62428397/201129024-1d1f8b4e-e8f0-466e-9b2d-14d50bfd5f6f.png">
<br><a>Ipv6 routing yaparken ipv6 router ospf 1 adımından sonra router-id 5.5.5.5 şeklinde örnek olarak router idsi veriliyor sonra route açılması istenilen yolun interface'ne girilerek int fa0/0-> ipv6 ospf 1 area 0 şeklinde diğer yolları belirtmeden routing başlatılıyor.</a><br>
<a>Yukarıdaki resimde de görüldüğü üzere Router 0 ve Router 1 arasındaki ipv6 routing sağladık.</a><br>
<br>


<img src="https://user-images.githubusercontent.com/62428397/201131828-fa196485-4437-4fdc-9fb5-7d486163d312.png"><br>
<a>Router 0 ve Router 2 arasındaki Ipv6 routing de sağlandı</a><br>
<br>
<br>

<img src="https://user-images.githubusercontent.com/62428397/201141894-219c5810-9fe7-4c91-bc8d-4913b0388971.png"><br>
<a>Cihazlar arası ipv6 routing de sağlanabilmesi için Router 1 ve switch arasında 'ipv6 ospf 1 area 0' şeklinde komutu yazarak bağlantıyı açıyoruz. </a><br>
<br>


<img src="https://user-images.githubusercontent.com/62428397/201142606-442aa54a-df78-4901-97c9-b64852568428.png"><br>
<a>Cihazlar arası ipv6 routing de sağlanabilmesi için Router 2 ve switch arasında  bağlantıyı açıyoruz. </a><br>
<br>

<img src="https://user-images.githubusercontent.com/62428397/201142930-a1195a7d-a540-4be1-9aa6-4ff34d4949ec.png"><br>
<a>Cihazlar arası ipv6 routing de sağlanabilmesi için Router 0 ve switch arasında  bağlantıyı açıyoruz. </a><br>
<br>
     

<h3>Sıra ipv6 Dns ayarlamasına geldi.</h3><br>
<br>

<img src="https://user-images.githubusercontent.com/62428397/201132213-4551dfb2-051b-430d-a11b-06ccf2ea283c.png"><br>
<a>Bütün cihazlara manuel olarak Ipv6 dns adresini giriyoruz.</a><br>
<br>


<img src="https://user-images.githubusercontent.com/62428397/201155534-a6f1ae1b-84ed-4b1d-8ce2-07fe06bf2395.png"><br>
<a>Dns servis ayarlarında tekrardan dns ayarlarını yapıyoruz ve bu sefer ipv6 için resimdeki gibi dns ayarlarını yapılandırıyoruz. </a><br>


<img src="https://user-images.githubusercontent.com/62428397/201146235-2dc566fe-4193-4efb-9837-9c2dce3cf85e.png"><br>
<a>Yukarıda ki resimde de görüldüğü üzere hem ping hem de tarayıcı üzerinden belirtmiş olduğumuz yola dns ile gidebiliyoruz.</a><br>
<br>
<h3>Şimdi Ipv6 ile Access List ayarlarını yapıyoruz.</h3><br>
<br>

<img src="https://user-images.githubusercontent.com/62428397/201150215-45f77bd1-092f-4e7d-a150-81a28308383c.png"><br>
<a>Resimde de görüldüğü üzere ; Router 0 da Web ve dns olduğu için aynı şekilde ipv4 ki gibi router 0 terminaline giriyoruz.</a><br>
<a>ipv6 access-list WEBACLIPV6 şeklinde acces-listimizi tanımlıyoruz.</a><br>
<a>permit ile izni veriyoruz ve any yazarak gelen tüm istekleri kabul ediyoruz fakat permit udp any  host 1ef0:111:11:1::2 eq 53 şeklinde sadece 1 port olmak üzere örnek olarak permit udp 1ef0:333:33:3::0/64  host 1ef0:111:11:1::2 eq 53 şeklinde yazsaydık sadece 1ef0:333:33:3::0 üzerinden gelenleri kabul etmiş olurduk yada ayni şekilde sadece tek cihaz için permit udp host 1ef0:333:33:3::2  host 1ef0:111:11:1::2 eq 53 şeklinde yazabilirdik.</a><br>
<br>
<a>Yukarıdaki resimde yaptığımız gibi Ipv6 için access listimizi ayarladık.</a><br>


<img src="https://user-images.githubusercontent.com/62428397/201155067-fb086547-8bea-4f4c-94fe-aa8600b717b6.png"><br>
<a>Son olarak test ettiğimizde dns ve tcp harici diğer portların kapanmış olduğunu görüyoruz.</a><br>
                                                           



