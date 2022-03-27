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

| Состояния | Названия | Метки | Изображение | Свойство |
| ----------- | ----------------- | ----------------- | ----------------- | ----------------- |
| 1 | Heterochromatin | H3k27me3 | ![1_state](https://user-images.githubusercontent.com/79662580/160300689-56252cbc-3a10-41f8-ab7f-40b44856a555.png)
 | Лежит вне генов, вне экзонов |
| 2 | Repressed | - | ![2_state](https://user-images.githubusercontent.com/79662580/160300699-50bb1d6b-020f-4078-a01a-446a126acb58.png)
 | Лежит вне генов, вне экзонов |
| 3 | Heterochromatin | H3k09me3 | ![3_state](https://user-images.githubusercontent.com/79662580/160300701-4bc2bee9-2802-4804-9155-ce635a7d5957.png)
 | Лежит вне генов, вне экзонов |
| 4 | Trabscribed | H3k36me3 | ![4_state](https://user-images.githubusercontent.com/79662580/160300704-34bff007-e820-48d3-98c1-dd0ccc79561a.png)
 | Лежит в генах и в экзонах |
| 5 | Trabscribed | H3k36me3, H4k20me1, H3k79me2 | ![5_state](https://user-images.githubusercontent.com/79662580/160300709-d8aff5af-24f6-4b93-b430-e2c3169ffdaf.png)
 | Лежит в генах и в экзонах |
| 6 | Trabscribed | H3k36me3, H4k20me1, H3k79me2, H3k04me1, H3k04me2 | ![6_state](https://user-images.githubusercontent.com/79662580/160300712-a7d4b578-c467-4508-87cf-61d3ae4e741f.png)
 | Лежит в генах и в экзонах |
| 7 | Weak enhancer | H3k04me1, H2az | ![7_state](https://user-images.githubusercontent.com/79662580/160300721-3c9b9a10-f705-4e1e-815a-b394525c152c.png)
 | Лежит вне генов, в экзонах |
| 8 | Weak Promoter | H3k04me1, H3k04me2, H3k09ac, H3k27ac, H3k04me3, H2az | ![8_state](https://user-images.githubusercontent.com/79662580/160300757-4e2212b6-83ff-4f92-bf77-23eefd9ba4a1.png)
 | Зависит от CpG островков, лежит вне генов |
| 9 | Active Promoter | H3k79me2, H3k04me1, H3k04me2, H3k09ac, H3k27ac, H3k04me3, H2az | ![9_state](https://user-images.githubusercontent.com/79662580/160300732-fd73ddd9-df38-417f-adff-a5449b409ff5.png)
 | Зависит от CpG островков, лежит вне генов |
| 10 | Trabscribed | H3k36me3, H4k20me1, H3k79me2, H3k04me1, H3k04me2, H3k09ac, H3k27ac, H3k04me3 | ![10_state](https://user-images.githubusercontent.com/79662580/160300734-6b84f24a-00ce-4f35-b84d-bacab3431a76.png)
 | Лежит в генах и в экзонах |

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

full_status_names = ['1_Heterochromatin', '2_Repressed', '3_Heterochromatin', '4_Trabscribed', 
                     '5_Trabscribed', '6_Trabscribed', 
                     '7_Weak_enhancer', '8_Weak_Promoter',
                     '9_Active_Promoter', '10_Trabscribed']

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
