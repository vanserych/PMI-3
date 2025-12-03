<h1 align="center">📊 Лабораторные по базам данных вариант 5</h1>

<div align="center">
  
</div>

---

<h1 name="content" align="center">
  <a href="">
    <img src="https://github.com/user-attachments/assets/e080adec-6af7-4bd2-b232-d43cb37024ac" width="20" height="20"/>
  </a> 
  MSSQL
</h1>

<p align="center">
  <a href="#-lab1"><img alt="lab1" src="https://img.shields.io/badge/Lab1-blue"></a> 
  <a href="#-lab2"><img alt="lab2" src="https://img.shields.io/badge/Lab2-red"></a>
  <a href="#-lab3"><img alt="lab3" src="https://img.shields.io/badge/Lab3-green"></a>
  <a href="#-lab4"><img alt="lab4" src="https://img.shields.io/badge/Lab4-yellow"></a>
  <a href="#-lab5"><img alt="lab5" src="https://img.shields.io/badge/Lab5-gray"></a>
  <a href="#-lab6"><img alt="lab6" src="https://img.shields.io/badge/Lab6-orange"></a> 
  <a href="#-lab7"><img alt="lab7" src="https://img.shields.io/badge/Lab7-brown"></a>
  <a href="#-lab8"><img alt="lab8" src="https://img.shields.io/badge/Lab8-purple"></a>
  <a href="#-lab9"><img alt="lab9" src="https://img.shields.io/badge/Lab9-violet"></a> 
</p>

