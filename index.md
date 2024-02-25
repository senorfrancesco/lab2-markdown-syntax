# This is a new markdown
## Step 1

![This image about the yellow mailbox](https://images.pexels.com/photos/11650554/pexels-photo-11650554.jpeg)

## This code about language ```Pandas```
```Python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

# Загрузка данных
car_data = pd.read_csv('Car details v3.csv')

# Извлечение бренда из названия
car_data['brand'] = car_data['name'].str.split(' ').str[0]

# Подготовка данных для диаграммы
pivot_df = car_data.groupby(['year', 'brand'])['brand'].size().unstack().fillna(0)

# Настройка параметров
N = len(pivot_df.index)
ind = np.arange(N)
width = 0.35

# Создание фигуры и осей
fig, ax = plt.subplots(figsize=(15, 10))

# Построение столбцов
for i, brand in enumerate(pivot_df.columns):
    bottom = 0 if i == 0 else pivot_df.iloc[:, :i].sum(axis=1)
    ax.bar(ind, pivot_df[brand], width, bottom=bottom, label=brand)

# Дополнительные элементы
ax.axhline(0, color='grey', linewidth=0.8)
ax.set_ylabel('Количество машин')
ax.set_title('Количество машин каждой марки по годам')
ax.set_xticks(ind)
ax.set_xticklabels(pivot_df.index)
ax.legend()

# Отображение диаграммы
plt.show()
```
