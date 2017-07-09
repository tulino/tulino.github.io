Cybele her ne kadar adını Anadolu tanrıçasından alsa da "Ruby on Rails'e" yeni başlayanlar için
 user-admin arayüzlerine sahip  projeleri kolayca oluşturmayı ve bu arayüzleri yönetmemizi sağlayan
 şablondur.
 
 Kurulum aşamasından önce sistemde ruby ve rails'in kurulu olması gerekiyor.
 Gerekli olan en düşük versiyon tipleri:
    

    Ruby ~> 2.3

    Rails ~> 4.2 'dir.
    
    
Eger sistemde kurulu başka rails versiyonu varsa 5.1 gibi
bu sorun oluşturur.Öncelikle bu versionu kaldırıp
4.2 versiyonunu yükleyip öyle kurulum aşamasına başlayın

Şimdi "Cybele" gem ini indirmeye başlayalım

    $ gem install cybele
    
Daha sonra terminalimizi açıp Cybele ile yeni proje oluşturalım

    $ cybele project_name
    
project_name yerine istediğiniz şekilde bir isimlendirme yapabilirsiniz.
anlatıma projenin adını cybele_example olarak devam edicem

    $cybele cybele_example
    
 cybele_example projemizin altında db/migrate klasörünün içerisinde bulunan devise_create_user ve devise_create_admin
 dosyalarında değiştirmemiz gereken alanlar bulunmakta.
 
    t.boolean :is_active
    t.string :time_zone
 Bu iki satırı şöyle değiştiriyoruz;
 
    t.boolean :is_active, default: true
    t.string :time_zone, default: "UTC"
    
 Projemizin içinde bulunan public klasörune gelerek aşağıdaki komutu
 çalıştırıyoruz.
 
    $ cd public
    
    $ ln -s ../VERSION.txt VERSION.txt
    
 config/databes.yml uzantılı dosyamızı açıyoruz.Görünen development
kısmı aşağıdaki şekilde olmalı

    development: &default
    adapter: postgresql
    database: cybele_example_development
    encoding: utf8
    min_messages: warning
    pool: 5
    timeout: 5000
    host: localhost
    port: 5432
    username: cybele_example
    password: cybele_example
    
Bundan sonraki aşama için sisteminizde Postgresql'in kurulu olduğundan emin olun kurulu değilse kurulumunu yapıp o şekilde ilerleyiniz

Yukardaki databes ismiyle aynı olacak sekilde Postgresql de databes oluşturup username ve pasword tanımlıycaz

    $ sudo -u postgres psql 
    
   postgresql terminalini açıyoruz.

    $ CREATE DATABASE ‘cybele_example_development’;
    
 yukardaki şekilde databes oluşturuyoruz.Databes isminin databes.yml klasöründeki ile aynı olmasına dikkat etmeliyiz

Aynı şekilde databes için username ve pasword oluştutuyoruz

    $ CREATE USER cybele_example PASSWORD 'cybele_example';
    
   Son databes işlemi olarak aşagıdaki komutu yazıyoruz.
   
    $ ALTER USER cybele_test WITH SUPERUSER;
  
 Şimdi sırayla Aşağıdaki komutları yazıp projeyi test edebiliriz
 
    $ bundle exec rake db:create
    $ bundle exec rake db:migrate
    $ budnle exec rake dev:seed
    
  Local de test etmek için
        
        $ rails s
        

yazarak çalıştırmıs oluyoruz [http://localhost:3000/ ](http://localhost:3000/ ) aderinden projenin çalışır halini görebilirsiniz
Admin olarak giriş yapmak için [http://localhost:3000/hq ](http://localhost:3000/hq ) adresini kullanın

Adminin e-posta ve parolası db/seeds.rb dosyasında yazıyor ordan bakabilirsiniz.

 
 
 
