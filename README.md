# YOLO-Webcam
Ultralytics, YOLO modelini kullanarak nesne algılama ve diğer görsel algılama görevleri için bir Python kütüphanesidir.

from ultralytics import YOLO

kodu, Ultralytics kütüphanesinde bulunan YOLO sınıfını içe aktarır.
Bu sınıf, YOLO modelini oluşturmak, eğitmek ve kullanmak için kullanılan bir arayüz sağlar.
YOLO sınıfı, PyTorch'un gücünü kullanarak nesne algılama görevlerini kolayca gerçekleştirmenize olanak tanır.

model = YOLO('../YOLO-Weights/yolov8l.pt')

Bir YOLOv8 modelini önceden eğitilmiş ağırlıklarıyla yükleyerek bir model değişkenine atandığını söylemektedir.
Bu noktadan sonra, model değişkeni üzerinden nesne algılama ve diğer görevleri gerçekleştirmek mümkün olacaktır.


results = model("Images/trafik.jpg",show=True)

Bu kod satırı, bir YOLO modelini kullanarak bir görüntüde nesne algılama yapmayı sağlar. İlgili parametrelerle birlikte şu işlevselliği sağlar:

model: Bu, YOLO modelini temsil eden bir değişken veya nesnedir.
"Images/trafik.jpg": Algılama yapılacak olan görüntünün dosya yolu.
Bu örnekte "trafik.jpg" adlı bir görüntü kullanılır.
İlgili görüntü dosyasının yolu doğru bir şekilde belirtilmelidir.
show=True: Bu parametre, algılama sonuçlarını görüntülemenin isteğe bağlı olduğunu belirtir.
Eğer show=True olarak ayarlanırsa, nesne algılama sonuçları görüntü üzerinde işaretlenecek ve görsel olarak görüntülenecektir.
Bu kod, belirtilen görüntü üzerindeki nesneleri algılayacak ve bu nesneleri çerçeve içine alarak görsel olarak göstermek için kullanılır.
Algılama sonuçları, results değişkenine atanır ve bu sonuçlar daha sonra başka işlemler için kullanılabilir.



cap = cv2.VideoCapture(0) 

Bu kodun çalıştırılması, belirtilen kamera cihazından veya video kaynağından canlı bir video akışı almak ve bu akışı işlemek için bir VideoCapture nesnesi oluşturacaktır.
VideoCapture : Bir video kaynağını açmak için kullanılan bir sınıftır.
0 : Parametre olarak verilen sayı, kullanılacak video kaynağını belirtir.
Burada 0, bilgisayarınıza bağlı olan ve varsayılan olarak birinci kamera cihazını temsil eder.
Eğer birden fazla kamera veya başka bir video kaynağı varsa, bu değeri değiştirerek farklı kaynakları seçebilirsiniz.


cap.set(3,1280)
cap.set(4,720)

Bu kod satırları, cap adlı bir cv2.VideoCapture nesnesi üzerinde görüntüleme ayarlarını değiştirmek için kullanılır.
Set fonksiyonu, belirli bir özellik (property) için yeni bir değer atamak için kullanılır.

cap.set(3, 1280): Video genişliğini 1280 piksel olarak ayarlar.
cap.set(4, 720): Video yüksekliğini 720 piksel olarak ayarlar.
Bu ayarlamalar, video akışının çözünürlüğünü belirler.
Bu örnekte, 1280x720 piksel çözünürlük ayarlanmış olur.

OpenCV kütüphanesinde, video çerçevesinin genişliği ve yüksekliği için kullanılan özellik tanımlayıcıları 3 ve 4'tür.
CV_CAP_PROP_FRAME_WIDTH (3): Video çerçevesinin genişliği.
CV_CAP_PROP_FRAME_HEIGHT (4): Video çerçevesinin yüksekliği.
CV_CAP_PROP_FPS (5): Video akışındaki kare hızı (fps).
CV_CAP_PROP_BRIGHTNESS (10): Parlaklık seviyesi.
CV_CAP_PROP_CONTRAST (11): Kontrast seviyesi.
CV_CAP_PROP_SATURATION (12): Doyma (saturation) seviyesi.
CV_CAP_PROP_EXPOSURE (15): Pozlama seviyesi.

Genişlik ve yükseklik için özellik tanımlayıcıları standart olarak 3 ve 4'tür. 


while True:
    success, img = cap.read()
    cv2.imshow("Image",img)
    cv2.waitKey(1)
	
Bu kod parçası, bir video akışını anlık olarak ekranda gösteren basit bir video oynatıcıdır.
cv2.imshow ve cv2.waitKey işlevleri, video akışındaki her karenin ekranda görüntülenmesini ve kullanıcının bir tuşa basmasını beklemesini sağlar.
Cap.read() fonksiyonu ile her bir kare okunur ve bu kare, cv2.imshow ile ekranda gösterilir.
cap.read(): Video akışından bir kareyi okur.
success adlı bir boolean değeri ve okunan kareyi içeren img adlı bir görüntü dizisi (NumPy dizisi) döndürür.


my_list = [1, 2, 3, 4, 5]

for item in my_list:
    print(item)

Bu örnekte, for item in my_list ifadesi, my_list içindeki her bir elemanı item değişkenine atar ve ardından ,
döngü gövdesinde bu elemanları kullanabiliriz.

Döngü şu şekilde çalışır:

İlk iterasyonda, item değeri 1 olur ve print(item) ifadesi 1'i ekrana yazdırır.
İkinci iterasyonda, item değeri 2 olur ve bu kez 2 yazdırılır.
Bu şekilde liste sonuna kadar devam eder.

