# 🚦 STOP Trafik İşareti Tespiti (YOLOv5 ile)

Bu proje, derin öğrenme tabanlı **YOLOv5 modeli** ile `STOP` trafik işareti tespitini gerçekleştirir. Eğitim, önceden hazırlanmış bir veri seti üzerinde yapılmıştır ve sonuçlar görsel olarak kaydedilmiştir.

## 🔧 Kullanılan Teknolojiler

* Python 3.13
* PyTorch 2.7.1 + CPU
* OpenCV
* Ultralytics YOLOv5

## 📂 Klasör Yapısı

```bash
.
├── output_images/       # Modelin tespit ettiği sonuç görselleri
├── README.md            # Bu dosya
└── yolov5/              # YOLOv5 model dosyaları
```

## 📦 Veri Seti Bilgisi

Bu projede kullanılan "STOP" trafik işareti veri seti, **Roboflow** platformundan alınmıştır:

* **Veri Seti Adı**: `h2politostop.v1i.yolov5pytorch`
* **Hazırlayan**: `blabla-awbkw` kullanıcısı
* **Kaynak**: [Roboflow Dataset](https://universe.roboflow.com/blabla-awbkw/h2politostop-ngxzy/dataset/1)
* **Lisans**: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

## 📊 Test Parametreleri

Modelin test aşamasında kullanılan önemli parametre:

* **confidence threshold (`--conf`)**: `0.5`

Bu değer, modelin güven eşiğini belirler. Yani, model sadece %50'den yüksek doğruluğa sahip olduğunu düşündüğü nesneleri tespit eder.

## 📊 Eğitim Sonuçları ve Anlamları

| Metrik         | Açıklama                                                                   |
| -------------- | -------------------------------------------------------------------------- |
| **Box Loss**   | Modelin nesnenin konumunu doğru tahmin edip etmediğini ölçer.              |
| **Class Loss** | Modelin sınıf tahmini doğruluğunu ölçer (bu projede tek sınıf var).        |
| **mAP\@0.5**   | Tüm tahminlerin doğruluğunun ortalamasıdır, `IoU=0.5` eşiğinde hesaplanır. |
| **Precision**  | Modelin tahminlerinin ne kadar doğru olduğunu gösterir.                    |
| **Recall**     | Modelin gerçek nesneleri ne kadar tespit edebildiğini gösterir.            |

## 📸 Çıktı Görselleri

`yolo5` klasörü altında test sırasında elde edilen tespit sonuçları yer almaktadır. Model başarılı şekilde STOP işaretlerini işaretlemiştir.
