# Reproduce BERT finetune resutlts for chinese datasets

This repo reproduces BERT finetune resutlts for chinese datasets. Data can be downloaded from Baidu ERNIE repo(*https://github.com/PaddlePaddle/LARK/tree/develop/ERNIE*, https://ernie.bj.bcebos.com/task_data.tgz), which contains MSRA-NER, LCQMC, XNLI, ChnSentiCorp, nlpcc-dbqa.

## MSRA-NER

Baidu reproduce result:

| Epoch | F1 in develop | F1 in test |
| ----- | ------------- | ---------- |
| 2     | 94.0          | 92.6       |

Our reproduce result:

| Epoch | F1 in develop | F1 in test |
| ----- | ------------- | ---------- |
| 2     | 94.15         | 92.34      |
| 10    | 95.75         | 94.89      |

run script:

```bash
python run_ner.py \
-device_map 0 \
-data_dir data/baidu_msra/bio/ \
-output_dir output/google_bert_wikicn_epoch2 \
-init_checkpoint bert_model/chinese_L-12_H-768_A-12/bert_model.ckpt \
-bert_config_file bert_model/chinese_L-12_H-768_A-12/bert_config.json \
-vocab_file bert_model/chinese_L-12_H-768_A-12/vocab.txt \
-batch_size 16 \
-decode=softmax \
-num_train_epochs=2
```