for r in results
for r in results ifadesi de results nesnesi içindeki her bir elemanı r değişkenine atayarak döngüyü gerçekleştirir.
Ve döngü gövdesinde bu elemanları kullanmanızı sağlar.

boxes = r.boxes
r.boxes ifadesi, nesne tespiti modeli tarafından üretilen sonuçlardaki tespit edilen nesnelerin kutularını temsil eden bir özelliği ifade eder.
Her bir kutu, tespit edilen bir nesnenin koordinatlarını (genellikle sol üst ve sağ alt köşe koordinatları) içerir.



for r in results:
    boxes = r.boxes
    for box in boxes:
        x1, y1, x2, y2 = box.xyxy
        print(x1, y1, x2, y2)
		
Burada, r.boxes ifadesi, bir tespit sonucundaki tüm kutuların bir listesini içerir.
İç içe iki döngü kullanılarak her bir kutunun koordinatlarına erişilir ve bu koordinatlar ekrana yazdırılır.
box.xyxy ifadesi, her bir kutunun sol üst ve sağ alt köşe koordinatlarını içeren bir özelliği temsil eder.
Bu koordinatlar daha sonra x1, y1, x2, y2 değişkenlerine atanarak ekrana yazdırılır.
Bu şekilde, tespit edilen nesnelerin konumları ekrana basılmış olur.

cv2.rectangle(img, (x1, y1), (x2, y2), (255, 0, 255), 3)
Bu kod satırı, OpenCV (cv2) kütüphanesini kullanarak bir görüntü üzerinde dikdörtgen çizmeyi ifade eder. 

cv2.rectangle: Bu fonksiyon, bir görüntü üzerine bir dikdörtgen çizmek için kullanılır.

img: Çizimin yapılacağı görüntüyü temsil eder.

(x1, y1): Dikdörtgenin sol üst köşesinin koordinatları. x1 ve y1 değişkenleri, tespit edilen nesnenin sol üst köşesinin x ve y koordinatlarını temsil eder.

(x2, y2): Dikdörtgenin sağ alt köşesinin koordinatları. x2 ve y2 değişkenleri, tespit edilen nesnenin sağ alt köşesinin x ve y koordinatlarını temsil eder.

(255, 0, 255): Dikdörtgenin çizgi rengini belirtir. Burada (B, G, R) formatında bir renk kullanılır. (255, 0, 255) mor renge karşılık gelir.

3: Çizilen dikdörtgenin kenar kalınlığını belirtir.

Bu kod satırı, tespit edilen nesnelerin koordinatlarına dayalı olarak bir görüntü üzerine mor renkte ve 3 piksel kalınlığında dikdörtgenler çizer.
Bu tür görselleştirmeler, nesne tespiti modelinin çalışmasını anlamak veya sonuçları görsel olarak kontrol etmek için sıkça kullanılır.

cvzone.cornerRect(img, (x1, y1, w, h))
cvzone.cornerRect(img, (x1, y1, w, h)): Bu satır, cvzone kütüphanesinin cornerRect fonksiyonunu kullanarak bir dikdörtgenin köşelerini vurgulamak için bir işlem gerçekleştirir.
cv2.rectangle ifadesi yerine daha süslü dikdörtgenler için kullandık.


conf = math.ceil((box.conf[0]*100))/100
box.conf[0]: Bu ifade, muhtemelen bir tespit sonucunu temsil eden box nesnesinin güven (confidence) değerine erişir.
Nesne tespiti modelleri genellikle her bir tespit sonucu için bir güven değeri sağlar, bu da o tespitin doğruluk derecesini gösterir.

box.conf[0]*100: Güven değerini 100 ile çarpar ve yüzdesini ifade eden bir değere dönüştürür.
Bu, genellikle 0 ile 1 arasında olan bir güven değerini, yüzde olarak ifade etmek için kullanılır.

math.ceil(...): ceil fonksiyonu (tavan fonksiyonu), ondalık sayıları bir üst tam sayıya yuvarlar.
Bu durumda, güven değerini yuvarlayarak daha anlamlı bir sayıya çevirmek için kullanılmıştır.

(box.conf[0]*100))/100: Son olarak, bu ifade, yuvarlanmış güven değerini 100'e böler,
Bu da bir ondalık sayıyı yuvarlamış yüzde değerine çevirir.

cvzone.putTextRect(img, f'{conf}', (max(0, x1), max(35, y1)))
cvzone.putTextRect: Bu fonksiyon, bir görüntü üzerine metin eklemek için kullanılır.
f'{conf}': Bu ifade, conf değişkeninin değerini metin olarak formatlar.
Eğer conf bir sayı (float veya int) ise, bu sayı metin haline getirilir.
Eğer conf bir string ise, doğrudan kullanılır.

(max(0, x1), max(35, y1)): Bu ifade, metnin konumunu belirtir. max(0, x1) ifadesi, x koordinatını 0'dan küçükse 0 olarak alır,
yani metni sol kenara taşır. max(35, y1) ifadesi ise y koordinatını 35'ten küçükse 35 olarak alır,
yani metni yukarı taşır. Bu, metnin görüntü kenarlarından taşmasını önler.

cls = box.cls[0]: Bu satır, muhtemelen bir tespit sonucunu temsil eden box nesnesinden sınıf etiketini (cls) alır.
Sınıf etiketi, tespit edilen nesnenin ait olduğu sınıfı gösterir.

scale=1: Bu, metnin boyutunu belirler. Varsayılan değeri 1'dir ve metni orijinal boyutunda tutar.
thickness=1: Bu, metin çizgilerinin kalınlığını belirler. Varsayılan değeri 1'dir. 
