# Sosyal Medya Hesapları İle Giriş Postman Testleri
Giriş/Kayıt ekranlarında kullanılan isim, soyisim, email, şifre kullanılarak yapılan işlemler aynı zamanda sosyal medya hesapları ile de yapılabilmektedir. Bu döküman google, facebook, microsoft ve apple hesapları ile giriş/kayıt işlemlerinin Postman testleri nasıl yapıldığını anlatmaktadır.

## 1. Google Kayıt/Giriş Testleri

Postman üzerinden yapılması gereken adımlar:

- **Postman'de** `Authorization` sekmesinden, `Auth Type` olarak `OAuth 2.0` seçilir. 
- **Token Name** alanına uygun bir isim girilebilir.
- **Grant Type** alanında **Authorization Code** seçilir.
- **Callback URL** alanına, **Developer Console** ekranında oluşturduğunuz uygulamanın `Redirect API` adresini girmelisiniz.
- **Auth URL** kısmına aşağıdaki URL girilmelidir:
    - https://accounts.google.com/o/oauth2/auth
    - Bu URL, Google'ın OAuth 2.0 yetkilendirme işlemleri için kullanılan yetkilendirme uç noktasıdır.
- **Access Token URL** kısmına şu URL girilmelidir:
    - https://oauth2.googleapis.com/token
    - Bu URL, Google'ın OAuth 2.0 token almak için kullanılan uç noktasıdır.
- **Client ID** alanına, Google Developer Console üzerinden oluşturduğunuz OAuth 2.0 istemci kimlik bilgilerini girmeniz gerekmektedir. Bu bilgiyi şu adımlarla bulabilirsiniz:
  - **Google Developer Console**'a gidin.
  - İlgili projenizi seçin.
  - **API ve Hizmetler > Kimlik Bilgileri** sekmesinde, OAuth 2.0 istemci kimlik bilgilerinizi görüntüleyebilir ve kopyalayabilirsiniz.
- **Client Secret** alanına, Google Developer Console üzerinden oluşturduğunuz OAuth 2.0 istemci kimlik bilgileriyle birlikte verilen Client Secret bilgisini girmeniz gerekmektedir. Bu bilgiyi şu adımlarla bulabilirsiniz:
  -  Google Developer Console'a gidin.
  - İlgili projenizi seçin.
  - API ve Hizmetler > Kimlik Bilgileri sekmesinde, OAuth 2.0 istemci kimlik bilgilerinizi görüntüleyebilir ve kopyalayabilirsiniz.

- **Scope** alanına, kullanıcıdan hangi izinleri talep ettiğinizi belirtmeniz gerekmektedir. Google için en yaygın kullanılan scope'lar şunlardır:

  - `email`: Kullanıcının e-posta adresine erişim izni verir.
  - `profile`: Kullanıcının profil bilgilerine erişim izni verir.
  - `openid`: OpenID Connect ile kullanıcı doğrulama işlemi yapar.
  - Örneğin, Google'dan temel profil bilgileri almak için şu scope'u kullanabilirsiniz:

    - `openid profile email`

- **State** alanı isteğe bağlıdır ancak güvenlik açısından önemlidir. Bu alan, saldırılara karşı korunmak için kullanılır ve oturumunuzu başlatan isteği doğrulamak için kullanılabilir. Bu değeri, test işlemleri için herhangi bir benzersiz string ile doldurabilirsiniz. Örneğin:
  - `123456`

- **Client Authentication** kısmında, Basic Auth veya Body seçenekleri bulunabilir. Google API'leri için Basic Auth kullanmak yaygındır. Bu durumda:

  - **Username** kısmına Client ID,
  - **Password** kısmına ise Client Secret girilir.

Bu şekilde Google OAuth 2.0 ile giriş ve kayıt işlemlerini Postman üzerinden başarılı bir şekilde test edebilirsiniz.


