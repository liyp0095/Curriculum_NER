## Re-Examine Distantly Supervised NER: A New Benchmark and a Simple Approach

This paper delves into Named Entity Recognition (NER) under the framework of Distant Supervision (DS-NER), where the main challenge lies in the compromised quality of labels due to inherent errors such as false positives, false negatives, and positive type errors. We critically assess the efficacy of current DS-NER methodologies using a real-world benchmark dataset named QTL, revealing that their performance often does not meet expectations. To tackle the prevalent issue of label noise, we introduce a simple yet effective approach, Curriculum-based Positive-Unlabeled Learning CuPUL, which strategically starts on "easy" and cleaner samples during the training process to enhance model resilience to noisy samples. Our empirical results highlight the capability of CuPUL to significantly reduce the impact of noisy labels and outperform existing methods.

### Performance of DS-NER Methods on QTL 
F1 Score (Precision/Recall) (in %). The best results are in **bold**, second
best results are in <ins>underline</ins>.

![alt text](fig/image.png)

### Environment

Python 3.7.6, pytorch 1.12

### How to run

For example, on CoNLL2003

```python
python train.py --do_train --do_eval --dataset_name CoNLL2003_KB \
        --train_epochs 2 --train_lr 2e-5 --drop_other 0.5  \
        --curriculum_train_sub_epochs 1 --curriculum_train_lr 5e-5  \ 
        --curriculum_train_epochs 5  \ 
        --self_train_epochs 5 --self_train_lr 5e-7 --m 50  --max_seq_length 150 
```

on QTL dataset,


```python
python train.py --do_train --do_eval --dataset_name QTL \ 
        --loss_type MAE --m 20     \
        --train_epochs 1 --train_lr 5e-7 --drop_other 0.5  \
        --curriculum_train_sub_epochs 1 --curriculum_train_lr 2e-7  \ 
        --curriculum_train_epochs 5 --self_train_lr 5e-7 --self_train_epochs 5  \
        --max_seq_length 300
```

Parameters are tuned from validation set, and all hyper-parameters show in Appendix D, Table 5. 

### Citation

```
@misc{2402.14948,
    Author = {Yuepei Li and Kang Zhou and Qiao Qiao and Qing Wang and Qi Li},
    Title = {Re-Examine Distantly Supervised NER: A New Benchmark and a Simple Approach},
    Year = {2024},
    Eprint = {arXiv:2402.14948},
}
```