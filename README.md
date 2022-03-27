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

|       Overlap      | Emissions | Transitions |
| ----------- | ----------------- | ----------------- |
| ![Image1](https://github.com/dRabbit-ab/hse_hw3_chromhmm/blob/main/images/A549_10_overlap.png) | ![Image2](https://github.com/dRabbit-ab/hse_hw3_chromhmm/blob/main/images/emissions_10.png) | ![Image3](https://github.com/dRabbit-ab/hse_hw3_chromhmm/blob/main/images/transitions_10.png) |

|       RefSeqTES_neighborhood      | RefSeqTSS_neighborhood |
| ----------- | ----------------- |
| ![Image4](https://github.com/dRabbit-ab/hse_hw3_chromhmm/blob/main/images/A549_10_RefSeqTES_neighborhood.png) | ![Image5](https://github.com/dRabbit-ab/hse_hw3_chromhmm/blob/main/images/A549_10_RefSeqTSS_neighborhood.png) |

### Epigenetic states

| Состояния | Названия | Метки | Изображение |
| ----------- | ----------------- | ----------------- | ----------------- |
| 1 |  | H3k27me3 |  |
| 2 |  | - |  |
| 3 |  | H3k09me3 |  |
| 4 |  | H3k36me3 |  |
| 5 | | H3k36me3, H4k20me1, H3k79me2 |  |
| 6 |  | H3k36me3, H4k20me1, H3k79me2, H3k04me1, H3k04me2 |  |
| 7 |  | H3k04me1, H2az |  |
| 8 |  | H3k04me1, H3k04me2, H3k09ac, H3k27ac, H3k04me3, H2az |  |
| 9 |  | H3k79me2, H3k04me1, H3k04me2, H3k09ac, H3k27ac, H3k04me3, H2az |  |
| 10 |  | H3k36me3, H4k20me1, H3k79me2, H3k04me1, H3k04me2, H3k09ac, H3k27ac, H3k04me3 |  |

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

full_status_names = ['1_Insulator', '2_Insulator', '3_Weak_transcribed', '4_Inactive/poised_Promoter', 
                     '5_Transcriptional_transition', '6_Transcriptional_transition', 
                     '7_Active_Promoter', '8_Heterochromatin_low_signal',
                     '9_Weak/poised_enhancer', '10_Inactive/poised_Promoter']

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