### Konfigürasyon ve Gereksinimler:
- Bu işlemi yapmadan önce, **Google Developer Console** üzerinden OAuth 2.0 istemci kimlik bilgilerinizi oluşturmanız gerekmektedir.
- Test işlemi başarılı olduğunda, Google hesabı ile giriş yapmış veya kayıt işlemini gerçekleştirmiş olacaksınız.

## 2. Microsoft Kayıt/Giriş Testleri

Postman üzerinden yapılması gereken adımlar:

- Postman'de `Authorization` sekmesinden, `Auth Type` olarak `OAuth 2.0` seçilir.
- **Token Name** alanına uygun bir isim girilebilir.
- **Grant Type** alanında Authorization Code seçilir.
- **Callback URL** alanına, Azure Portal üzerinden aldığınız Redirect URI adresini girmelisiniz.
- **Auth URL** kısmına aşağıdaki URL girilmelidir:
  - https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
  - `{tenant}` kısmını, Azure'da kullandığınız kiracı kimliği ile değiştirin. Eğer belirli bir kiracınız yoksa, `common` veya `organizations` gibi genel değerler kullanabilirsiniz.
  - Bu URL, Microsoft'un OAuth 2.0 yetkilendirme işlemleri için kullanılan yetkilendirme uç noktasıdır.
- **Access Token URL** kısmına şu URL girilmelidir:
  - https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
  - `{tenant}` kısmını, kiracı kimliğinizle değiştirin. Bu URL, Microsoft'un OAuth 2.0 token almak için kullanılan uç noktasıdır.
- **Client ID** alanına, Azure Portal üzerinden oluşturduğunuz OAuth 2.0 istemci kimlik bilgilerini girmeniz gerekmektedir. Bu bilgiyi şu adımlarla bulabilirsiniz:
  - **Azure Portal**'a gidin.
  - İlgili projenizi seçin.
  - **Uygulama Kaydı > Kimlik Bilgileri** sekmesinde, Application (client) ID'yi görüntüleyebilir ve kopyalayabilirsiniz.
- **Client Secret** alanına, Azure Portal üzerinden oluşturduğunuz Client Secret bilgisini girmeniz gerekmektedir. Bu bilgiyi şu adımlarla alabilirsiniz:
  - **Azure Portal**'a gidin.
  - İlgili uygulamanızı seçin.
  - **Sertifikalar & gizlilikler** sekmesinden yeni bir Client Secret oluşturun.
  - Oluşturduktan sonra bu secret'ı kopyalayın ve Client Secret alanına yapıştırın.
- **Scope** alanına, kullanıcıdan hangi izinleri talep ettiğinizi belirtmeniz gerekmektedir. Microsoft için en yaygın kullanılan scope'lar şunlardır:
  - `openid`: OpenID Connect ile kullanıcı doğrulama işlemi yapar.
  - `profile`: Kullanıcının profil bilgilerine erişim izni verir.
  - `email`: Kullanıcının e-posta adresine erişim izni verir.
  - `User.Read`: Kullanıcının temel profil bilgilerine erişim izni verir.
  - Örneğin, Microsoft'dan temel profil bilgileri almak için şu scope'u kullanabilirsiniz:
    - `openid profile email User.Read`
- **State** alanı isteğe bağlıdır ancak güvenlik açısından önemlidir. Bu alan, saldırılara karşı korunmak için kullanılır ve oturumunuzu başlatan isteği doğrulamak için kullanılabilir. Bu değeri, test işlemleri için herhangi bir benzersiz string ile doldurabilirsiniz. Örneğin:
  - `123456`
- **Client Authentication** kısmında, Basic Auth veya Body seçenekleri bulunabilir. Body seçeneğini seçebilirsiniz.

- **Konfigürasyon ve Gereksinimler:**
  - Bu işlemi yapmadan önce, Azure Portal üzerinden OAuth 2.0 istemci kimlik bilgilerinizi oluşturmanız gerekmektedir.
  - Test işlemi başarılı olduğunda, Microsoft hesabı ile giriş yapmış veya kayıt işlemini gerçekleştirmiş olacaksınız.

## 3. Facebook Kayıt/Giriş Testleri



## 4. Apple Kayıt/Giriş Testleri
