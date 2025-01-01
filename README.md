# Sistem_Programlama





**HAZIRLAYANLAR:**

BERFİN GÖKÇE - 22060375

KEMALCAN ÇALIKOĞLU - 22060911

ÖNDER UMUT FİLİZ - 22060909

TAHA MUSTAFA AVCIOĞLU - 22060362


**Proje yapımız şu şekilde:** 

update/

├── bin/

│   ├── javafiles/

│   │   ├── Client.class

│   │   ├── ClientHasup.class

│   │   ├── HASUP.class

│   │   ├── Server.class

│   │   └── ServerHandler.class

│   ├── python/

│   │   ├── client.py

│   │   └── server.py

│   └── ruby/

│       ├── client.rb

│       └── server.rb

├── src/

    ├── javafiles/
    
    │   ├── Client.class
    
    │   ├── Client.java
    
    │   ├── ClientHasup.class
    
    │   ├── ClientHasup.java
    
    │   ├── HASUP.class
    
    │   ├── HASUP.java
    
    │   ├── Server.class
    
    │   ├── Server.java
    
    │   ├── ServerHandler.class
    
    │   └── ServerHandler.java
    
    ├── python/
    
    │   ├── client.py
    
    │   └── server.py
    
    └── ruby/
    
        ├── client.rb
        
        └── server.rb
        

