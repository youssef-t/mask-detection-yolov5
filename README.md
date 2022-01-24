# mask-detection-yolov5

## Guide d'utilisation

1-	git clone https://github.com/youssef-t/mask-detection-yolov5.git

2- cd yolov5-master

3- pip install -r requirements.txt

### Entrainenement

On définit custom_data.yaml qui contient la configuration du réseau.

Poids initialisés arbitrairement:
python train.py --img 416 --batch 16 --epochs 65 --data custom_data.yaml --weights '' --cfg yolov5n.yaml --name yolov5n_results  --cache

Poids initialisés selon les recommandations de Yolov5
python train.py --img 416 --batch 16 --epochs 65 --data custom_data.yaml –weights yolov5n.yaml --name yolov5n_results  --cache

### Mise en place
Source 0 pour camera, --conf-thresh: seuil de confiance :
python detect.py --img 416 --source 0 --weights ./weights_after_training/yolov5_n/best.pt --conf-thres 0.5 --line-thickness 2

python detect.py --img 416 --source CHEMIN_VERS_REPERTOIRE_IMAGES --weights ./weights_after_training/yolov5_n/best.pt --save-txt --line-thickness 1

### Validation avec mAP
On met les données de validation dans ./mAP/input/images-optional/images, Et leurs labels dans ground-truth. 
Avec Roboflow, on transforme xml en format Yolo. Ensuite on met les résultats dans le dossier ./mAP/input/images-optional/labels.

On définit dans custom_data_validation_coco_map.yaml  les données de validations
python val.py --img 416 --weights ./weights_after_training/yolov5_n/best.pt --data custom_data_validation_coco_map.yaml --save-txt
