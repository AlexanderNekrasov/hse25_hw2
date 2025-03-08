# hse25_hw2

Клеточная линия: Karpas-422, метка: H3K9me3

Эксперимент: ENCSR978BQI

id_1: ENCFF584ZQM, id_2: ENCFF002AVO, control: ENCFF002AXD

# FastQC

ENCFF584ZQM:
![CleanShot 2025-03-07 at 18 11 45@2x](https://github.com/user-attachments/assets/cef0cb1e-9d18-40f4-914b-e2640f43821a)

ENCFF002AVO:
![CleanShot 2025-03-07 at 18 12 08@2x](https://github.com/user-attachments/assets/160d9386-3b17-4661-bf95-a141c43c5940)

ENCFF002AXD:
![CleanShot 2025-03-07 at 18 12 24@2x](https://github.com/user-attachments/assets/f58870ca-71db-4073-80aa-d8a05f38f52d)

Видно, что качество чтений во второй реплике, а также в контроле, не очень хорошее. Подрезаем все чтения, опять запускаем FastQC.

ENCFF584ZQM:
![CleanShot 2025-03-07 at 18 13 25@2x](https://github.com/user-attachments/assets/69546148-30a0-4761-a0b7-dae3bdfe64c6)

ENCFF002AVO:
![CleanShot 2025-03-07 at 18 14 06@2x](https://github.com/user-attachments/assets/344620d6-a71c-4197-b05b-94d77e73371f)

ENCFF002AXD:
![CleanShot 2025-03-07 at 18 14 35@2x](https://github.com/user-attachments/assets/51d9f59c-3182-4229-b17a-28b6c86e5da4)

# bowtie

Вывод:
```
$ bowtie2  -p 2 \
           -x chromosome_index \
           -U ENCFF584ZQM_trimmed.fastq \
           -S bowtie2_res/res_ZQM.sam
25922328 reads; of these:
  25922328 (100.00%) were unpaired; of these:
    20649911 (79.66%) aligned 0 times
    1447501 (5.58%) aligned exactly 1 time
    3824916 (14.76%) aligned >1 times
20.34% overall alignment rate
CPU times: user 8.86 s, sys: 1.33 s, total: 10.2 s
Wall time: 32min 22s

$ bowtie2  -p 2 \
           -x chromosome_index \
           -U ENCFF002AVO_trimmed.fastq \
           -S bowtie2_res/res_AVO.sam
16614814 reads; of these:
  16614814 (100.00%) were unpaired; of these:
    13223758 (79.59%) aligned 0 times
    934177 (5.62%) aligned exactly 1 time
    2456879 (14.79%) aligned >1 times
20.41% overall alignment rate
CPU times: user 6.04 s, sys: 796 ms, total: 6.84 s
Wall time: 20min 49s

$ bowtie2  -p 2 \
           -x chromosome_index \
           -U ENCFF002AXD_trimmed.fastq \
           -S bowtie2_res/res_AXD.sam
40851379 reads; of these:
  40851379 (100.00%) were unpaired; of these:
    33374914 (81.70%) aligned 0 times
    2315422 (5.67%) aligned exactly 1 time
    5161043 (12.63%) aligned >1 times
18.30% overall alignment rate
CPU times: user 13 s, sys: 1.93 s, total: 14.9 s
Wall time: 47min 50s
```

Процент выравниваний довольно низкий. Это произошло, потому что выравнивание производилось только на одну хромосому.

# Сравнение результатов

Результаты запуска `intervene` лежат в папке `venn_results/`. 

Видно, что в ENCODE в разы больше пиков, а в пересечении получается немного. Это можно объяснить тем, что выравнивание мы производили только на одну хромосому, в то время как в ENCODE выравнивание производилось на весь геном.

# Бонус 

![result](https://github.com/user-attachments/assets/6a79c46e-790a-4414-9727-a2dbac1addb6)

Распределение гистоновой метки согласуется с теоретическим, пик находится ближе к концу, в начале наблюдается просадка.

# Бонус 2
![image](https://github.com/user-attachments/assets/e08451e1-360e-46ba-b7fe-b6953fc3239e)