![1](https://github.com/user-attachments/assets/00d9e457-2997-48d3-8a42-a5d357151991)

        

Bu kod, bir çoklu istemci destekli TCP sunucusu oluşturur. Kullanıcı kayıtlarını tutar ve istemcilerden gelen komutlara göre işlem yapar. İşleyişi şu şekilde özetleyebiliriz:

**1. Kütüphane İthalatı**

socket: Ağ bağlantıları oluşturmak için.
threading ve Lock: Aynı anda birden fazla istemciye hizmet verebilmek ve veri tutarlılığını sağlamak için.

**2. Kullanıcı Veritabanı ve Kilit**

users: Kullanıcı bilgilerini saklayan bir liste.
data_lock: Çoklu istemcinin aynı anda users listesine erişiminde veri tutarlılığını sağlamak için kullanılan kilit.

**3. Mesaj İşleme Fonksiyonu (process_message)**

KAYIT:<kullanıcı>: Kullanıcı bilgisi kaydeder.
GÖRÜNTÜLE: Kayıtlı tüm kullanıcıları döner.
Diğer Komutlar: Geçersiz komut mesajı gönderir.

**4. İstemci İşleme Fonksiyonu (handle_client)**

İstemciden gelen mesajları okur ve process_message ile işler.
Yanıtı istemciye geri gönderir.
İstemci bağlantısı kesilirse döngü sonlanır.

**5. Sunucuyu Başlatma (start_server)**

Sunucu bir soket oluşturur ve belirtilen porta bağlanır.
Bağlantıları dinler ve her istemci için bir yeni iş parçacığı başlatır.

**6. Ana Program**

start_server(8080): Sunucuyu 8080 portunda başlatır ve istemcilerle iletişim kurar.


![2](https://github.com/user-attachments/assets/63de87b0-b6ac-4b13-8917-4c499df85265)

Bu kod, TCP istemcisi oluşturur ve bir sunucuya bağlanarak kullanıcıdan gelen komutları gönderir ve yanıt alır. İşleyiş şu şekilde özetlenebilir:

**1. Kütüphane İthalatı**

socket: Ağ bağlantıları oluşturmak ve sunucuyla iletişim kurmak için kullanılan kütüphane.

**2. İstemci Başlatma Fonksiyonu (start_client)**

port: Bağlanılacak sunucunun port numarası.
socket.socket(socket.AF_INET, socket.SOCK_STREAM):
AF_INET: IPv4 adreslerini kullanır.
SOCK_STREAM: TCP protokolü ile çalışır.
connect(("localhost", port)):
İstemci, belirtilen sunucu (localhost) ve port numarasına bağlanır.

**3. Komut Gönderme ve Yanıt Alma**

Kullanıcıdan bir komut alınır (input("> ")).
Komut, sunucuya gönderilir (send(message.encode())).
Sunucudan gelen yanıt alınır (recv(1024).decode()) ve ekrana yazdırılır.

**4. Ana Program**

if __name__ == "__main__":: Kodun bağımsız çalışmasını sağlar.
start_client(8080): İstemciyi 8080 portundaki bir sunucuya bağlar.

![3](https://github.com/user-attachments/assets/2f35db72-2eed-453e-9fe5-5f68a7fe1ca0)


Bu Ruby kodu, çoklu istemci destekli bir TCP sunucusu oluşturur. Sunucu, istemcilerden gelen mesajları işler ve belirli komutlara göre cevaplar döner. İşleyiş şu şekilde açıklanabilir:

**Gerekli Kütüphaneler:**

socket kütüphanesi, TCP bağlantıları kurmak ve iletişim sağlamak için kullanılır.
thread kütüphanesi, aynı anda birden fazla istemciye hizmet verebilmek için çoklu iş parçacıkları (thread) kullanılır.

**Kullanıcı Veritabanı ve Kilit:**


users dizisi, kaydedilen kullanıcıları tutar.
mutex bir kilit nesnesidir, böylece birden fazla iş parçacığının aynı anda users dizisine erişmesini engeller ve veri tutarlılığını sağlar.

**Mesaj İşleme Fonksiyonu:**

process_message fonksiyonu, gelen mesajı işler:
Eğer mesaj "KAYIT:" ile başlıyorsa, bu mesajdaki kullanıcı bilgisi kaydedilir.
Eğer mesaj "GORUNTULE" ise, kayıtlı tüm kullanıcılar ekrana yazdırılır.
Diğer mesajlar için geçersiz komut yanıtı döndürülür.
Ayrıca mesajlar UTF-8 formatına zorla dönüştürülür.

**Sunucuyu Başlatma ve Bağlantıları Kabul Etme:**

Sunucu, localhost üzerinde 8081 portunu dinler ve gelen istemci bağlantılarını kabul eder.
İstemci İletişimi:

Her yeni istemci bağlantısı için ayrı bir iş parçacığı (thread) başlatılır.
Bu iş parçacığı, istemciden gelen mesajı alır, işlemi yapar ve yanıtı geri gönderir.
Her istemciden gelen mesajlar, UTF-8 formatında işlenir.

**İstemci Bağlantısının Kapanması:**

Mesajlar işlendiğinde, istemci bağlantısı kapatılır.

![4](https://github.com/user-attachments/assets/37989cec-93e9-43bc-86a6-be7fca78e5ac)

**Gerekli Kütüphane İthalatı:**

require 'socket': socket kütüphanesini içeri aktarır. Bu kütüphane, TCP/IP üzerinden bağlantı kurmak ve veri iletmek için kullanılır.
Bağlantı Kurulması:

socket = TCPSocket.new('localhost', 8081): localhost adresi ve 8081 portu ile bir TCP istemcisi soketi oluşturulur ve sunucuya bağlanılır.

**Başlangıç Mesajı:**

puts "Bağlantı kuruldu. Komutlarınızı yazın:": Bağlantı başarılı bir şekilde kurulduğunda, ekrana bir bilgi mesajı yazdırılır.

**Mesaj Alma Döngüsü:**

loop do: Sonsuz bir döngü başlatılır. Bu döngüde kullanıcıdan sürekli olarak mesaj alınır ve işlem yapılır.
print "> ": Kullanıcıdan mesaj almak için ekrana bir prompt (">") yazdırılır.
message = gets.chomp: Kullanıcıdan bir satır girişi alınır ve satır sonu karakteri (\n) kaldırılır.

socket.puts message: Kullanıcının yazdığı mesaj, TCP soketi üzerinden sunucuya gönderilir.

**Sunucudan Yanıt Alma:**

response = socket.gets: Sunucudan gelen yanıt bir satır olarak alınır.
Yanıtın UTF-8 Formatına Dönüştürülmesi:

response = response.encode('UTF-8', invalid: :replace, undef: :replace, replace: '?') if response.encoding.name != 'UTF-8': Sunucudan gelen yanıtın karakter kodlaması UTF-8 değilse, yanıt UTF-8 formatına dönüştürülür.

**Yanıtın Ekrana Yazdırılması:**

puts response: Sunucudan alınan yanıt ekrana yazdırılır.

![5](https://github.com/user-attachments/assets/f2415a80-7f6e-4932-979e-1aa2b74931f1)


**Port Numarasının ve Pool'un Tanımlanması:**

int port = 8082;: Sunucunun dinleyeceği port numarası 8082 olarak belirlenir.
HASUP hasup = new HASUP();: HASUP sınıfından bir nesne oluşturulur (bu sınıfın içeriği kodda gösterilmemiş, ancak veritabanı veya işlem yöneticisi olabilir).
ExecutorService pool = Executors.newFixedThreadPool(10);: 10 iş parçacığına kadar eş zamanlı işlem yapabilmek için bir iş parçacığı havuzu (pool) oluşturulur.

**Sunucunun Başlatılması:**

try (ServerSocket serverSocket = new ServerSocket(port)) { ... }: ServerSocket nesnesi, belirtilen portta istemci bağlantılarını kabul edebilmek için oluşturulur. Bu satırda ServerSocket otomatik olarak kapatılacaktır.
System.out.println("Sunucu " + port + " portunda başlatıldı...");: Sunucu başlatıldığında, belirtilen port numarasına dair bilgi ekrana yazdırılır.

**İstemci Bağlantılarının Kabul Edilmesi:**

while (true) { ... }: Sonsuz bir döngü başlatılır, böylece sunucu sürekli olarak istemci bağlantılarını dinler.
Socket clientSocket = serverSocket.accept();: serverSocket.accept() metodu, istemciden gelen bağlantıyı kabul eder ve bir Socket nesnesi oluşturur.

**İş Parçacığının Başlatılması:**

pool.execute(new ServerHandler(clientSocket, hasup));: Her bir istemci bağlantısı için yeni bir iş parçacığı (ServerHandler) başlatılır. Bu iş parçacığı, istemci bağlantısını işlemek için clientSocket ve hasup nesnelerini kullanacaktır.

**Hata Yönetimi:**

} catch (IOException e) { ... }: Bağlantı sırasında bir hata oluşursa, bu hata yakalanır ve ekrana yazdırılır.

![6](https://github.com/user-attachments/assets/e69f2ad7-e72e-49f3-bfdd-f498944e31f7)

**Sınıf Tanımlaması:**

public class ServerHandler implements Runnable { ... }: ServerHandler sınıfı, istemciyle iletişimi yönetmek için kullanılan bir iş parçacığı (thread) sınıfıdır. Bu sınıf, Runnable arayüzünü implement eder, yani bir iş parçacığı olarak çalışacak bir görev tanımlar.

**Değişkenler:**

private final Socket clientSocket;: Bu sınıfın her örneği için bir istemci bağlantısını temsil eden Socket nesnesi tanımlanır.
private final HASUP hasup;: HASUP sınıfı bir işlevsellik nesnesi olabilir ve mesajları işlemeyi sağlar. Bu sınıf, bağlantıya dair işlem veya veri yönetimi işlevlerini yerine getirir.

**Konstruktor (Yapıcı) Metod:**

public ServerHandler(Socket clientSocket, HASUP hasup) { ... }: ServerHandler sınıfının yapıcı metodu, istemci bağlantısını (clientSocket) ve HASUP nesnesini alır ve bu verileri sınıfın örnek değişkenlerine atar.

**run Metodu:**

@Override public void run() { ... }: Runnable arayüzü ile zorunlu olarak implement edilen run metodudur. Bu metod, iş parçacığı çalıştırıldığında gerçekleştirilecek işlemi tanımlar.

**I/O Akışları (Input/Output Streams):**

try (BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream())); ... ): Bu satırda, istemciden gelen veriyi okumak için bir BufferedReader ve istemciye veri göndermek için bir PrintWriter nesnesi oluşturulur. Her iki akış da clientSocket üzerinden alınır.
in.readLine(): İstemciden bir satır okur. Eğer bir mesaj alınırsa, mesaj işlenmek üzere message değişkenine atanır.
out.println(response): Sunucudan alınan cevap, istemciye gönderilir. Her response bir işlem sonucudur (örneğin, HASUP sınıfı tarafından üretilen bir yanıt).

**Mesajın İşlenmesi:**

String response = hasup.processMessage(message);: İstemciden alınan mesaj, hasup nesnesi tarafından işlenir. processMessage metodu, mesajı işler ve bir yanıt (response) döner.

**Hata Yönetimi:**

} catch (IOException e) { ... }: Bu blok, herhangi bir I/O hatasını yakalar ve hata mesajını ekrana yazdırır.

![7](https://github.com/user-attachments/assets/9e7739c4-74dc-41b5-9038-5341f3f3cfa2)

**Değişkenler:**

String host = "localhost";: Sunucunun adresi (localhost), istemciye bağlanılacak adresi belirtir.
int port = 8082;: Bağlanılacak port numarası (8082), sunucu ile iletişim için kullanılan portu belirtir.

**Bağlantı Kurulması:**

try (Socket socket = new Socket(host, port); ... ): Sunucuya bağlanmak için bir Socket nesnesi oluşturulur. Bu Socket, istemci ve sunucu arasındaki iletişimi sağlar. Bu nesne, bağlantı sağlandığında otomatik olarak kapatılır.
BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));: Sunucudan gelen verileri okumak için BufferedReader nesnesi oluşturulur.
PrintWriter out = new PrintWriter(socket.getOutputStream(), true);: Sunucuya veri göndermek için PrintWriter nesnesi oluşturulur. İkinci parametre (true), çıkış akışının her println işleminde otomatik olarak flush edilmesini sağlar.
Scanner scanner = new Scanner(System.in);: Kullanıcıdan komut almak için Scanner nesnesi oluşturulur.

**Kullanıcıdan Giriş Alma ve Gönderme:**

System.out.println("Bağlantı kuruldu. Komutlarınızı yazın:");: Bağlantı kurulduğunda ekrana bilgi mesajı yazdırılır.
while (true) { ... }: Sonsuz bir döngü başlatılır, böylece istemci sürekli olarak komutlar alıp gönderebilir.
System.out.print("> ");: Kullanıcıdan komut almak için ekrana bir prompt (> ) yazdırılır.
String command = scanner.nextLine();: Kullanıcıdan bir komut alınır.
out.println(command);: Alınan komut, sunucuya gönderilir.

**Sunucudan Yanıt Alma ve Yazdırma:**

System.out.println(in.readLine());: Sunucudan gelen yanıt, BufferedReader üzerinden okunur ve ekrana yazdırılır.

**Hata Yönetimi:**

catch (IOException e) { e.printStackTrace(); }: Bu blok, herhangi bir I/O hatasını yakalar ve hata mesajını ekrana yazdırır.


![8](https://github.com/user-attachments/assets/a273f8f6-bbad-4b31-81b9-6c9bcfb37e3a)

**Metod Tanımlaması:**

public synchronized String processMessage(String message) { ... }: Bu metod, bir mesaj alır ve mesajın içeriğine göre uygun bir yanıt döndürür. synchronized anahtar kelimesi, bu metodun birden fazla iş parçacığı tarafından aynı anda çalıştırılmasını engeller, yani thread-safe olmasını sağlar.

**Mesaj İşleme:**

message = message.trim();: Gelen mesajdaki baştaki ve sondaki boşluklar temizlenir.
if (message.startsWith("KAYIT:")) { ... }: Eğer mesaj, "KAYIT:" ile başlıyorsa, kullanıcı bilgisi kaydedilmeye çalışılır.
String userInfo = message.substring(6).trim();: Mesajın başındaki "KAYIT:" kısmı kaldırılır ve kalan kısım kullanıcı bilgisi olarak alınır.
users.add(userInfo);: Kullanıcı bilgisi, users listesinin sonuna eklenir.
return "Kullanıcı başarıyla kaydedildi: " + userInfo;: Kullanıcı başarıyla kaydedildikten sonra bir başarı mesajı döndürülür.
else if (message.equalsIgnoreCase("GORUNTULE")) { ... }: Eğer mesaj "GORUNTULE" ise, tüm kayıtlı kullanıcıların listesi döndürülür.
return "Kayıtlı kullanıcılar: " + String.join(", ", users);: users listesindeki tüm kullanıcılar, virgül ile ayrılarak birleştirilir ve döndürülür.
else { return "Geçersiz komut."; }: Eğer mesaj yukarıdaki iki durumu da sağlamıyorsa, geçersiz komut mesajı döndürülür.

![9](https://github.com/user-attachments/assets/37993a8b-381f-4fa6-8519-a94b49c4b9d4)


**Üye Değişkenleri:**

private final Socket socket;: İstemci ile sunucu arasında bağlantı sağlayan Socket nesnesi.
private final BufferedReader in;: Sunucudan gelen veriyi okumak için kullanılan BufferedReader nesnesi.
private final PrintWriter out;: Sunucuya veri göndermek için kullanılan PrintWriter nesnesi.

**Yapıcı Metod (Constructor):**

public ClientHasup(String host, int port) throws IOException { ... }: Bu metod, istemci nesnesini başlatmak için kullanılır. Parametre olarak verilen host ve port bilgileriyle sunucuya bağlanır.
this.socket = new Socket(host, port);: Verilen host ve port bilgilerini kullanarak sunucuya bağlanılır.
this.in = new BufferedReader(new InputStreamReader(socket.getInputStream()));: Sunucudan gelen veriyi okumak için bir BufferedReader oluşturulur.
this.out = new PrintWriter(socket.getOutputStream(), true);: Sunucuya veri göndermek için bir PrintWriter oluşturulur. true parametresi, otomatik flush (veriyi hemen gönderme) sağlar.

**Komut Gönderme Metodu:**

public void sendCommand(String command) throws IOException { ... }: Bu metod, sunucuya bir komut gönderir.
out.println(command);: PrintWriter kullanarak, komut satırını sunucuya gönderir.

**Yanıt Alma Metodu:**

public String receiveResponse() throws IOException { ... }: Bu metod, sunucudan gelen yanıtı alır.
return in.readLine();: BufferedReader kullanarak, sunucudan bir satır okuyup döndürür.

**Bağlantıyı Kapatma Metodu:**

public void close() throws IOException { ... }: Bu metod, istemci bağlantısını sonlandırmak için kullanılır.
in.close();: BufferedReader nesnesini kapatır.
out.close();: PrintWriter nesnesini kapatır.
socket.close();: Socket nesnesini kapatır, böylece bağlantı sona erdirilir.




Kodların anlatıldığı youtube linki: https://www.youtube.com/watch?v=s2OCcXZ8ebE
