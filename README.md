# mask-detection-yolov5
<p align="center">
  <a href="" target="blank"><img src="https://quantmetry.b-cdn.net/wp-content/uploads/2019/11/article-tme-min.png" width="320" alt="AI" /></a>
</p>

***
[![pypi](https://img.shields.io/pypi/v/sysbus.svg)](https://pypi.python.org/pypi/sysbus)
[![pypi](https://img.shields.io/pypi/pyversions/sysbus.svg)](https://pypi.python.org/pypi/sysbus)
[![MIT License](https://img.shields.io/github/license/rene-d/sysbus.svg?logoColor=silver&logo=open-source-initiative&label=&color=blue)](https://github.com/rene-d/sysbus/blob/master/LICENSE)

## Guide d'utilisation Windows et Linux

```bash
$ git clone https://github.com/youssef-t/mask-detection-yolov5.git
```

```bash
$ cd yolov5-master
```

```bash
$ pip install -r requirements.txt
```

### Entrainenement

On définit custom_data.yaml qui contient la configuration du réseau.

Poids initialisés arbitrairement:
```bash
$ python train.py --img 416 --batch 16 --epochs 65 --data custom_data.yaml --weights '' --cfg yolov5n.yaml --name yolov5n_results  --cache
```

Poids initialisés selon les recommandations de Yolov5
```bash
$ python train.py --img 416 --batch 16 --epochs 65 --data custom_data.yaml –weights yolov5n.yaml --name yolov5n_results  --cache
```

### Mise en place
Source 0 pour camera, --conf-thresh: seuil de confiance :
```bash
$ python detect.py --img 416 --source 0 --weights ./weights_after_training/yolov5_n/best.pt --conf-thres 0.5 --line-thickness 2
```

```bash
$ python detect.py --img 416 --source CHEMIN_VERS_REPERTOIRE_IMAGES --weights ./weights_after_training/yolov5_n/best.pt --save-txt --line-thickness 1
```

### Evaluation avec mAP
Avec Roboflow, on transforme xml en format Yolo. Ensuite, on met les résultats (images et annotations) dans le dossier dans ./test_validation_kaggle.

On définit les données de validations dans custom_data_validation_coco_map.yaml :
```bash
$ python val.py --img 416 --weights ./weights_after_training/yolov5_n/best.pt --data custom_data_validation_coco_map.yaml --task test
```
