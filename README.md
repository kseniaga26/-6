# -6
Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.

## Цель работы
Интеграция экономической системы в проект Unity и обучение ML-Agent. 

## Задание 1
### Интегрировать экономическую систему в проект Unity и обучить ML-Agent.

- Откроем проект юнити:
![image_1](https://user-images.githubusercontent.com/103308669/204274064-7e609ffa-1742-44d3-a5f2-ad2fe304e5ac.png)

- Перед тем как перейти к началу обучения, запустим Anaconda Prompt и создадим виртуальное пространство с помощью следующих команд:
```
conda create -n MLAgents python=3.6
conda activate MLAgents
```

- Устанавливаем нужные библиотеки:
```
pip install mlagents==0.28.0
pip install torch~=1.7.1 -f https://download.pytorch.org/whl/torch_stable.html
```

- Далее запускаем обучение модели:
![image_2](https://user-images.githubusercontent.com/103308669/204274918-837ff851-3805-414b-944d-0545a223cb25.png)
![image_3](https://user-images.githubusercontent.com/103308669/204274944-506fe9d9-d66a-40f8-bf8e-e0a58f3cb221.png)

https://user-images.githubusercontent.com/103308669/204280054-9e196b38-e355-417d-824e-91466409b0bf.mp4

Шарик начинает двигаться от одного кубика к другому.

- Чтобы ускорить процесс обучения – увеличим количество префабов TargetAreaEconomic до 12 и снова запустим обучение:

https://user-images.githubusercontent.com/103308669/204280105-1be841d5-4461-4df4-b3bc-f085a7d0ac47.mp4

- Далее построим графики для оценки результатов обучения. Для этого установим библиотеку TensorBoard с помощью следующей команды:
```
pip install tensorflow
```

![image_4](https://user-images.githubusercontent.com/103308669/204275932-3d54dae5-3892-4202-b163-dd6c58e2b79e.png)
![image_5](https://user-images.githubusercontent.com/103308669/204275968-54fafe7f-761f-4b71-b250-5a31d7b259ba.png)

- После завершения установки запустим TensorBoard и рассмотрим полученные графики стандартного агента:
![image_6](https://user-images.githubusercontent.com/103308669/204276023-8af189e6-118f-4435-988a-fd7727484f35.png)
![image_7](https://user-images.githubusercontent.com/103308669/204276045-8c6aa36e-d6b3-44c4-b1ac-42412c32ed61.png)


## Задание 2
### Изменить параметры файла yaml-агента, определить какие параметры и как влияют на обучение модели. Описать результаты, выведенные в TensorBoard.

- Попробуем изменить параметр num_layers с 2 на 3:

![image_8](https://user-images.githubusercontent.com/103308669/204276765-e8fc8c50-9182-4aab-924e-116875f858ac.png)
![image_9](https://user-images.githubusercontent.com/103308669/204276789-a8fc364a-4a31-4298-b743-c8a185f49ad4.png)

Получим такие графики: 

![image_10](https://user-images.githubusercontent.com/103308669/204276865-43d751a2-b9b0-4a73-b412-48fa62e2fc76.png)

- Изменим параметр batch_size с 1024 на 2048:

![image_11](https://user-images.githubusercontent.com/103308669/204276962-a6d9ce9b-0a32-4a9b-b3d4-91cd524ba581.png)
![image_12](https://user-images.githubusercontent.com/103308669/204276994-d04f85d7-2909-4d02-8af9-f11322f2c13b.png)

Получим графики:
![image_13](https://user-images.githubusercontent.com/103308669/204277035-27aeb253-b186-43f0-99c2-08dc8d82db01.png)

- Изменим параметр epsilon с 0.2 на 0.3:

![image_14](https://user-images.githubusercontent.com/103308669/204277158-25ef01eb-27d3-41d0-8517-f89b1dc7b8a3.png)
![image_15](https://user-images.githubusercontent.com/103308669/204277186-0009d7b1-f422-4195-9da7-67fb2bfe9879.png)

Получим графики:
![image_16](https://user-images.githubusercontent.com/103308669/204277237-ead67d96-1296-493b-8489-86133fd8a419.png)

- Изменим параметр lambd с 0.95 на 0.8:

![image_17](https://user-images.githubusercontent.com/103308669/204277329-9b15186c-5900-414d-8741-5d749c455a6c.png)
![image_18](https://user-images.githubusercontent.com/103308669/204277343-a9e06a55-0049-4edd-a18a-44d1bcb3dbad.png)

Получим графики: 
![image_19](https://user-images.githubusercontent.com/103308669/204299228-cb51112e-8b51-4e8a-8751-c84a8fb02ad0.png)

- Изменим параметр buffer_size с 10240 до 100:

![image_21](https://user-images.githubusercontent.com/103308669/204294530-4155ad79-bc24-4452-be24-3dd2d9f1a8f6.png)
![image_22](https://user-images.githubusercontent.com/103308669/204294561-6ce52a1f-fddf-460a-8909-0145d572ba63.png)

Получим графики: 
![buffer_size](https://user-images.githubusercontent.com/103308669/204294656-ab36e157-56cf-4ec0-b964-f0347c3b83b9.png)

Рассмотрев все графики можно сделать следующий вывод:
при изменении всех перечисленных значений график Entropy либо растет быстрее чем при оригинальных значениях, либо не изменяется. При изменении всех значений, кроме epsilon, график Extrinsic Value Estimate тоже значительно растет вверх. Также можно заметить, что при изменении параметра batch_size уменьшается график вознаграждений. Остальные графики либо не меняются, либо меняются незначительно. В целом можно сказать, что изменение данных параметров положительно сказывается на обучении модели.

## Выводы

В ходе выполнения данной лабораторной работы, я научилась интегрировать экономическую систему в проект Unity в связке с MLAgent. Поняла как можно обучить ML-Агента справляться с инфляцией. Также понаблюдала за изменениями значений агентов при разных конфигурациях yaml файла.

![image](https://user-images.githubusercontent.com/114469025/208314560-b447ad97-5750-4416-af3f-61eefb0c464e.png)

