#### Rails de Authentication için Devise Nasıl Kullanılır



Devise, rails uygulamaları için popüler bir
kimlik doğrulama gemi dir.Bu yazıda gemi mizin kullanımını sıfırdan bir proje oluşturarak anlatıcam
eğer var olan bir projenizde kullanacaksanız gem kurulum aşamasından
başlayarak projenize ekleyebilirsiniz

    $ rails new devise_test
    
   diyerek bir rails projesi oluşturuyoruz
   
    $ cd devise_tes  # proje klasorune giriyoruz
    
  
Projemiz için bir controller oluşturuyoruz

    $ rails generate controller welcome index
    
 config/routes.rb dosyasını açıp aşağıdaki satırı ekliyoruz
 
    root 'welcome#index'
    
   Bundan sonra gem kurulum işlemlerine başlayabiliriz [https://rubygems.org/gems/devise ](https://rubygems.org/gems/devise)
   sayfasından sağdaki Gemfile kısmından gemi kopyalıyoruz.Kopyaladığımız gemi Gemfile dosyasında group:development,:test do alanına ekliyoruz.
   
    group :development, :test do
      gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
      gem 'capybara', '~> 2.13'
      gem 'selenium-webdriver'
      gem 'devise', '~> 4.3'
    end
    
 Yukardaki işlemleri yaptıktan sonra gem in kurulması için terminale aşağıdaki kodu yazıyoruz.
 
    $ bundle install
    
    
 gem kullanıma hazır
 
    $ rails g devise:install
    
  Bu komuttan sonra ekranda gözüken adımları takip etmemiz yeterli
  ![]([Imgur](http://i.imgur.com/Lr1CqNK.jpg))
config/environments/development.rb dosyasında aşağıdaki satır yoksa ekleyin öncelikle

    config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }

app/views/application.html.erb dosyasındaki body kısmına aşağıdaki satırları ekliyoruz.

      <body>
           <p class="notice"><%= notice %></p>
           <p class="alert"><%= alert %></p>
        <%= yield %>
      </body>
 
 Devise views oluşturmak için aşağıdaki komutu yazıyoruz.
    
    $ rails g devise:views
 
Şimdi devise için model oluşturacağız User,Admin vb gibi

    $ rails g devise User
    $ rake db:migrate
 
 Gem ile ilgili işlemler bu kadar test etmek için;
 
    $ rails s
    
 [http://localhost:3000/users/sign_in](http://localhost:3000/users/sign_in)
 
 [http://localhost:3000/users/sign_up](http://localhost:3000/users/sign_up)   

Gem kurulumu ile ilgili [https://github.com/plataformatec/devise](https://github.com/plataformatec/devise) sayfasından da yardım alabilirsiniz.
