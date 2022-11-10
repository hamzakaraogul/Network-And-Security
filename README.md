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
<a>Şimdi routerlar arası bağlantıyı kuracağız ve bu bağlantı ospf üzerinden olacaktır. Bu bağlantı yine ipv4 üzerinden olacaktır.</a><br>




