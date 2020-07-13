Download model weights from here : https://drive.google.com/drive/folders/1I-HI6ylwdn2arckhzIPap1u2i0q4rrkz?usp=sharing


MaskRCNN: 

MaskRCNN uses a COCO styled mitosis dataset. We have used Detectron2 MaskRCNN.After importing your dataset, register it using function in code "register_coco_instances". Use the weights from the link above or train it using COCO weights from here: https://github.com/facebookresearch/Detectron/blob/master/MODEL_ZOO.md

Cascade RCNN:
Cascade uses a VOC styled dataset. We have used mmdetection models. The models use are pre-trained on ImageNet dataset.

Evaluation:
The F-score was used as an evaluation measure for these models. Basically first all the predictions are checked if predictions are within 40 pixels of eachother, only one is kept while others are deleted. Then predictions are checked with the original annotations, if they are within 30 pixel it is considered a True Positive, if it misses any they are False Negative and if any prediction is not within 30 pixel of any actual tumor, then we consider it as a False Positive.
