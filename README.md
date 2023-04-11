# Whatsapp API PHP SDK
[kariha.net](https://www.kariha.net) tarafından sağlanan PHP'de whatsapp mesajlarını göndermek için WhatsApp API kitaplığı


# Kurulum

Sadece karihawp.class.php dosyasını indirin veya Composer kullanın:

```
composer require kariha/whatsapp-api-php
```


# Örnek Kullanım

```php
<?php
require_once ('vendor/autoload.php'); // if you use Composer
//require_once('karihawp.class.php'); // if you download karihawp.class.php

$token="hxwhlg9ieqayjxax"; // Kariha Wapi token
$instance_id="instance3169"; // Kariha Wapi instance id
$client = new KarihaWP\WhatsAppApi($token,$instance_id);

$to="mesaj_gonderilecek_numara"; 
$body="Hello world"; 
$api=$client->sendChatMessage($to,$body);
print_r($api);
```
> **NOT:**  instance_id ve token için kendi değerlerinizi giriniz.

## Mesaj Gönderme
* **$to** :  uluslararası formatta test için numaranız, örn. Kişi veya grup için +905553699678 veya sohbet kimliği, ör. 905553699678@c.us veya 905553699678-908503035670@g.us
* **$body** : Mesaj metni, UTF-8 veya UTF-16 string emoji ile
* **$priority** : Bu parametre opsiyoneldir,

Mesajlar için profesyonel bir sıra oluşturmak için kullanabilirsiniz, Öncelik değeri daha az olan Mesajlar önce gönderilir.

örnek kullanım :

öncelik = 0: OTP mesajları gibi yüksek öncelikli mesajlar.

öncelik = 5: genel mesajlar için kullanılır.

öncelik =10: Önemli olmayan mesajlar için kullanılır. Teklif veya promosyon mesajları gibi.

**Varsayılan değer** : 10
* **$referenceId** : Bu mesaj için özel referans kimliğiniz.
```php
$to="mesaj_gonderilecek_numara"; 
$body="Hello world";
$priority=10;
$referenceId="SDK";
$api=$client->sendChatMessage($to,$body,$priority,$referenceId);
print_r($api);
```

## Fotoğraf Gönderme
* **$caption** : Fotoğraf alt metni, UTF-8 veya UTF-16 string emoji ile
* **$image** : HTTP link fotoğraf veya base64 ile enkode edilmiş dosya

Desteklenen uzantılar ( jpg , jpeg , gif , png , svg , webp , bmp ) .

Maksimum dosya boyutu : 16MB .

Maksimum Base64 Uzunluğu : 2,000,000

* **$nocache** : varsayılan olarak false'dir.

false : daha önce yüklenmiş olan dosya kullanılarak gönderilir.
true : her istekte fotoğraf tekrar kontrol edilir.

```php
$to="mesaj_gonderilecek_numara"; 
$image="https://file-example.s3-accelerate.amazonaws.com/images/test.jpg"; 
$caption="image Caption"; 
$priority=10;
$referenceId="SDK";
$nocache=false; 
$api=$client->sendImageMessage($to,$image,$caption,$priority,$referenceId,$nocache);
print_r($api);
```
## Dosya Gönderme
* **$filename** : Dosya adı dekont.jpg veya fatura.pdf gibi
* **$document** : HTTP link dosya veya base64 ile enkode edilmiş dosya

Desteklenen genel dosyalar ( zip , xlsx , csv , txt , pptx , docx ....vb ) .

Maksium dosya boyutu : 100MB .
Maksimum Base64 uzunluğu : 2,000,000

```php
$to="mesaj_gonderilecek_numara"; 
$filename="image Caption"; 
$document="https://file-example.s3-accelerate.amazonaws.com/documents/cv.pdf"; 
$api=$client->sendDocumentMessage($to,$filename,$document);
print_r($api);
```

## Ses Dosyası Gönderme
* **$audio** : HTTP link ses veya base64 ile enkode edilmiş dosya

Desteklenen uzantılar ( mp3 , aac , ogg ) .

Maksium dosya boyutu : 16MB .
Maksimum Base64 uzunluğu : 2,000,000

```php 
$to="mesaj_gonderilecek_numara"; 
$audio="https://file-example.s3-accelerate.amazonaws.com/audio/2.mp3"; 
$api=$client->sendAudioMessage($to,$audio);
print_r($api);
```
## Ses Kaydı Gönderme
* **$audio** : HTTP link ses dosyası ogg dosyası opus codec ile veya base64 ile enkode edilmiş dosya

Maksium dosya boyutu : 16MB .
Maksimum Base64 uzunluğu : 2,000,000

```php 
$to="mesaj_gonderilecek_numara"; 
$audio="https://file-example.s3-accelerate.amazonaws.com/voice/oog_example.ogg"; 
$api=$client->sendVoiceMessage($to,$audio);
print_r($api);
```

## Video Gönderme
* **$video** : HTTP link video veya base64 ile enkode edilmiş dosya

Desteklenen uzantılar ( mp4 , 3gp , mov ) .
Maksium dosya boyutu : 16MB .
Maksimum Base64 uzunluğu : 2,000,000

```php 
$to="mesaj_gonderilecek_numara"; 
$video="https://file-example.s3-accelerate.amazonaws.com/video/test.mp4";
$caption="video Caption"; 
$api=$client->sendVideoMessage($to,$video,$caption);
print_r($api);
```
## Link Gönderme
* **$link** : HTTP or HTTPS link

```php 
$to="mesaj_gonderilecek_numara"; 
$link="https://kariha.net"; 
$api=$client->sendLinkMessage($to,$link);
print_r($api);
```
## Kişi Gönderme
* **$contact** :Kişi ID ve Kişi ID'sinin array edilmiş hâli:

Örnek

905553699678@c.us

or

905553699678@c.us,908503035670@c.us,902526060980@c.us

Maksimum uzunluk : 300 karakter, ortalama 15 kişi yapar

```php 
$to="mesaj_gonderilecek_numara"; 
$contact="14000000001@c.us"; 
$api=$client->sendContactMessage($to,$contact);
print_r($api);
```
## Konum Gönderme
* **$address** : Yazı altında lokasyon.

İki satır desteklenir. İkinci satırı kullanmak için \n kullanın.

Maksimum uzunluk : 300 karakter.
* **$lat** : enlem
* **$lng** : boylam
```php 
$to="mesaj_gonderilecek_numara"; 
$address="Cumhuriyet Mah. Süleyman Demirel Bulvarı \n Fethiye Muğla"; 
$lat="36.659246"; 
$lng="29.126347"; 
$api=$client->sendLocationMessage($to,$address,$lat,$lng);
print_r($api);
```
## Vcard Gönderme
* **$vcard** : vcard 3.0 için yazı metni

Maksimum uzunluk : 4096 karakter

```php 
$to="mesaj_gonderilecek_numara"; 
$vcard="BEGIN:VCARD
VERSION:3.0
N:lastname;firstname
FN:firstname lastname
TEL;TYPE=CELL;waid=14000000001:14000000002
NICKNAME:nickname
BDAY:01.01.1987
X-GENDER:M
NOTE:note
ADR;TYPE=home
ADR;TYPE=work
END:VCARD";
$vcard = preg_replace("/[\n\r]/", "\n", $vcard);
$api=$client->sendVcardMessage($to,$vcard);
print_r($api);
```

## Duruma göre mesajları tekrar gönderme
* **$status** :  gönderilmemiş veya zaman aşımına uğramış (unsent & expired)

```php 
$status="expired";
$api=$client->resendByStatus($status);
print_r($api);
```

## ID'lerine göre mesajları tekrar gönderme
* **$id** :   mesaj ID

```php
$id=123;
$api=$client->resendById($id);
print_r($api);
```

## Mesajları Alma
api ile gönderilmiş mesajları döker

* **$page** : sayfa numarası
* **$limit** : istek için mesaj limiti. maksimum limit: 100
* **$status** : Mesaj durumu [sent , queue , unsent]
    - sent : gönderilmiş mesajları çeker.
    - queue : sıradaki mesajları çeker.
    - unsent : gönderilmemiş mesajları çeker.
    - invalid : geçersiz mesajları çeker.
    - expired : zaman aşımına uğramış mesajları çeker.
    - all : tüm mesajları çeker.
* **$sort** :
    - asc : Mesaj ID numarası küçükten büyüğe doğru çeker
    - desc : Mesaj ID numarası büyükten küçüğe doğru çeker
* **$id** : Mesaj ID'sine göre filtreler
* **$referenceId** : Referans ID'sine göre filtreler.
* **$from** : Gönderici numarasına göre filteler. örnek: 905553699678@c.us .
* **$to** : Hedef numarasına göre filtreler. örnek: 908503035670@c.us veya 905553699678-908503035670@g.us .
* **$ack** : Mesajları ack durumuna göre filtreler [ pending , server , device , read , played ] .


```php 
$page=1;
$limit=100;
$status="all";
$sort="asc";
$id="";
$referenceId="";
$from="";
$to="";
$ack="";
$api=$client->getMessages($page,$limit,$status,$sort,$id,$referenceId,$from,$to,$ack);
print_r($api);
```

## Mesaj İstatistiklerini Çeker

```php 
$api=$client->getMessageStatistics();
print_r($api);
```

## Makine Durumunu Çeker

```php 
$api=$client->getInstanceStatus();
print_r($api);
```

## Makinenin QR İmajını Çeker

```php 
header('Content-Type: image/png');
$api=$client->getInstanceQr();
print_r($api);
```
## Makinenin QR Kodunu Çeker

```php  
$api=$client->getInstanceQrCode();
print_r($api);
```
## Makinenin SS'ini alır

```php  
header('Content-Type: image/png');
$api=$client->getInstanceScreenshot();
print_r($api);
```
veya base64
```php
$api=$client->getInstanceScreenshot("base64");
print_r($api);
```
## Makine Bilgilerini Çeker
Bağlı telefonun bilgilerini gösterir: numara, ad, fotoğraf gibi...
```php
$api=$client->getInstanceMe();
print_r($api);
```
## Makine Ayarları
sendDelay : Mesaj gönderme aralığını belirler. Varsayılan değer 1'dir.
webhook_url : Http or https URL ile bilgilendirme almak için.
webhook_message_ack : açık/kapalı ack (mesaj teslim edildi veya mesaj görüntülendi) bilgilendirmeleri için webhook
webhook_message_received : açık/kapalı mesaj alındığında tetiklenecek webhook
webhook_message_create : mesaj oluşturulduğunda bilgilendirme için webhook
webhook_message_download_media  :  açık/kapalı döküman veya medya dosyaları için
```php
$api=$client->getInstanceSettings();
print_r($api);
```

## Makine Devralma
Cihaz başka bir Web WhatsApp örneğine bağlandıysa etkin oturumu döndürür

```php  
$api=$client->sendInstanceTakeover();
print_r($api);
```
## Makineden Çıkış
Yeni QR kodunu almak için WhatsApp Web'den çıkış yapar.

```php  
$api=$client->sendInstanceLogout();
print_r($api);
```
## Makine Yeniden Başlatma
Makineyi yeniden başlatır.

```php  
$api=$client->sendInstanceRestart();
print_r($api);
```
## Makine Ayarlarını Günceller
* **sendDelay** : Mesaj gönderme aralığını belirler. Varsayılan değer 1'dir.
* **webhook_url** : Http or https URL ile bilgilendirme almak için.
* **webhook_message_received** : true/false mesaj alındığında tetiklenecek webhook
* **webhook_message_create** : true/false mesaj oluşturuduğunda bilgilendirme için webhook
* **webhook_message_ack** : true/false ack (mesaj teslim edildi veya mesaj görüntülendi) bilgilendirmeleri için webhook

```php  
$sendDelay=1;
$webhook_url="";
$webhook_message_received=false;
$webhook_message_create=false;
$webhook_message_ack=false;
$webhook_message_download_media=false;

$api=$client->sendInstanceSettings($sendDelay,$webhook_url,$webhook_message_received,$webhook_message_create,$webhook_message_ack,$webhook_message_download_media);
print_r($api);
```

## Sohbet Listesini Çeker

```php  
$api=$client->getChats();
print_r($api);
```

## Görüşmedeki Son Mesajı/Mesajları Çeker

* **$chatId** : chatID, kişi veya grup. örnek: 905553699678@c.us or 14155552671-441234567890@g.us
* **$limit** : istek başına mesaj limiti.

Maksimum değer: 1000 .

```php  
$chatId="905553699678@c.us";
$limit=100;
$api=$client->getChatsMessages($chatId,$limit);
print_r($api);
```


## Kişi Listesini (Rehberi) Çeker

```php  
$api=$client->getContacts();
print_r($api);
```

## Kişi Bilgilerini Çeker

* **$chatId** : chatID veya kişi. örnek: 905553699678@c.us

```php  
$chatId="905553699678@c.us"; 
$api=$client->getContact($chatId);
print_r($api);
```


## Engellenmiş Kişileri Çeker

```php  
$api=$client->getBlockedContacts();
print_r($api);
```

## Kişiyi Engeller

* **$chatId** : chatID veya kişi. örnek: 905553699678@c.us

```php  
$chatId="905553699678@c.us"; 
$api=$client->blockContact($chatId);
print_r($api);
```

## Engellemeyi Kaldırır

* **$chatId** : chatID veya kişi. örnek: 905553699678@c.us

```php  
$chatId="905553699678@c.us"; 
$api=$client->unblockContact($chatId);
print_r($api);
```

## WhatsApp Kullanıcısı Olup Olmadığını Kontrol Eder

* **$chatId** : chatID veya kişi. örnek: 905553699678@c.us

```php  
$chatId="905553699678@c.us"; 
$api=$client->checkContact($chatId);
print_r($api);
```



# Destek
**Sorunlar** ve **Geliştirme Talepleri** için bize ulaşın
