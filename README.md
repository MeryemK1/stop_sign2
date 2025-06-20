# stop_sign2
# STOP Trafik Levhası Tespiti - YOLOv5

Bu projede, YOLOv5 modelini kullanarak 'STOP' trafik işaretinin tespiti gerçekleştirilmiştir. Model, Roboflow'dan indirilen özel bir veri seti ile eğitilmiş ve test edilmiştir.

## İçerik

* [Kurulum](#kurulum)
* [Veri Seti Yapısı](#veri-seti-yapısı)
* [Model Eğitimi](#model-eğitimi)
* [Model Testi](#model-testi)
* [Parametre Açıklamaları](#parametre-açıklamaları)
* [Sonuçlar ve Göstergeler](#sonuçlar-ve-göstergeler)

## Kurulum

```bash
# Gerekli kütüphaneleri yükleyin
pip install -r requirements.txt

# YOLOv5 klasörüne gidin
cd yolov5
```

## Veri Seti Yapısı

Veri seti Roboflow'dan indirildi ve şu yapıda düzenlendi:

```
dataset/
├── train/
│   ├── images/
│   └── labels/
├── valid/
│   ├── images/
│   └── labels/
├── test/
│   ├── images/
│   └── labels/
data.yaml
```

`data.yaml` dosyasında tanımlı:

```yaml
train: ../train/images
val: ../valid/images
test: ../test/images
nc: 1
names: ['stop sign']
```

## Model Eğitimi

```bash
python train.py --img 640 --batch 16 --epochs 100 \
--data data.yaml --weights yolov5s.pt --name stop_sign_detector
```

## Model Testi

Test için aşağıdaki komut kullanıldı:

```bash
python detect.py --weights runs/train/stop_sign_detector/weights/best.pt \
--source dataset/test/images --conf 0.5
```

## Parametre Açıklamaları

* `--conf`: Modelin bir nesneyi STOP olarak algılaması için gereken minimum güven eşiği (confidence threshold). 0.5 seçilmiştir.
* `--weights`: Eğitilen modelin kullanılacağı dosya yolu.
* `--source`: Test görüntülerinin bulunduğu klasör.

## Sonuçlar ve Göstergeler

Eğitim sonunda elde edilen çıktılar `runs/train/stop_sign_detector/results.png` dosyasında yer alır. Burada aşağıdaki metrikler gösterilir:

* **box loss**: Sınır kutusu tahmininin doğruluğunu belirten kayıp değeridir. Düşüek olması istenir.
* **class loss**: Doğru sınıf etiketiyle tahmin yapma kabiliyetini belirten kayıptır.
* **mAP50 (mean Average Precision @ IoU 0.5)**: Modelin nesne tespit başarısını ölçer. 1.0'a yaklaştıkça daha iyi performans gösterir.
* **Precision**: STOP etiketi verdiklerinin ne kadarı gerçekten STOP. (TP / (TP + FP))
* **Recall**: Gerçek STOP'ların ne kadarını bulabildiği (TP / (TP + FN))

Grafikler bu metriklerin eğitim boyunca nasıl geliştiğini gösterir. Modelin iyi öğrendiğini söylemek için bu değerlerin iyileşme göstermesi beklenir.

## GitHub

Bu proje public bir GitHub reposuna yüklenmiştir. \[Repo Linki Buraya Eklenecek]

Repo README'sinde kodları çalıştırmak için gerekli tüm adımlar yer almaktadır. Test çıktıları ve eğitim grafiklerine /runs klasöründen erişilebilir.
