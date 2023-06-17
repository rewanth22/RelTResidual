# Generating scene graphs using Transformers with Knowledge infusion and Residual Connections

Scene Graph Generation is an active research topic which involves representing a visual scene in term of nodes and edges. Given an image, the objective is to determine the actors or objects present in an image and identify the relationship between the actors. The nodes in a scene graph are the proposed objects and the edges correspond to the relationship between the nodes. For instance, given an image containing a car and a person, the model needs to identify if there is an action connecting the car and the person if it exists. In this project, we extend the work done from the [Relation Transformer](https://github.com/yrcong/RelTR) research work. We introduce residual connections between modules and infuse prior knowledge about the objects into the system. We hypothesize that in doing so, the model will be able to identify the objects and their relationships faster and accurately. We compare the performance of the customized architecture against the baseline RelTR model on the visual genome dataset with 5,000 and 7,500 training samples. We provide detailed inference about the pros and cons of the proposed model.

### Dependency Installation
1. Clone the repo
   ```sh
   git clone https://github.com/rewanth22/RelTResidual.git
   ```
   For accounts that are SSH configured
   ```sh
    git clone git@github.com:rewanth22/RelTResidual.git
   ```
2. Install pip
   ```sh
   python -m pip install --upgrade pip
   ```
3. Create and Activate Virtual Environment (Linux)
   ```sh
   python3 -m venv [environment-name]
   source [environment-name]/bin/activate
   ```
4. Install dependencies
   ```sh
   pip install -r requirements.txt
   ```

## Training/Evaluation on Visual Genome 
```
a) Follow [README](https://github.com/yrcong/RelTR/blob/main/data/README.md) in the data directory to prepare the datasets.

# compile the code computing box intersection
cd lib/fpn
sh make.sh
```
## Inference

a) Download our [RelTR model](https://drive.google.com/file/d/1id6oD_iwiNDD6HyCn2ORgRTIKkPD3tUD/view) pretrained on the Visual Genome dataset and put it under 
```
ckpt/checkpoint0149.pth
```
b) Infer the relationships in an image with the command:
```
python inference.py --img_path $IMAGE_PATH --resume $MODEL_PATH
```
## Training
```
python main.py --dataset vg --img_folder data/vg/images/ --ann_path data/vg/ --batch_size 2 --output_dir ckpt
```

## Evaluation
```
python main.py --dataset vg --img_folder data/vg/images/ --ann_path data/vg/ --eval --batch_size 1 --resume ckpt/checkpoint0149.pth
```

#### NOTE: 
For working with the baseline, you need to swap 3 files. main.py with main_src.py, transformer.py with transformer_src.py and reltr.py with reltr_src.py. For working with the custom model vice-versa. This is done in order to prevent import error issues across different python scripts.

## Authors 

[Krish Rewanth Sevuga Perumal](https://github.com/rewanth22), [Prasannakumaran Dhanasekaran](http://github.com/PrasannaKumaran)