# Reproduce BERT finetune results for chinese datasets

This repo reproduces BERT finetune resutlts for chinese datasets. Data can be downloaded from Baidu ERNIE repo(*https://github.com/PaddlePaddle/LARK/tree/develop/ERNIE*, https://ernie.bj.bcebos.com/task_data.tgz), which contains MSRA-NER, LCQMC, XNLI, ChnSentiCorp, nlpcc-dbqa.

------

## MSRA-NER

Baidu reproduce result:

| Epoch | F1 in develop | F1 in test |
| ----- | ------------- | ---------- |
| 3     | 94.0%          | 92.6%       |

Our reproduce result:

| Epoch | F1 in develop | F1 in test |
| ----- | ------------- | ---------- |
| 2     | 94.15%         | 92.34%      |
| 10    | 95.75%         | 94.89%      |

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

------

## XNLI

XNLI data was download from google's bert repo.

google's result:

| Epoch | Acc in develop (infer from log) | Acc in test |
| ----- | ------------------------------- | ----------- |
| 2     | 77.4%                           | 77.2%       |

Baidu reproduce result:

| Epoch | Acc in develop | Acc in test |
| ----- | -------------- | ----------- |
| 3     | 78.1%          | 77.2%       |

Our reproduce result:

| Epoch | Acc in develop | Acc in test |
| ----- | -------------- | ----------- |
| 2     | 77.91%         | 77.56%      |

run script:

```bash
python run_classifier.py \
--task_name=XNLI \
--do_train=true \
--do_eval=true \
--data_dir=../../../corpus/xnli/XNLI-MT-1.0 \
--vocab_file=bert_model/chinese_L-12_H-768_A-12/vocab.txt \
--bert_config_file=bert_model/chinese_L-12_H-768_A-12/bert_config.json \
--init_checkpoint=bert_model/chinese_L-12_H-768_A-12/bert_model.ckpt \
--max_seq_length=128 \
--train_batch_size=32 \
--learning_rate=5e-5 \
--num_train_epochs=2.0 \
--output_dir output_model/bert_xnli_output_ep4/
```

------

## LCQMC

Baidu reproduce result:

| Epoch | Acc in develop | Acc in test |
| ----- | -------------- | ----------- |
| 3     | 88.8%          | 87.0%       |

Our reproduce result:

| Epoch | Acc in develop | Acc in test |
| ----- | -------------- | ----------- |
| 3     | 88.7%          | 86.49%      |

run script:

```bash
python run_classifier.py \
--task_name=LCQMC \
--do_train=true \
--do_eval=true \
--data_dir=../../../corpus/baidu_ernie_task_data/lcqmc/ \
--vocab_file=bert_model/chinese_L-12_H-768_A-12/vocab.txt \
--bert_config_file=bert_model/chinese_L-12_H-768_A-12/bert_config.json \
--init_checkpoint=bert_model/chinese_L-12_H-768_A-12/bert_model.ckpt \
--max_seq_length=128 \
--train_batch_size=32 \
--learning_rate=5e-5 \
--num_train_epochs=2.0 \
--output_dir output_model/bert_lcqmc_output_ep3/
```

## ChnSentiCorp

Baidu reproduce result:

| Epoch | Acc in develop | Acc in test |
| ----- | -------------- | ----------- |
| 3     | 94.6%          | 94.3%       |

Our reproduce result:

| Epoch | Acc in develop | Acc in test |
| ----- | -------------- | ----------- |
| 5     | 92.7%          | 94.5%       |
| 10    | 93.58%         | 94.5%       |

run script:

```bash
python run_classifier.py \
--task_name=chnsenticorp \
--do_train=true \
--do_eval=true \
--data_dir=../../../corpus/baidu_ernie_task_data/chnsenticorp/ \
--vocab_file=bert_model/chinese_L-12_H-768_A-12/vocab.txt \
--bert_config_file=bert_model/chinese_L-12_H-768_A-12/bert_config.json \
--init_checkpoint=bert_model/chinese_L-12_H-768_A-12/bert_model.ckpt \
--max_seq_length=128 \
--train_batch_size=32 \
--learning_rate=5e-5 \
--num_train_epochs=5.0 \
--output_dir output_model/bert_chnsenticorp_output_ep5/
```

## nlpcc-dbqa

Baidu reproduce result:

| Epoch | MRR in develop | MRR in test | F1 in develop | F1 in test |
| ----- | -------------- | ----------- | -------------- | ----------- |
| 3     | 94.7%          | 94.6%       | 80.7%          | 80.8%       |

Our reproduce result:

| Epoch | MRR in develop | MRR in test | F1 in develop | F1 in test |
| ----- | -------------- | ----------- | -------------- | ----------- |
| 3     | 93.9%          | 94.0%       | 78.6%          | 81.3%       |

run script:

```bash
python run_classifier.py \
--task_name=nlpccdbqa \
--do_train=true \
--do_eval=true \
--do_predict=true \
--data_dir=../../../corpus/baidu_ernie_task_data/chnsenticorp/ \
--vocab_file=bert_model/chinese_L-12_H-768_A-12/vocab.txt \
--bert_config_file=bert_model/chinese_L-12_H-768_A-12/bert_config.json \
--init_checkpoint=bert_model/chinese_L-12_H-768_A-12/bert_model.ckpt \
--max_seq_length=128 \
--train_batch_size=32 \
--learning_rate=5e-5 \
--num_train_epochs=3.0 \
--output_dir output_model/bert_nlpccdbqa_output_ep2/
```

------
## Reference

<https://github.com/google-research/bert>

<https://github.com/kyzhouhzau/BERT-NER>

<https://github.com/macanv/BERT-BiLSTM-CRF-NER>