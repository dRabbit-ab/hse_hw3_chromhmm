# hse_hw3_chromhmm

## Colab

## Files and names

|       Клеточная линия      | Гистоновая метка | Файл для скачивания | Имя в колабе |
| ----------- | ----------------- | ----------------- | ----------------- |
| A549 | H2AFZ | wgEncodeBroadHistoneA549H2azDex100nmAlnRep1.bam | H2az.bam |
| A549 | H3K27ac | wgEncodeBroadHistoneA549H3k27acDex100nmAlnRep1.bam | H3k27ac.bam |
| A549 | H3K27me3 | wgEncodeBroadHistoneA549H3k27me3Dex100nmAlnRep1.bam | H3k27me3.bam |
| A549 | H3K36me3 | wgEncodeBroadHistoneA549H3k36me3Dex100nmAlnRep1.bam | H3k36me3.bam |
| A549 | H3K4me1 | wgEncodeBroadHistoneA549H3k04me1Dex100nmAlnRep1.bam | H3k04me1.bam |
| A549 | H3K4me2 | wgEncodeBroadHistoneA549H3k04me2Dex100nmAlnRep1.bam | H3k04me2.bam |
| A549 | H3K4me3 | wgEncodeBroadHistoneA549H3k04me3Dex100nmAlnRep1.bam | H3k04me3.bam |
| A549 | H3K79me2| wgEncodeBroadHistoneA549H3k79me2Dex100nmAlnRep1.bam | H3k79me2.bam |
| A549 | H3K9ac | wgEncodeBroadHistoneA549H3k09acEtoh02AlnRep1.bam | H3k09ac.bam |
| A549 | H3K9me3 | wgEncodeBroadHistoneA549H3k09me3Etoh02AlnRep1.bam | H3k09me3.bam |
| A549 | H4K20me1  | wgEncodeBroadHistoneA549H4k20me1Etoh02AlnRep1.bam | H4k20me1.bam |
| A549 | Control | wgEncodeBroadHistoneA549ControlDex100nmAlnRep1.bam | A549Control.bam |

## Main part

### ChromHMM

|       Overlap      | emissions | transitions |
| ----------- | ----------------- | ----------------- |
| A549 | H2AFZ | wgEncodeBroadHistoneA549H2azDex100nmAlnRep1.bam |

|       RefSeqTES_neighborhood      | RefSeqTSS_neighborhood |
| ----------- | ----------------- |
| A549 | H2AFZ |

### Epigenetic states

## Bonus Part

См. Code examples

## Code examples

Код для создания cellmarkfiletable.txt
```
import os

with open('cellmarkfiletable.txt', 'w') as f:
  for file in os.listdir():
    if file.split('.')[-1] == 'bed' and 'Control' not in file:
      to_write = f'A549\t{file.split(".")[0]}\t{file}\tA549Control.bed\n'
      f.write(to_write)
```

Код для бонусной части
```
import pandas as pd

full_status_names = ['1_Active_Promoter', '2_Weak_Promoter', '3_Inactive/poised_Promoter', '4_Strong_enhancer', '5_Strong_enhancer', '6_Weak/poised_enhancer',\
                '7_Weak/poised_enhancer', '8_Insulator', '9_Transcriptional_transition', '10_Transcriptional_elongation']
data = pd.read_csv('/content/data_LearnModel_10/A549_10_dense.bed', sep='\t', skiprows=1, names=[1, 2, 3, 'status', 4, 5, 6, 7, 8])

status = pd.DataFrame(full_status_names, columns=['full_status'], index=[i for i in range(1, 11)])

data = data.merge(status, left_on='status', right_index=True).sort_index().drop(['status'], axis=1).rename(columns={'full_status': 'status'})
data = data[[1, 2, 3, 'status', 4, 5, 6, 7, 8]]

data.to_csv('new_A549_10_dense.bed', sep='\t', header=False, index=False)
```
## Comand list

  1) **! wget** : скачивание файлов
  2) **! bedtools bamtobed** : перевод bam формат в bed
  3) **! cat** : вывод файла
  4) **! java -mx5000M -jar ChromHMM.jar BinarizeBed** : разбиение генома на условные интервалы
  5) **! java -mx5000M -jar ChromHMM.jar LearnModel** : присвоение каждому геномному интервалу определенный эпигенетический тип
  6) **! zip** : архивирование файлов
