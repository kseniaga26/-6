# Перцептрон
Лабораторная №4 для АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ

Отчет по лабораторной работе 2 выполнил(а):
- Голубятникова Ксения Александровна
- РИ210936

Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

## Задание 1
### В проекте Unity реализовать прецептрон, который умеет производить вычисления:

![image](https://user-images.githubusercontent.com/114469025/204133039-8220dca8-e5e2-44dd-8e48-157847c20152.png)
- Подключение С#-скрипта к сцене

```py
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
	public double[] input;
	public double output;
}

public class Perceptron : MonoBehaviour {

	public TrainingSet[] ts;
	double[] weights = {0,0};
	double bias = 0;
	double totalError = 0;

	double DotProductBias(double[] v1, double[] v2) 
	{
		if (v1 == null || v2 == null)
			return -1;
	 
		if (v1.Length != v2.Length)
			return -1;
	 
		double d = 0;
		for (int x = 0; x < v1.Length; x++)
		{
			d += v1[x] * v2[x];
		}

		d += bias;
	 
		return d;
	}

	double CalcOutput(int i)
	{
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}

	void InitialiseWeights()
	{
		for(int i = 0; i < weights.Length; i++)
		{
			weights[i] = Random.Range(-1.0f,1.0f);
		}
		bias = Random.Range(-1.0f,1.0f);
	}

	void UpdateWeights(int j)
	{
		double error = ts[j].output - CalcOutput(j);
		totalError += Mathf.Abs((float)error);
		for(int i = 0; i < weights.Length; i++)
		{			
			weights[i] = weights[i] + error*ts[j].input[i]; 
		}
		bias += error;
	}


	double CalcOutput(double i1, double i2)
	{
		double[] inp = new double[] {i1, i2};
		double dp = DotProductBias(weights,inp);
		if(dp > 0) return(1);
		return (0);
	}

	void Train(int epochs)
	{
		InitialiseWeights();
		
		for(int e = 0; e < epochs; e++)
		{
			totalError = 0;
			for(int t = 0; t < ts.Length; t++)
			{
				UpdateWeights(t);
				Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
			}
			Debug.Log("TOTAL ERROR: " + totalError);
		}
	}

	void Start () {
		Train(8);
		
		Debug.Log("Test 0 0: " + CalcOutput(0,0));
		Debug.Log("Test 0 1: " + CalcOutput(0,1));
		Debug.Log("Test 1 0: " + CalcOutput(1,0));
		Debug.Log("Test 1 1: " + CalcOutput(1,1));		
	}
	
	void Update () {
		
	}
}
```

- OR 

Корректность работы: перцептрон обучился на 3 эпохе. Работает корректно.

![image](https://user-images.githubusercontent.com/114469025/204133054-81874c49-8423-41b4-83b2-6db41cde250d.png)

![image](https://user-images.githubusercontent.com/114469025/204133063-7d2bca43-7c9e-4527-bea4-7a9370d26531.png)

- AND

Корректность работы: перцептрон обучился на 6 эпохе. Работает корректно.

![image](https://user-images.githubusercontent.com/114469025/204133079-14df3bf6-fe60-4dea-8d4f-01fb81d705d8.png)

- NAND

Корректность работы: перцептрон обучился на 3 эпохе. Работает корректно.

![image](https://user-images.githubusercontent.com/114469025/204133114-3d87e980-9f0b-402d-a6aa-0435d465a3be.png)

- XOR

Корректность работы: перцептрон не обучается при любом количестве эпох и значение totalError так же равно 4. Так как из информации, данной в лекции и найденной в интернете, ясно что однослойного перцептрона для решения задачи XOR не достаточно.

![image](https://user-images.githubusercontent.com/114469025/204133104-28f4476e-193d-44e3-a885-35173c21538e.png)

## Задание 2
### Построить графики зависимости количества эпох от ошибки обучения.

![image](https://user-images.githubusercontent.com/114469025/204133373-98e248ad-79c4-4771-97d7-5e10df9d2788.png)
![image](https://user-images.githubusercontent.com/114469025/205047094-1ea5f27a-d249-4db3-9504-d2ae7a7c4b53.png)
![image](https://user-images.githubusercontent.com/114469025/205047746-71f00049-11af-47f4-87cb-35730ac03342.png)
![image](https://user-images.githubusercontent.com/114469025/205054008-878963ce-a3eb-4aef-aa0c-6500d5a0a640.png)

Количество эпох обучения зависит от ошибки, которую выдает программа на тестовом наборе данных. Т.е. даже если на какой-то эпохе перцептрон удачно выполнил задачу, лучше взять чуть больше эпох обучения для избежания появления редких ошибок.


