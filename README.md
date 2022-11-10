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




