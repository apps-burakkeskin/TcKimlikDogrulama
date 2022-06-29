# PHP ile T.C. Kimlik No Doğrulama

Devletin bize verdiği SOAP servisi sayesinde, T.C. Kimlik Numarasının gerçekten doğru olup olmadığını kontrol edebiliyoruz. Bunuda PHP’de aşağıdaki şekilde kullanıyoruz. Burada dikkat edilmesi gereken gönderilen ad ve soyad’ın büyük harflerle yazılmasıdır. Aksi taktirde doğrulama işlemi çalışmamaktadır. Eğer bu TCKimlikNoDogrula metodu nereden çıktı, TCKimlikNoDogrulaResult property’sini nasıl elde ettik derseniz SoapClientile bağlandığımız yerden aldık bu bilgileri.

## TÜRK T.C. SORGULAMA

```php
<?php

$client = new SoapClient("https://tckimlik.nvi.gov.tr/Service/KPSPublic.asmx?WSDL");
try {
    $result = $client->TCKimlikNoDogrula([
        'TCKimlikNo' => '5555555555',
        'Ad' => 'BURAK',
        'Soyad' => 'KESKİN',
        'DogumYili' => '1991'
    ]);
    if ($result->TCKimlikNoDogrulaResult) {
        echo 'T.C. Kimlik No Doğru';
    } else {
        echo 'T.C. Kimlik No Hatalı';
    }
} catch (Exception $e) {
    echo $e->faultstring;
}

?>
```


## YABANCI T.C. SORGULAMA

```php
<?php

$client = new SoapClient("https://tckimlik.nvi.gov.tr/Service/KPSPublicYabanciDogrula.asmx?WSDL");
try {
    $result = $client->YabanciKimlikNoDogrula([
        'TCKimlikNo' => '5555555555',
        'Ad' => 'BURAK',
        'Soyad' => 'KESKİN',
        'DogumGun' => '05',
        'DogumAy' => '11',
        'DogumYil' => '1991'
    ]);
    if ($result->YabanciKimlikNoDogrulaResult) {
        echo 'T.C. Kimlik No Doğru';
    } else {
        echo 'T.C. Kimlik No Hatalı';
    }
} catch (Exception $e) {
    echo $e->faultstring;
}

?>
```