# <a id="-lab1"></a><img src="https://github.com/user-attachments/assets/e080adec-6af7-4bd2-b232-d43cb37024ac" width="20" height="20"/> Lab1
[Назад](#content)

<h3 align="center">

### ER-model:
![ER-model](https://github.com/vanserych/PMI-3/blob/8c9cddbf3a410c4cd2a14ec63bcf126128d51a4f/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%94%D0%B8%D0%B5%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B0%D1%8F%20%D1%81%D1%82%D0%BE%D0%BB%D0%BE%D0%B2%D0%B0%D1%8F%20ER-%D0%BC%D0%BE%D0%B4%D0%B5%D0%BB%D1%8C%20%D0%A5%D1%80%D1%83%D0%BB%D0%B5%D0%B2%20%D0%98..png)

### Relational model:
![REL-model](https://github.com/vanserych/PMI-3/blob/40f773fee537ba51e3ddf5f254f3b9c066ad4c69/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A0%D0%9C%20%D0%A5%D1%80%D1%83%D0%BB%D1%91%D0%B2.png))

# <a id="-lab2"></a><img src="https://github.com/user-attachments/assets/e080adec-6af7-4bd2-b232-d43cb37024ac" width="20" height="20"/> Lab2
[Назад](#content)

<h3 align="center">
  Лабораторная работа №2
</h3>

### Создание SQL таблицы:

```sql
CREATE TABLE Работник (
    ID INT PRIMARY KEY IDENTITY,
    Имя NVARCHAR(50) NOT NULL,
    Фамилия NVARCHAR(50) NOT NULL,
    Номер_телефона NVARCHAR(50),
    Номер_паспорта NVARCHAR(50),
    Стаж TINYINT,
    Зарплата MONEY,
);

CREATE TABLE Кладовщик (
    ID INT PRIMARY KEY IDENTITY,
    Работник_ID INT NOT NULL FOREIGN KEY REFERENCES Работник(ID),
);

CREATE TABLE Поставщик (
    ID INT PRIMARY KEY IDENTITY,
    Компания NVARCHAR(50),
    Работник_ID INT NOT NULL FOREIGN KEY REFERENCES Работник(ID),
);

CREATE TABLE Повар (
    ID INT PRIMARY KEY IDENTITY,
    Специализация NVARCHAR(50),
    Работник_ID INT NOT NULL FOREIGN KEY REFERENCES Работник(ID),
);

CREATE TABLE Кассир (
    ID INT PRIMARY KEY IDENTITY,
    Работник_ID INT NOT NULL FOREIGN KEY REFERENCES Работник(ID),
);

CREATE TABLE Склад (
    ID INT PRIMARY KEY IDENTITY,
    Тип NVARCHAR(50),
    Вместимость BIGINT
);

CREATE TABLE Продукт (
    ID INT PRIMARY KEY IDENTITY,
    Название NVARCHAR(50) NOT NULL,
    Количество DECIMAL(10, 2), 
    Калорийность DECIMAL(10, 2),
    Цена MONEY 
);

CREATE TABLE Блюдо (
    ID INT PRIMARY KEY IDENTITY,
    Название NVARCHAR(50) NOT NULL,
    Тип NVARCHAR(50),
    Калорийность DECIMAL(10, 2),
    Стоимость MONEY
);

CREATE TABLE Клиент (
    ID INT PRIMARY KEY IDENTITY,
    Имя NVARCHAR(50) NOT NULL,
    Фамилия NVARCHAR(50) NOT NULL,
    Номер_телефона NVARCHAR(50),
    Номер_паспорта NVARCHAR(50),
);

CREATE TABLE Заказ (
    ID INT PRIMARY KEY IDENTITY,
    Дата DATE,
    Время TIME,
    Стоимость MONEY,
    Кассир_ID INT NOT NULL FOREIGN KEY REFERENCES Кассир(ID),
    Клиент_ID INT NOT NULL FOREIGN KEY REFERENCES Клиент(ID),
);

CREATE TABLE Диетические_предпочтения (
    ID INT PRIMARY KEY IDENTITY,
    Название NVARCHAR(500) NOT NULL,
);

CREATE TABLE Кладовщик_склад (
    Кладовщик_ID INT NOT NULL FOREIGN KEY REFERENCES Кладовщик(ID),
    Cклад_ID INT NOT NULL FOREIGN KEY REFERENCES Склад(ID),
    PRIMARY KEY (Кладовщик_ID, Cклад_ID)
);

CREATE TABLE Кладовщик_продукт (
    Кладовщик_ID INT NOT NULL FOREIGN KEY REFERENCES Кладовщик(ID),
    Продукт_ID INT NOT NULL FOREIGN KEY REFERENCES Продукт(ID)
    PRIMARY KEY (Кладовщик_ID, Продукт_ID)
);

CREATE TABLE Продукт_склад (
    Продукт_ID INT NOT NULL FOREIGN KEY REFERENCES Продукт(ID),
    Cклад_ID INT NOT NULL FOREIGN KEY REFERENCES Склад(ID),
    PRIMARY KEY (Продукт_ID, Cклад_ID)
);

CREATE TABLE Повар_блюдо (
    Повар_ID INT NOT NULL FOREIGN KEY REFERENCES Повар(ID),
    Блюдо_ID INT NOT NULL FOREIGN KEY REFERENCES Блюдо(ID),
    PRIMARY KEY (Повар_ID, Блюдо_ID)
);

CREATE TABLE Продукт_блюдо (
    Продукт_ID INT NOT NULL FOREIGN KEY REFERENCES Продукт(ID),
    Блюдо_ID INT NOT NULL FOREIGN KEY REFERENCES Блюдо(ID),
    PRIMARY KEY (Продукт_ID, Блюдо_ID)
);

CREATE TABLE Заказ_блюдо (
    Заказ_ID INT NOT NULL FOREIGN KEY REFERENCES Заказ(ID),
    Блюдо_ID INT NOT NULL FOREIGN KEY REFERENCES Блюдо(ID),
    PRIMARY KEY (Заказ_ID, Блюдо_ID)
);

CREATE TABLE Клиент_Диетические_предпочтения (
    Клиент_ID INT NOT NULL FOREIGN KEY REFERENCES Клиент(ID),
    Диетические_предпочтения_ID INT NOT NULL FOREIGN KEY REFERENCES Диетические_предпочтения(ID),
    PRIMARY KEY (Клиент_ID, Диетические_предпочтения_ID)
);
```

### Таблица Работник:
![Рисунок1](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A21.PNG)
### Таблица Кладовщик:
![Рисунок2](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A22.PNG)
### Таблица Поставщик:
![Рисунок3](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A23.PNG)
### Таблица Повар:
![Рисунок4](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A24.PNG)
### Таблица Кассир:
![Рисунок5](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A25.PNG)
### Таблица Склад:
![Рисунок6](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A26.PNG)
### Таблица Продукт:
![Рисунок7](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A27.PNG)
### Таблица Блюдо:
![Рисунок8](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A28.PNG)
### Таблица Клиент:
![Рисунок9](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A29.PNG)
### Таблица Заказ:
![Рисунок10](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A210.PNG)
### Таблица Диети_еские_предпо_тения:
![Рисунок11](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A211.PNG)
### Таблица Кладовщик_склад:
![Рисунок12](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A212.PNG)
### Таблица Кладовщик_продукт:
![Рисунок13](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A213.PNG)
### Таблица Продукт_склад:
![Рисунок14](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A214.PNG)
### Таблица Повар_блюдо:
![Рисунок15](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A215.PNG)
### Таблица Заказ_блюдо:
![Рисунок16](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A216.PNG)
### Таблица Клиент_ДП:
![Рисунок17](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%A217.PNG)
### Диаграмма:
![Рисунок18](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%941.PNG)
![Рисунок19](https://github.com/vanserych/PMI-3/blob/e16b4a2acb053203fdbbe3cc3614afa87bec210c/%D0%9A%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B8/%D0%942.PNG)

# <a id="-lab3"></a><img src="https://github.com/user-attachments/assets/e080adec-6af7-4bd2-b232-d43cb37024ac" width="20" height="20"/> Lab3
<h1 align="center">📊 часть 1</h1>
https://github.com/vanserych/PMI-3/blob/344008daf3fbcf9a4e7975d43ef63dd5e103b2bc/%D0%A5%D1%80%D1%83%D0%BB%D0%B5%D0%B2_%D0%9F%D0%9C%D0%98-32%D0%91%D0%9E.docx
<h1 align="center">📊 часть 2</h1>
https://github.com/vanserych/PMI-3/blob/e32d2a0b310959d8c0df52c69fc4a2d6d3b57890/%D0%A5%D1%80%D1%83%D0%BB%D0%B5%D0%B2_%D0%9F%D0%9C%D0%98-32%D0%91%D0%9E%202.docx

# <a id="-lab4"></a><img src="https://github.com/user-attachments/assets/e080adec-6af7-4bd2-b232-d43cb37024ac" width="20" height="20"/> Lab4
https://github.com/vanserych/PMI-3/blob/7c6a79b5bdbdb9f696064ad69d0ee9c804de4e7c/%D0%9B%D0%B0%D0%B1%D0%BE%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BD%D0%B0%D1%8F%204%20%D0%B1%D0%B4.docx
