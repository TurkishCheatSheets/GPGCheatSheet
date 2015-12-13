 _____ _____ _____    _____ _           _       _           _   
|   __|  _  |   __|  |     | |_ ___ ___| |_ ___| |_ ___ ___| |_ 
|  |  |   __|  |  |  |   --|   | -_| .'|  _|_ -|   | -_| -_|  _|
|_____|__|  |_____|  |_____|_|_|___|__,|_| |___|_|_|___|___|_|  
                                                                

gpg --gen-key

Anahtar çifti oluşturmak için kullanılır.

Not:Bu noktadan sonra gpg anahtar çiftinin nasıl oluşturulacağı ile ilgili 
seçenekler listeler.

2. adımda satır boş bırakılırsa gpg anahtarı öntanımlı olarak 2048 bit oluşturacaktır.
İyi bir anahtar için 4096 bit daha avantajlıdır. 3. adım olarak son geçerlilik tarihi için ise
1 veya 2 yıldan daha uzun bir süre seçmemek yine avantajlı olacaktır.

----

gpg -ao sertifika.asc --gen-revoke key_id

id'si belirtilen anahtara iptal sertifikası oluşturmak için kullanılır.

----
gpg --list-secret-keys

Kayıtlı özel anahtarları ve ilgili bilgileri (key id, son kullanma tarihi vs.) listeler

----

gpg --list-keys

Kayıtlı genel anahtarları ve ilgili bilgileri (key id, son kullanma tarihi vs.) listeler

----

gpg --fingerprint

Parmak izlerini (fingerprint) listeler. 

----
gpg --delete-secret-key "kullanici_adi"

Belirtilen key id veya kullanıcı adına ait özel anahtarı siler.

----

gpg --delete-key "kullanici_adi"

Belirtilen key id veya kullanıcı adına ait genel anahtarı siler.

not:Bu komut belirtilen kullanıcı adına ait bir özel anahtar olmadığında kullanılabilir.
Aksi ihtimalde önce bir üstte bulunan komutu kullanarak özel anahtarı silmeniz gerekir.

----

gpg -ao ozel_anahtar.asc --export-secret-keys "anahtar_id"

id'si belirtilen özel anahtarı ASCII zırhlı ve açık biçimde dışa aktarır.

----

gpg -a --export-secret-keys "anahtar_id" | gpg -aco ozel_anahtar.gpg.asc

id'si belirtilen özel anahtarı "ozel_anahtar.gpg.asc" olarak, ASCII zırhlı
biçimde şifreli olarak dışa aktarır. Komutun ilk kısmı ise özel anahtarı ekrana yazdırır.

----

gpg -ao genel_anahtar.asc --export "anahtar_id"

id'si ya da email hesabı belirtilen genel anahtarı ASCII zırhlı olarak dışa aktarır.

----

gpg --allow-secret-key-import --import ozel.anahtar

"ozel.anahtar" adındaki özel anahtarı içe aktarır.

----

gpg --import genel.anahtar

"genel.anahtar" adındaki genel anahtarı içe aktarır.

----
gpg --passphrase devletsırrı -c foo.tar.gz

İnteraktif olmayan biçimde (crontab ya da bash script için) dosya şifreler.

----

gpg --passphrase devletsırrı foo.tar.gz.gpg

İnteraktif olmayan biçimde (crontab ya da bash script için) şifreli dosyayı açar. 

----

gpg -e -u "gonderen@sifreleyen.com" -r "alan@sifreyiacan.com" dosya.txt

Gönderen (gonderen@sifreleyen.com) tarafından, "dosya.txt" dosyasını 
alıcı (alan@sifreyiacan.com) için şifreler. > dosya.txt.gpg
 
----

gpg -e -u "gonderen@sifreleyen.com" -r "alan@sifreyiacan.com" --sign dosya.txt

Gönderen (gonderen@sifreleyen.com) tarafından, "dosya.txt" dosyasını 
alıcı (alan@sifreyiacan.com) için şifreler ve imzalar. 

not: Gönderilen veriyi imzalamak güvenliği arttıracaktır. Bu durumda gpg aracı 
deşifre işlemi esnasında imzayı otomatik olarak kontrol eder ve çıktıları ekrana yazar.   
----

gpg -d dosya.txt.gpg

Şifreli dosyayı (dosya.txt.gpg) deşifre eder ve 
ekrana yazdırır.

----

gpg -o dosya.txt -d dosya.txt.gpg

Şifreli dosyayı (dosya.txt.gpg) deşifre eder ve
belirtilen ad-tür ile dışa aktarır.

----

gpg --keyserver sunucu_url --send-keys key_id

id'si belirtilen anahtarı istenen anahtar sunucusuna (örn. pgp.mit.edu) gönrerir.

----

gpg --keyserver sunucu_url --recv-key key_id

id'si belirtilen anahtarı istenen anahtar sunucusundan çeker. 

----

utf8-strings
keyserver  hkp://keyserver.ubuntu.com

her seferinde keyserver belirtmemek ve encoding sorunu yaşamamak için ~/.gnupg/gpg.conf dosyasına yukarıdakileri ekleyin.

----

default-cache-ttl 43200
max-cache-ttl 43200

gpg parolanızı belli bir süre hafızada tutmak için (örn. 12 saat, saniye cinsinden) yukarıdakileri ~/.gnupg/gpg-agent.conf dosyasına ekleyin.

----

--edit-key key_id

id'si belirtilen anahtar ile ilgili belirli düzenlemeler yapmak için kullanılır.

Bu noktada gpg aracı id'si belirtilen anahtar için bir komut satırı başlatır ve aşağıdaki
komutlar uygulanarak anahtar üzerinde düzenlemeler yapılır.

--

passwd

Belirtilen özel anahtarın passphrase'ini değiştirmek için kullanılır.

-

sign 

Belirtilen anahtarı imzalamak için kullanılır.

-

addphoto

Belirtilen anahtara görsel eklemek için kullanılır.

Not 1: Görsel jpg ve 240x288px'den büyük olmamalıdır. 
Not 2: Bazı anahtar sunucuları bu biçimdeki anahtarları kabul etmez veya
anahtarınıza sunucu üzerinden ulaşmak isteyenler bu işlemden sonra sorun yaşayabilir.

-

showphoto

Eğer anahtara görsel eklenmişse bu görseli görüntülemek için kullanılır.

-

save

Değişiklikleri kaydedip çıkmak için kullanılır.

-

quit

Değişiklikleri kaydetmeden çıkmak için kullanılır.











