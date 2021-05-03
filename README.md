# BIOBERT-Relation-Extraction

#### Relation Exctraction

#### BIOBERT vs BERT

#### Requirements and Setup

> $git clone https://github.com/seemapatel151997/BIOBERT-Relation-Extraction.git

Install all required python packages

> pip install -r requirements.txt

To use BioBERT(biobert_v1.1_pubmed), download & unzip the [pretrained model](https://drive.google.com/file/d/1R84voFKHfWV9xjzeLzWBbmY1uOMYpnyD/view) to ./additional_models folder.

run bash script to convert from tensorflow into pytorch version of the model.

#### Fine-Tuning

Run main_task.py with arguments below. Requires SemEval2010 Task 8 dataset, available [here.](https://github.com/sahitya0000/Relation-Classification/blob/master/corpus/SemEval2010_task8_all_data.zip) Download & unzip to ./data/ folder.

> $python main_task.py
> --train_data ./data/SemEval2010_task8_all_data/SemEval2010_task8_training/TRAIN_FILE.TXT
> --test_data ./data/SemEval2010_task8_all_data/SemEval2010_task8_testing_keys/TEST_FILE_FULL.TXT
> --use_pretrained_blanks 0
> --num_classes 19
> --batch_size 128
> --gradient_acc_steps 2
> --max_norm 1.0
> --fp16 0
> --num_epochs 50
> --lr 0.00001
> --model_no 2
> --model_size 'bert-base-uncased'
> --train 1
> --infer 0


#### Inference

The script can also automatically detect potential entities in an input sentence, in which case all possible relation combinations are inferred.

Set infer=1 to enable inference mode and train=0 to disable training mode. model_no=2 to use the fine-tuned BioBERT model.

> $python main_task.py
> --train 0
> --infer 1
> --model_no 2
> --input_sent "The COVID-19 pandemic, also known as the coronavirus pandemic, is an ongoing global pandemic of coronavirus disease 2019 (COVID‑19) caused by severe acute respiratory syndrome coronavirus 2 (SARS-CoV-2)."
