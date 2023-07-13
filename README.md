# LambdaTest'te JUnit ile Selenium Testlerini Çalıştırma

![image](https://user-images.githubusercontent.com/70570645/171432631-dcc31b10-6590-4877-98c0-4ac702fbd441.png)

<p align="center">
  <a href="https://www.linkedin.com/in/teykinaycerkezoglu/" target="_bank">Linkedin</a>
  &nbsp; &#8901; &nbsp;
  
</p>
&emsp;
&emsp;
&emsp;

*Java otomasyon testi betiklerinizi LambdaTest platformunda yapılandırmak ve çalıştırmak için JUnit çerçevesini nasıl kullanacağınızı öğrenin*

[<img height="58" width="200" src="https://user-images.githubusercontent.com/70570645/171866795-52c11b49-0728-4229-b073-4b704209ddde.png">](https://accounts.lambdatest.com/register?utm_source=github&utm_medium=repo&utm_campaign=junit-selenium-sample)


## İçindekiler

* [Pre-requisites](#pre-requisites)
* [İlk Testinizi Yapın](#run-your-first-test)
* [JUnit ile Paralel Test](#run-parallel-tests-using-junit)
* [JUnit ile Yerel Test](#testing-locally-hosted-or-privately-hosted-projects)

## Pre-requisites

Selenium ile Java otomasyon testi yapmaya başlamadan önce yapmanız gerekenler:

**- En son **Java development environment**, yani **JDK 1.6** veya üstünü yükleyin. En son sürümü kullanmanızı öneririz.**

En son **Selenium Client** ve **WebDriver gereksinimlerini** [resmi web sitesinden](https://www.selenium.dev/downloads/) indirin. Selenium Client ve WebDriver'ın en son sürümleri, otomasyon betiğinizi LambdaTest Selenium cloud grid'de çalıştırmanız için idealdir.

-  **JUnit** çerçevesini destekleyen **Maven**'i kurun. **Maven**, [resmi web sitesindeki](https://maven.apache.org/) adımlar izlenerek indirilebilir ve kurulabilir. Maven ayrıca [Homebrew](https://brew.sh/) paket yöneticisi kullanılarak **Linux/MacOS** üzerine kolayca kurulabilir.

- Yerel projeniz üzerinde çalışıyorsanız, aşağıdaki maven bağımlılığını pom.xml dosyanıza eklemeniz gerekir.
  ```xml
  <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
  </dependency>
  ```

### Depoyu Klonlama ve Bağımlılıkları Kurma

**1. Adım:** LambdaTest'in JUnit-Selenium-Sample deposunu kopyalayın ve aşağıda gösterildiği gibi kod dizinine gidin:

```bash
git clone https://github.com/LambdaTest/junit-selenium-sample
cd junit-selenium-sample
```

Eski versionları kontrol etmek için aşağıdaki komutu da çalıştırmak isteyebilirsiniz.

```bash
mvn versions:display-dependency-updates
```

### Authentication Ayarlama

Test otomasyon komut dosyalarını çalıştırmak için LambdaTest kimlik bilgilerinizin yanınızda olduğundan emin olun. Bu kimlik bilgilerini [LambdaTest Automation Dashboard](https://automation.lambdatest.com/build?utm_source=github&utm_medium=repo&utm_campaign=junit-Selenium-sample) veya [LambdaTest Profilinizden](https://accounts) alabilirsiniz. .lambdatest.com/login?utm_source=github&utm_medium=repo&utm_campaign=junit-selenium-sample).
**Adım 2:** environment variableslarda LambdaTest **Kullanıcı Adı** ve **Erişim Anahtarı**'nı ayarlayın.

* For **Linux/macOS**:
  
  ```bash
  export LT_USERNAME="YOUR_USERNAME" 
  export LT_ACCESS_KEY="YOUR ACCESS KEY"
  ```
  * For **Windows**:
  ```bash
  set LT_USERNAME="YOUR_USERNAME" 
  set LT_ACCESS_KEY="YOUR ACCESS KEY"
  ```

##İlk Testinizi Yapın

>**Test Senaryosu**: Örnek dosya: [JUnitTodo.java](https://github.com/LambdaTest/junit-Selenium-sample/blob/master/src/test/java/com/lambdatest/JUnitTodo.java) . Bu JUnit Selenium betiği, birkaç öğeyi tamamlandı olarak işaretleyerek, listeye yeni bir öğe ekleyerek ve son olarak bekleyen öğelerin sayısını çıktı olarak görüntüleyerek örnek bir to-do list uygulamasını test eder.

### Configuring Test Capabilities

**3. Adım:** Test komut dosyasında, test yeteneklerinizi güncellemeniz gerekir. Bu kodda, yetenekler nesnesi aracılığıyla LambdaTest Selenium grid capabilities ile birlikte tarayıcı, tarayıcı sürümü ve işletim sistemi bilgilerini aktarıyoruz. Yukarıdaki koddaki capabilities nesnesi şu şekilde tanımlanır:

```java
DesiredCapabilities capabilities = new DesiredCapabilities();
        capabilities.setCapability("browserName", "chrome");
        capabilities.setCapability("version", "70.0");
        capabilities.setCapability("platform", "win10"); // If this cap isn't specified, it will just get the any available one
        capabilities.setCapability("build", "LambdaTestSampleApp");
        capabilities.setCapability("name", "LambdaTestJavaSample");
        capabilities.setCapability("network", true); // To enable network logs
        capabilities.setCapability("visual", true); // To enable step by step screenshot
        capabilities.setCapability("video", true); // To enable video recording
        capabilities.setCapability("console", true); // To capture console logs
```

[Desired Capability Generator](https://www.lambdatest.com/capabilities-generator/?utm_source=github&utm_medium=repo&utm_campaign=junit-Selenium-sample) yardımıyla test gereksinimleriniz için capabilities'leri oluşturabilirsiniz.

### Executing the Test

**Adım 4:** Testler, aşağıdaki komut kullanılarak terminalde gerçekleştirilebilir.

```bash
mvn test -P single
```

Test sonuçlarınız test konsolunda (veya terminal/cmd kullanıyorsanız komut satırı arabiriminde) ve [LambdaTest otomasyon panosunda](https://automation.lambdatest.com/build) görüntülenecektir.

## Run Parallel Tests Using JUnit

Çalıştırmak için kullandığımız [Parallelized.java](https://github.com/LambdaTest/junit-Selenium-sample/blob/master/src/test/java/com/lambdatest/Parallelized.java) class'ına göz atın. JUnit kullanarak Paralel Testler.


JUnit otomasyon çerçevesi kullanarak paralel test yürütmek için [JUnitConcurrentTodo.java](https://github.com/LambdaTest/junit-selenium-sample/blob/master/src/test/java/com/lambdatest/JUnitConcurrentTodo.java) dosyasına bakın. 

### Executing Parallel Tests Using JUnit

**JUnit** kullanarak paralel testler yapmak için terminalde aşağıdaki komutu çalıştırmamız gerekir:

```bash
mvn test -P parallel
```

## Yerel Olarak Barındırılan veya Özel Olarak Barındırılan Projeleri Test Etme

Yerel olarak barındırılan veya özel olarak barındırılan projelerinizi LambdaTest Tunnel kullanarak LambdaTest Selenium grid ile test edebilirsiniz. Tek yapmanız gereken, tüneli kullanarak bir SSH tüneli kurmak ve istenen yetenekler aracılığıyla toggle `tunnel = True`yu geçmek. LambdaTest Tüneli, yerel olarak barındırılan veya özel olarak barındırılan sayfalarınızı canlı yayına girmeden önce bile test etmenize izin veren güvenli bir SSH protokolü tabanlı tünel oluşturur.
Daha fazla bilgi için [LambdaTest Tüneli belgelerimize](https://www.lambdatest.com/support/docs/testing-locally-hosted-pages/?utm_source=github&utm_medium=repo&utm_campaign=junit-selenium-sample) bakın.
İşte LambdaTest Tüneli'ni nasıl kurabileceğiniz.

Şunun binary file'ını indirin:
* [LambdaTest Tunnel for Windows](https://downloads.lambdatest.com/tunnel/v3/windows/64bit/LT_Windows.zip)
* [LambdaTest Tunnel for macOS](https://downloads.lambdatest.com/tunnel/v3/mac/64bit/LT_Mac.zip)
* [LambdaTest Tunnel for Linux](https://downloads.lambdatest.com/tunnel/v3/linux/64bit/LT_Linux.zip)

Komut istemini açın ve binary file'a gidin.

Run the following command:

```bash
LT -user {user’s login email} -key {user’s access key}
```
**Dolayısıyla, kullanıcı adınız lambdatest@example.com ve anahtar 123456 ise, komut şöyle olacaktır:**

```bash
LT -user lambdatest@example.com -key 123456
```
**LambdaTest Tunnel**'e başarıyla bağlanabildiğinizde, aşağıda gösterilen kodda tünel özelliklerini aktarmanız yeterlidir:

**Tunnel Capability**

```java
DesiredCapabilities capabilities = new DesiredCapabilities();        
        capabilities.setCapability("tunnel", true);
```

## Dokümantasyon ve Kaynaklar :books:

      
Visit the following links to learn more about LambdaTest's features, setup and tutorials around test automation, mobile app testing, responsive testing, and manual testing.

* [LambdaTest Documentation](https://www.lambdatest.com/support/docs/?utm_source=github&utm_medium=repo&utm_campaign=junit-selenium-sample)
* [LambdaTest Blog](https://www.lambdatest.com/blog/?utm_source=github&utm_medium=repo&utm_campaign=junit-selenium-sample)
* [LambdaTest Learning Hub](https://www.lambdatest.com/learning-hub/?utm_source=github&utm_medium=repo&utm_campaign=junit-selenium-sample)    

## LambdaTest Community :busts_in_silhouette:

The [LambdaTest Community](https://community.lambdatest.com/?utm_source=github&utm_medium=repo&utm_campaign=junit-selenium-sample) allows people to interact with tech enthusiasts. Connect, ask questions, and learn from tech-savvy people. Discuss best practises in web development, testing, and DevOps with professionals from across the globe 🌎

## LambdaTest'te yenilikler ❓

To stay updated with the latest features and product add-ons, visit [Changelog](https://changelog.lambdatest.com) 
      
## LambdaTest Hakkında

[LambdaTest](https://www.lambdatest.com/?utm_source=github&utm_medium=repo&utm_campaign=junit-selenium-sample) is a leading test execution and orchestration platform that is fast, reliable, scalable, and secure. It allows users to run both manual and automated testing of web and mobile apps across 3000+ different browsers, operating systems, and real device combinations. Using LambdaTest, businesses can ensure quicker developer feedback and hence achieve faster go to market. Over 500 enterprises and 1 Million + users across 130+ countries rely on LambdaTest for their testing needs.    

### Özellikler

* 3000'den fazla gerçek masaüstü ve mobil ortamda Selenium, Cypress, Puppeteer, Playwright ve Appium otomasyon testlerini çalıştırın.
* 3000'den fazla ortamda gerçek zamanlı çapraz tarayıcı testi.
* Gerçek cihaz bulutunda test edin
* HyperExecute ile ışık hızında test otomasyonu
* Ölçekte Test ile testi hızlandırın, iş sürelerini kısaltın ve kod değişiklikleri hakkında daha hızlı geri bildirim alın.
* Bulutta Akıllı Görsel Regresyon Testi
* CI/CD, Proje Yönetimi, Kodsuz Otomasyon ve daha fazlası için favori aracınızla 120'den fazla üçüncü taraf entegrasyonu.
* Tek bir tıklamayla birden çok tarayıcıda Otomatik Ekran Görüntüsü testi.
* Web ve mobil uygulamaların yerel testi.
* 3000'den fazla masaüstü ve mobil tarayıcı, tarayıcı sürümü ve işletim sisteminde Çevrimiçi Erişilebilirlik Testi.
* 53'ten fazla ülkede web ve mobil uygulamaların coğrafi konum testi.
* LT Tarayıcı - önceden yüklenmiş 50'den fazla mobil cihaz, tablet, masaüstü ve dizüstü bilgisayar görüntü alanında yanıt testi için

    
[<img height="58" width="200" src="https://user-images.githubusercontent.com/70570645/171866795-52c11b49-0728-4229-b073-4b704209ddde.png">](https://accounts.lambdatest.com/register)

      
## We are here to help you :headphones:

* Got a query? we are available 24x7 to help. [Contact Us](mailto:support@lambdatest.com)
* For more info, visit - [LambdaTest](https://www.lambdatest.com/?utm_source=github&utm_medium=repo&utm_campaign=junit-selenium-sample)
