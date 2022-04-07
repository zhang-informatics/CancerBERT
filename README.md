# CANCERBERT-NER

So in this updated version,there are some new ideas and tricks （On data Preprocessing and layer design） that can help you quickly implement the fine-tuning model (you just need to try to modify crf_layer or softmax_layer).

### Folder Description:
```
BERT-NER
|____ bert                          # need git from [here](https://github.com/google-research/bert)
|____ CancerBERT_model	    # wait for university approval, can use other models instead (e.g. BLUEBERT)
|____ data		            # train data (Annotated in BIO format, data cannot be shared due to privacy issue)
|____ middle_data	        # middle data (label id map)
|____ output			    # output (final model, predict results)
|____ BERT_NER.py		    # mian code
|____ conlleval.pl		    # eval code
|____ run_ner.sh    		    # run model and eval result

```


### Usage:
```
bash run_ner.sh
```

### What's in run_ner.sh:
```
python BERT_NER.py\
    --task_name="NER"  \
    --do_lower_case=False \
    --crf=False \
    --do_train=True   \
    --do_eval=True   \
    --do_predict=True \
    --data_dir=data   \
    --vocab_file=cased_L-12_H-768_A-12/vocab.txt  \
    --bert_config_file=cased_L-12_H-768_A-12/bert_config.json \
    --init_checkpoint=cased_L-12_H-768_A-12/bert_model.ckpt   \
    --max_seq_length=128   \
    --train_batch_size=32   \
    --learning_rate=2e-5   \
    --num_train_epochs=3.0   \
    --output_dir=./output/result_dir

perl conlleval.pl -d '\t' < ./output/result_dir/label_test.txt
```

**Notice:** 
We used uncased model with max_seq_length=128 due to limited computing resource

### RESULTS:(On test set)
#### Parameter setting:
* do_lower_case=True 
* num_train_epochs=5.0
* crf=True
```

### Result description:

Evaluation results can be found in Table 3 of the paper:
https://academic.oup.com/jamia/advance-article/doi/10.1093/jamia/ocac040/6554005





