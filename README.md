{
 "cells": [
  {
   "cell_type": "markdown",
   "id": "f53f30ad",
   "metadata": {},
   "source": [
    "# 0. Описание задачи"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "80460fbb",
   "metadata": {},
   "source": [
    "## a) Введение"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "77f016ad",
   "metadata": {},
   "source": [
    "Инсульт - острое нарушение кровоснабжения головного мозг, характеризующееся внезапным (в течение нескольких минут, часов) появлением очаговой и/или общемозговой неврологической симптоматики. \n",
    "\n",
    "По данным Всемирной организации здравоохранения (ВОЗ) на 2011 год, инсульт занимал второе место среди причин смерти в мире (около 11% всех смертей). \n",
    "\n",
    "Есть ряд патологий, присутствие которых существенно увеличивает угрозу возникновения инсульта: \n",
    "    атеросклероз сосудов головного мозга; \n",
    "    мерцательная аритмия; \n",
    "    инфаркт миокарда;\n",
    "    наличие предыдущего инсульта;\n",
    "    почечная недостаточнойсть или дисфункция;\n",
    "    высокое артериальное давление; \n",
    "    варикозная болезнь; \n",
    "    нарушение свертываемости крови; \n",
    "    сахарный диабет; \n",
    "    ожирение; \n",
    "    тромботические риски с полицитемией;\n",
    "    малоподвижный образ жизни; \n",
    "    мужской пол;\n",
    "    наследственная предрасположенность;\n",
    "    курение, алкоголизм.\n",
    "\n",
    "Поскольку в последние годы все больше людей ведут сидячий образ жизни, который зачастую сопуствует с переработкой, то риск возникновения данного заболевания увеличивается. Так, иссследование 2016 года (https://www.sciencedirect.com/science/article/pii/S0160412021002208), посвещенное анализу воздействия длительного рабочего дня в 194 странах показали, что продолжительный рабочий день (>55 часов в неделю) стал причиной смерти 745 000 человек в результате инсульта и ишемической болезни сердца в 2016 г., что на 29 процентов больше, чем в 2000 г. Этот эффект связанный с переработкой особенно велико среди мужчин (на них приходится 72% смертей). В исследовании делается вывод о том, что при работе в течение 55 или более часов в неделю риск инсульта повышается примерно на 35%, а риск ишемической болезни сердца – на 17% по сравнению с работой в течение 35‑40 часов в неделю.\n",
    "\n",
    "В силу возрастающего риска возникновения инсульта, существует потребность в мониторинге здоровья людей с использованием некоторых биомаркеров. Факторы риска, описанные выше могут быть разделены на модифицируемые факторы, которые могут блокированы с помощью антитромботические препаратов, бета-блокаторов, изменения образа жизни, а также немодифицируемые факторы, такие как возраст, предыдущий инсульт, почечная недостаточность и т.п.\n",
    "\n",
    "Таким образом, анализ состояния здоровья человека и его предрасположенности к некоторым заболеваниям, может помочь вовремя обратить нимание на риски развития инсульта и при своевременной корректироваки образа жизни/применение препоратов можно избежать возникновения инсульта. "
   ]
  },
  {
   "cell_type": "markdown",
   "id": "fa61e2ac",
   "metadata": {},
   "source": [
    "## b) Описание данных "
   ]
  },
  {
   "cell_type": "markdown",
   "id": "88b1f377",
   "metadata": {},
   "source": [
    "Этот набор данных используется для прогнозирования вероятности инсульта у пациента на основе неоторых факторов риска таких как пол, возраст, различные заболевания и статус курения и т.п. Общий перечень исследуемых факторов был представлен создателями dataset:\n",
    "\n",
    "1) id: Уникальный номер человека\n",
    "2) gender: \"Male\", \"Female\" or \"Other\"\n",
    "3) age: Возраст пациента\n",
    "4) hypertension: 0 если пациент никогда не имел гипертензию, 1 если у человека была гипертензия (гипертензия представляет собой стойкое повышение кровяного давления)\n",
    "5) heart_disease: 0 если пациент никогда не имел сердечных заболеваний, 1 если у человека были сердечные заболевания\n",
    "6) ever_married: \"No\" or \"Yes\" # А в факторах риска такого не было... \n",
    "7) work_type: \"children\", \"Govt_jov\", \"Never_worked\", \"Private\" or \"Self-employed\"\n",
    "8) Residence_type: \"Rural\" или \"Urban\" # Предположительно человек живущий в городе мало двигается, что увеличивает риски развития инсульта \n",
    "9) avg_glucose_level: средний уровень глюкозы в крови\n",
    "10) bmi: индекс массы тела\n",
    "11) smoking_status: \"formerly smoked\", \"never smoked\", \"smokes\" or \"Unknown\"*\n",
    "12) stroke: 1 если у человека был инсульт и 0 если не было"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "68062523",
   "metadata": {},
   "source": [
    "## c) Описание задачи"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "94452a1d",
   "metadata": {},
   "source": [
    "Нужно предсказать, был ли инсульт у человека "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "id": "dc4b4689",
   "metadata": {},
   "outputs": [],
   "source": [
    "import numpy as np              \n",
    "import matplotlib.pyplot as plt \n",
    "%matplotlib inline \n",
    "    # Говорим jupyter'у, чтобы весь графический вывод был в браузере, а не в отдельном окне\n",
    "import pandas as pd             \n",
    "import seaborn as sns           \n",
    "import sklearn                  # Алгоритмы машинного обучения"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "42b78bff",
   "metadata": {},
   "source": [
    "# 1. Чтение данных"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "id": "d6d37fb8",
   "metadata": {},
   "outputs": [],
   "source": [
    "data_raw = pd.read_csv(\"./healthcare-dataset-stroke-data.csv\") # прочитала данные из локальной дирректории.Почему-то не удалось прочитать данные с git (см. ниже)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "id": "91165f38",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Почему-то не получается(?)\n",
    "#data = \"https://github.com/enot9910/ML_EEG/blob/main/data/EEG_data.csv\"\n",
    "#data_raw = pd.read_csv(data)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f5cbdc26",
   "metadata": {},
   "source": [
    "## Посмотрим, что из себя представляют данные"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "id": "1af42e68",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>id</th>\n",
       "      <th>gender</th>\n",
       "      <th>age</th>\n",
       "      <th>hypertension</th>\n",
       "      <th>heart_disease</th>\n",
       "      <th>ever_married</th>\n",
       "      <th>work_type</th>\n",
       "      <th>Residence_type</th>\n",
       "      <th>avg_glucose_level</th>\n",
       "      <th>bmi</th>\n",
       "      <th>smoking_status</th>\n",
       "      <th>stroke</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>9046</td>\n",
       "      <td>Male</td>\n",
       "      <td>67.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>Yes</td>\n",
       "      <td>Private</td>\n",
       "      <td>Urban</td>\n",
       "      <td>228.69</td>\n",
       "      <td>36.6</td>\n",
       "      <td>formerly smoked</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>51676</td>\n",
       "      <td>Female</td>\n",
       "      <td>61.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>Yes</td>\n",
       "      <td>Self-employed</td>\n",
       "      <td>Rural</td>\n",
       "      <td>202.21</td>\n",
       "      <td>NaN</td>\n",
       "      <td>never smoked</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>31112</td>\n",
       "      <td>Male</td>\n",
       "      <td>80.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>Yes</td>\n",
       "      <td>Private</td>\n",
       "      <td>Rural</td>\n",
       "      <td>105.92</td>\n",
       "      <td>32.5</td>\n",
       "      <td>never smoked</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>60182</td>\n",
       "      <td>Female</td>\n",
       "      <td>49.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>Yes</td>\n",
       "      <td>Private</td>\n",
       "      <td>Urban</td>\n",
       "      <td>171.23</td>\n",
       "      <td>34.4</td>\n",
       "      <td>smokes</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>1665</td>\n",
       "      <td>Female</td>\n",
       "      <td>79.0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>Yes</td>\n",
       "      <td>Self-employed</td>\n",
       "      <td>Rural</td>\n",
       "      <td>174.12</td>\n",
       "      <td>24.0</td>\n",
       "      <td>never smoked</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>56669</td>\n",
       "      <td>Male</td>\n",
       "      <td>81.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>Yes</td>\n",
       "      <td>Private</td>\n",
       "      <td>Urban</td>\n",
       "      <td>186.21</td>\n",
       "      <td>29.0</td>\n",
       "      <td>formerly smoked</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6</th>\n",
       "      <td>53882</td>\n",
       "      <td>Male</td>\n",
       "      <td>74.0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>Yes</td>\n",
       "      <td>Private</td>\n",
       "      <td>Rural</td>\n",
       "      <td>70.09</td>\n",
       "      <td>27.4</td>\n",
       "      <td>never smoked</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>7</th>\n",
       "      <td>10434</td>\n",
       "      <td>Female</td>\n",
       "      <td>69.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>No</td>\n",
       "      <td>Private</td>\n",
       "      <td>Urban</td>\n",
       "      <td>94.39</td>\n",
       "      <td>22.8</td>\n",
       "      <td>never smoked</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>8</th>\n",
       "      <td>27419</td>\n",
       "      <td>Female</td>\n",
       "      <td>59.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>Yes</td>\n",
       "      <td>Private</td>\n",
       "      <td>Rural</td>\n",
       "      <td>76.15</td>\n",
       "      <td>NaN</td>\n",
       "      <td>Unknown</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>9</th>\n",
       "      <td>60491</td>\n",
       "      <td>Female</td>\n",
       "      <td>78.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>Yes</td>\n",
       "      <td>Private</td>\n",
       "      <td>Urban</td>\n",
       "      <td>58.57</td>\n",
       "      <td>24.2</td>\n",
       "      <td>Unknown</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "      id  gender   age  hypertension  heart_disease ever_married  \\\n",
       "0   9046    Male  67.0             0              1          Yes   \n",
       "1  51676  Female  61.0             0              0          Yes   \n",
       "2  31112    Male  80.0             0              1          Yes   \n",
       "3  60182  Female  49.0             0              0          Yes   \n",
       "4   1665  Female  79.0             1              0          Yes   \n",
       "5  56669    Male  81.0             0              0          Yes   \n",
       "6  53882    Male  74.0             1              1          Yes   \n",
       "7  10434  Female  69.0             0              0           No   \n",
       "8  27419  Female  59.0             0              0          Yes   \n",
       "9  60491  Female  78.0             0              0          Yes   \n",
       "\n",
       "       work_type Residence_type  avg_glucose_level   bmi   smoking_status  \\\n",
       "0        Private          Urban             228.69  36.6  formerly smoked   \n",
       "1  Self-employed          Rural             202.21   NaN     never smoked   \n",
       "2        Private          Rural             105.92  32.5     never smoked   \n",
       "3        Private          Urban             171.23  34.4           smokes   \n",
       "4  Self-employed          Rural             174.12  24.0     never smoked   \n",
       "5        Private          Urban             186.21  29.0  formerly smoked   \n",
       "6        Private          Rural              70.09  27.4     never smoked   \n",
       "7        Private          Urban              94.39  22.8     never smoked   \n",
       "8        Private          Rural              76.15   NaN          Unknown   \n",
       "9        Private          Urban              58.57  24.2          Unknown   \n",
       "\n",
       "   stroke  \n",
       "0       1  \n",
       "1       1  \n",
       "2       1  \n",
       "3       1  \n",
       "4       1  \n",
       "5       1  \n",
       "6       1  \n",
       "7       1  \n",
       "8       1  \n",
       "9       1  "
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data_raw.head(10) # посмотрю на первые 10 строчек данных "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "id": "e639cc13",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(5110, 12)"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data_raw.shape # посмотрю на размеры таблицы с данными"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "9a7dfde9",
   "metadata": {},
   "source": [
    "# 4. Обработка пропущенных значений"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "id": "653c6371",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "id                     0\n",
       "gender                 0\n",
       "age                    0\n",
       "hypertension           0\n",
       "heart_disease          0\n",
       "ever_married           0\n",
       "work_type              0\n",
       "Residence_type         0\n",
       "avg_glucose_level      0\n",
       "bmi                  201\n",
       "smoking_status         0\n",
       "stroke                 0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data_raw.isna().sum() # Смотрю, сколько всего вропущенных значений в разных категориях"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "7499e662",
   "metadata": {},
   "source": [
    "Таким образов в dataset содержится данные с пропущенными значениями. У нас 2 пути: \n",
    "\n",
    "1.Заполнить пропущенные значения \n",
    "2.Исключить проущенные значения \n",
    "\n",
    "Поскольку у нас достаточное количесвто данных, я выберу второй путь."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "id": "c8a4cc18",
   "metadata": {},
   "outputs": [],
   "source": [
    "data_raw = data_raw.dropna() # удалила всезначения, где нет данных о"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "id": "2d8df0e2",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(4909, 12)"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data_raw.shape # Хочу вывести новые размеры таблицы с учетом того, что я удалила строки с отсутвующими значениями"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "871b33f3",
   "metadata": {},
   "source": [
    "Хочу еще чуть-чуть почистить данные. В категории 'gender' я обратила внимание на вариант 'other'. Если таких данных не слишком много, мне бы хотелось удалить соотвествующие строчки. Для этого выведу количество человек раличных полов:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "id": "6a7e818d",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Female    2897\n",
       "Male      2011\n",
       "Other        1\n",
       "Name: gender, dtype: int64"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data_raw.gender.value_counts()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "7d6891eb",
   "metadata": {},
   "source": [
    "Мы видим, что в datas всего один человек с полом 'other', поэтому удалю соотвествующую строчку:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "id": "c7633f52",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(4908, 12)"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data_raw = data_raw[data_raw.gender != 'Other'] # Удаляю строчку если gender = 'Other'\n",
    "data_raw.shape # Хочу проверить, корректно ли почистились данные ((4909, 12) -> (4908, 12))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "604f1620",
   "metadata": {},
   "source": [
    "# 3. Визуализация данных"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "id": "efe93c6f",
   "metadata": {},
   "outputs": [],
   "source": [
    "data_raw = data_raw.drop(data_raw.iloc[:,[0]], axis = 1) # Поскольку \"id\" обозначает номер пациента не влияет на классификацию, я от него избавляюсь"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "66546f56",
   "metadata": {},
   "source": [
    "## Выведу график корреляции для dataset"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "id": "f477c5d3",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:>"
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 640x480 with 2 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.heatmap(data_raw.corr(), cmap = 'coolwarm', annot=True, linewidths=1)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "696f93b5",
   "metadata": {},
   "source": [
    "   Из корреляционный матрицы видно, что сильных корреляций (> 0.5) нет. \n",
    "   \n",
    "   Самый большой для инсульта коэффицент корреляции - коэффициент между инсультом и возрастом.Зависимость между инсультом и гипертонией, уровнем глюкозы в крови, сердечными заболеваниями присутсвует, однако меньше, чем для возраста. Что касается зависимости между инсультом и индексом массы тела, то она почти нулевая \n",
    "\n",
    "   Что касается других корреляций, то наименьшая зависимость есть между сердечными заболеваниями и индексом массы тела (Возникает вопрос о корректности данных, поскольку исследования показывают обратную корреляцию). С возрастом имеется корреляция для всех категорий (повышенного давления, болезей сердца, повышенного уровня глюкозы, индексом массы тела, инсульта)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "d6e9baa6",
   "metadata": {},
   "source": [
    "## Рассмотрю подробней числовые характеристики"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "46c1f8d4",
   "metadata": {},
   "source": [
    "Признаки \"Gender\"(нулевой столбец), \"hypertension\"(второй стобец), \"heart_disease\"(третий столбец), \"ever_married\" (четвертый столбец), \"work_type\" (пятый столбец), \"Residence_type\" (шестой столбец), \"smoking_status\" (9 столбец), \"stroke\" (10 столбец) являются категориальными."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "id": "e9e6adf3",
   "metadata": {},
   "outputs": [],
   "source": [
    "data_raw.iloc[:,[0, 2, 3, 4, 5, 6, 9, 10]] = data_raw.iloc[:,[0, 2, 3, 4, 5, 6, 9, 10]].astype('category') # определила часть столбцов в категориальные данные (iloc - описывает столбцы)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "5753af1a",
   "metadata": {},
   "source": [
    "Выведу описательную статичтику для количественных данных (age, avg_glucose_level, bmi)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "id": "f1df5a69",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>age</th>\n",
       "      <th>avg_glucose_level</th>\n",
       "      <th>bmi</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>4908.000000</td>\n",
       "      <td>4908.000000</td>\n",
       "      <td>4908.00000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>42.868810</td>\n",
       "      <td>105.297402</td>\n",
       "      <td>28.89456</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>22.556128</td>\n",
       "      <td>44.425550</td>\n",
       "      <td>7.85432</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>0.080000</td>\n",
       "      <td>55.120000</td>\n",
       "      <td>10.30000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>25.000000</td>\n",
       "      <td>77.067500</td>\n",
       "      <td>23.50000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>44.000000</td>\n",
       "      <td>91.680000</td>\n",
       "      <td>28.10000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>60.000000</td>\n",
       "      <td>113.495000</td>\n",
       "      <td>33.10000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>82.000000</td>\n",
       "      <td>271.740000</td>\n",
       "      <td>97.60000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "               age  avg_glucose_level         bmi\n",
       "count  4908.000000        4908.000000  4908.00000\n",
       "mean     42.868810         105.297402    28.89456\n",
       "std      22.556128          44.425550     7.85432\n",
       "min       0.080000          55.120000    10.30000\n",
       "25%      25.000000          77.067500    23.50000\n",
       "50%      44.000000          91.680000    28.10000\n",
       "75%      60.000000         113.495000    33.10000\n",
       "max      82.000000         271.740000    97.60000"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data_num = data_raw\n",
    "data_num = data_num.drop(['stroke'], axis = 1)\n",
    "data_num.describe() # таблица будет отписывать среднее значение, стандартное отоклонение, минимальное и максимальное значение для каждого количественного признака"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "4ee7b0ac",
   "metadata": {},
   "source": [
    "Из таблицы видно, что у нас в данных есть люди,чей возраст слишком мал для анализа инсульта (min(age) = 0.08). Предположительно, люди меньше какого-то возраста с наличием инсульта будут выбросами на plt.scatter"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "id": "597ed855",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.collections.PathCollection at 0x22eb56f8b50>"
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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det8I36HkSNHjqiiokIVFRWSTn51t6KiQtXV1ZJO3mLJzs52tc/JydH+/fuVl5en3bt3a/ny5Vq2bJkefvjhrjkCnHM3J8Wq+M4xinG4X0qPcYTxtd5u1hPGwlsfYh1hGjXY81VMX+YZ+brtPnBNgmJ9OOZXsq/2GkjsNveXO2/b7RMaojPvIAcHSfH9fX9hvrhvqE/tgoNOvoH7mh/DewX73NYfNj/eCcJ7eW585jwjnzw12edA4u958PX8+sufcxsa4ntjf85vT/izrivnGfGV3/OMrFu3Ttddd12H+t13360VK1Zo5syZqqqq0rp161yPrV+/XvPmzXNNevboo48y6VkA6gmzfuKknjAWzMDKDKzMwMoMrGdzziY9M4EwAgBA4PH1/Zt/lAcAAIwijAAAAKMIIwAAwCjCCAAAMIowAgAAjCKMAAAAowgjAADAKMIIAAAwijACAACMIowAAACjCCMAAMAowggAADCKMAIAAIwijAAAAKMIIwAAwCjCCAAAMIowAgAAjCKMAAAAowgjAADAKMIIAAAwijACAACMIowAAACjCCMAAMAowggAADCKMAIAAIwijAAAAKMIIwAAwCjCCAAAMIowAgAAjCKMAAAAowgjAADAKMIIAAAwijACAACMIowAAACjCCMAAMAowggAADCKMAIAAIwijAAAAKMIIwAAwCjCCAAAMIowAgAAjCKMAAAAowgjAADAKMIIAAAwijACAACMIowAAACjCCMAAMAowggAADCKMAIAAIwijAAAAKMIIwAAwCjCCAAAMIowAgAAjCKMAAAAowgjAADAKMIIAAAwijACAACM6lQYKSoqUkJCgsLCwpScnKyNGzd+bfuVK1fqyiuvVO/evRUbG6t77rlHhw4d6lSHAQDA+cXvMFJSUqLc3FwtXLhQO3bsUFpamjIyMlRdXe2x/aZNm5Sdna377rtPu3bt0jvvvKO//OUvuv/++79x5wEAQODzO4w8//zzuu+++3T//fcrMTFRS5YsUVxcnIqLiz22/9Of/qShQ4dqzpw5SkhI0MSJE/XAAw9o+/bt37jzAAAg8PkVRlpaWlReXq709HS3enp6urZs2eJxndTUVH3xxRcqLS2VZVn68ssv9etf/1qZmZle99Pc3Cyn0+m2AACA85NfYaShoUFtbW2Kjo52q0dHR6uurs7jOqmpqVq5cqWy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\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.scatter(data_raw['age'],data_raw['stroke'])"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "c06b2647",
   "metadata": {},
   "source": [
    "Мы видим, что на граффике есть выброс (у человека меньше 20 лет)."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "id": "6f186ab0",
   "metadata": {},
   "outputs": [],
   "source": [
    "indexAge = data_raw[((data_raw['age'] < 20) & (data_raw['stroke'] == 1)) ].index  # удаляю выброс (количество данных: (4908, 11)->(4907, 11))\n",
    "data_raw.drop(indexAge , inplace=True) "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "id": "90f0791b",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(4907, 11)"
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data_raw.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "id": "5256152d",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Не знаю, как лучше было сделать. Просто удалить выброс или удалить значения у всех людей, кто младше 20(?). Оставила первый вариант, т.к. он не такой грубый\n",
    "# data_raw = data_raw[data_raw.age > 20] # удалю данные о людях меньше 20 лет\n",
    "# data_raw.shape #(3908,11)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "cef2752d",
   "metadata": {},
   "source": [
    "## После чистки данных хочу посмотреть на зависимость между возрастом и инстультом поподробней "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "id": "3b2205fc",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:xlabel='stroke', ylabel='age'>"
      ]
     },
     "execution_count": 19,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.boxplot(x=\"stroke\", y=\"age\", data = data_raw)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "d5630e2d",
   "metadata": {},
   "source": [
    "Из диаграммы видно, что отсутствие инсульта больше характерно для людей до 60 лет, при этом для второй подгруппы видно, что люди старше 60 лет больше склонны к инсульту."
   ]
  },
  {
   "cell_type": "markdown",
   "id": "9cb3a5a9",
   "metadata": {},
   "source": [
    "Выведу матрицу корреляции для числовых значений"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "id": "6599eb7d",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:>"
      ]
     },
     "execution_count": 20,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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Xr906RIGDx4MNzc3ODo6ok2bNkhISNC9LuXnprS0FG+//TaaNGkCR0dHdO7cGb///jsAoKCgAPb29ti2bZveMZs2bYKjoyOKiooAAFlZWYiMjISbmxs8PDwwdOhQXLx40ax46pPy8nK89tprus/2nDlzcG8JGD8/PyxYsABRUVFwcnKCr68vfv75Z1y/fh1Dhw6Fk5MT2rZti8OHD+v64zABVRWTgRpQXFyM6OhoHDp0CDt37oRMJsPw4cOh1WpRWFiIwYMHo23btjh69Cj++c9/4p133tE7Xq1Wo1evXujQoQMOHz6Mbdu24dq1axg5cqSF3pFlPOz3OHr0aKxfvx5/X0MrPj4eKpUKvXr1AgBERUXh6tWr+P3337Fx40bExcUhJyfHpHNrtVoMGzYMDg4OOHDgAOLi4jB79uzHfk+//PILRowYgYEDByI1NRU7d+5EWFiY7vVx48bh8OHD2LJlC/bv3w9RFDFgwACUlZUBAF599VWUlJRg7969OHHiBD766CM4OTkBkP5zM378eCQnJ+OHH35AWloaXnjhBfTr1w9nz56Fq6srBg4ciLVr1+ods27dOt0F6/bt2+jduzecnJywd+9eJCUlwcnJCf369UNpaamZv8H64dtvv4VCocCBAwfwxRdfYNGiRVixYoXu9UWLFqFbt25ITU3FwIEDMWbMGERFReGll17C0aNHERAQgKioKHANOTKbSDUuJydHBCCeOHFCXLp0qejh4SHeuXNH9/ry5ctFAGJqaqooiqI4d+5cMSIiQq+Py5cviwDE06dP12Totcrff485OTmiQqEQ9+7dq3s9PDxcfOutt0RRFMX09HQRgHjo0CHd62fPnhUBiIsWLXrkuX799VdRoVCIarVa15aYmCgCEH/66SdRFEUxIyND7+/tm2++EV1dXfX6+emnn8S//7MLDw8XR48eXek5z5w5IwIQk5OTdW25ubmivb29+J///EcURVFs27at+N5771V6/ON+bnr16iVOnz5dFEVRPHfunCgIgpiVlaW3T58+fcSYmBhRFEVx06ZNopOTk1hcXCyKoigWFBSISqVS/OWXX0RRFMWVK1eKgYGBolar1R1fUlIi2tvbi9u3bxdFURTHjh0rDh069JGx1Se9evUSg4OD9X4v77zzjhgcHCyKoij6+vqKL730ku41tVotAhDnzp2ra9u/f78I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\n",
      "text/plain": [
       "<Figure size 640x480 with 2 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.heatmap(data_raw.corr(), cmap = 'coolwarm', annot=True)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "89197858",
   "metadata": {},
   "source": [
    "Мы видим, что для этих числовых данных сохраняется корреляция. Самая больша между возрастом и индексом массы тела"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "a72c9766",
   "metadata": {},
   "source": [
    "## Посмотрим, сбалансированы ли наши данные "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "id": "ad30b79c",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:xlabel='stroke', ylabel='count'>"
      ]
     },
     "execution_count": 21,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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ZYvuvPNOHT58WD6fT2vWrJEkRUVF6dixY5KkefPmaenSpVqzZo3sdruefvppLV26VKtWrdL111+vF154Qenp6dq/f7/i4+MD3rOurk4ZGRn67LPPtHXrVsXExOjdd9/Vr3/9az3zzDMaMmSIPvvsM02dOlWStGDBgtb9oQC4KPxr9wDanX/+859KSkrS559/rp49ewY8dtddd6myslKvvfaatfb555+rV69eWrFihR588EFr/YorrtD06dP18MMPW2s33XSTbrzxRv3ud7+znrdlyxYtWrRINTU1evvtt+VwOCRJQ4cO1bhx4zR//nzr+evWrdPcuXOtCAPQPnCGCEC7079/f40cOVKJiYkaM2aMUlNT9ctf/lJdu3Y97/MGDBhg/bfP59OxY8c0ePDggJnBgwfrX//6V8Da7bffrh49eui9995T586drfWioiLt2rVLTz75pLVWX1+vU6dO6eTJkwGzANo2riEC0O6EhIQoPz9f77zzjvr166dnn31Wffr0UXFx8Xmf16VLl0ZrNpst4L7f72+0dsstt2jPnj0qLCwMWG9oaNCiRYvk8Xis2969e/XJJ5+oU6dOTTw6AMHAGSIA7ZLNZtPgwYM1ePBgPfbYY+rZs6dyc3MVFham+vr673x+ZGSkXC6Xtm7dqqFDh1rr27Zt00033RQwe//99yshIUHp6el6++23NWzYMEnSDTfcoEOHDumqq65q3oMD0OoIIgDtzo4dO/Tee+8pNTVVMTEx2rFjh8rLy9W3b1+dOnVK7777rg4dOqTo6Gjrep9zeeihh7RgwQL96Ec/0nXXXac1a9bI4/Fo/fr1jWZnzJih+vp6paWl6Z133tFPfvITPfbYY0pLS1NcXJxuu+02dejQQXv27NHevXv1xBNPtOSPAEAzI4gAtDuRkZH64IMPtGLFCvl8PvXs2VNLly7VuHHjNGDAAG3evFkDBgxQdXW13n//ff3whz885+vMnDlTPp9Ps2fPVllZmfr166c33nij0SfMznC73WpoaNAtt9yivLw8jRkzRm+99ZYef/xxLVmyRB07dtQ111yje+65pwWPHkBL4FNmAADAeFxUDQAAjEcQAQAA4xFEAADAeAQRAAAwHkEEAACMRxABAADjEUQAAMB4BBEAADAeQQQAAIxHEAEAAOMRRAAAwHj/D7/+X89JU12dAAAAAElFTkSuQmCC\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.countplot(x=\"stroke\", data = data_raw)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "008973e4",
   "metadata": {},
   "source": [
    "Классы в задаче не сблансированы"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "6ec3c975",
   "metadata": {},
   "source": [
    "## Рассмотрим подробней категориальные данные и зависимость инсульта от категориальных данных "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "id": "bb309f48",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>gender</th>\n",
       "      <th>hypertension</th>\n",
       "      <th>heart_disease</th>\n",
       "      <th>ever_married</th>\n",
       "      <th>work_type</th>\n",
       "      <th>Residence_type</th>\n",
       "      <th>smoking_status</th>\n",
       "      <th>stroke</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>4907</td>\n",
       "      <td>4907</td>\n",
       "      <td>4907</td>\n",
       "      <td>4907</td>\n",
       "      <td>4907</td>\n",
       "      <td>4907</td>\n",
       "      <td>4907</td>\n",
       "      <td>4907</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>unique</th>\n",
       "      <td>2</td>\n",
       "      <td>2</td>\n",
       "      <td>2</td>\n",
       "      <td>2</td>\n",
       "      <td>5</td>\n",
       "      <td>2</td>\n",
       "      <td>4</td>\n",
       "      <td>2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>top</th>\n",
       "      <td>Female</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>Yes</td>\n",
       "      <td>Private</td>\n",
       "      <td>Urban</td>\n",
       "      <td>never smoked</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>freq</th>\n",
       "      <td>2896</td>\n",
       "      <td>4456</td>\n",
       "      <td>4664</td>\n",
       "      <td>3204</td>\n",
       "      <td>2810</td>\n",
       "      <td>2490</td>\n",
       "      <td>1852</td>\n",
       "      <td>4699</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "        gender  hypertension  heart_disease ever_married work_type  \\\n",
       "count     4907          4907           4907         4907      4907   \n",
       "unique       2             2              2            2         5   \n",
       "top     Female             0              0          Yes   Private   \n",
       "freq      2896          4456           4664         3204      2810   \n",
       "\n",
       "       Residence_type smoking_status  stroke  \n",
       "count            4907           4907    4907  \n",
       "unique              2              4       2  \n",
       "top             Urban   never smoked       0  \n",
       "freq             2490           1852    4699  "
      ]
     },
     "execution_count": 22,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data_raw.describe(include = ['category'])"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "19d90f42",
   "metadata": {},
   "source": [
    "## Зависимость от типа работы"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "46ab85cb",
   "metadata": {},
   "source": [
    "Можно предположить, что от типа работы может зависеть наличие или отсутсвие инсульта. Давайте проверим это"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "id": "3c88452f",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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y5YtGTFiROUcK1euzMCBAzN37twcPXo0l112WdatW5cBAwb01bAA4IwR7AGAPrVx48ZnPV4qldLU1JSmpqZT1gwZMiSrV6/O6tWre7h3AND/ecYeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDA+jTYL1++PBdccEFGjBiRsWPH5sorr8yjjz7araZcLqepqSl1dXUZOnRopk2blr1793ar6ezszMKFCzNmzJgMHz48c+bMyYEDB7rVtLW15Zprrkl1dXWqq6tzzTXX5IknnujtIQIAAECv6tNgv23bttx4443ZuXNntm7dmt/97neZOXNmnnzyyUrNihUrctttt2XNmjXZtWtXamtrM2PGjBw+fLhS09jYmE2bNmXjxo3Zvn17jhw5ktmzZ+f48eOVmnnz5mX37t3ZvHlzNm/enN27d+eaa645o+MFAACAnjawL7988+bN3fbvuuuujB07Ni0tLXnb296WcrmcVatW5ZZbbslVV12VJLn77rtTU1OTDRs25IYbbkh7e3vWrl2be++9N9OnT0+SrF+/PvX19bn//vtz+eWX55FHHsnmzZuzc+fOTJ48OUly55135qKLLsqjjz6a1772tWd24AAAANBD+tUz9u3t7UmSUaNGJUn27duX1tbWzJw5s1JTVVWVqVOnZseOHUmSlpaWHDt2rFtNXV1dJkyYUKn5t3/7t1RXV1dCfZJceOGFqa6urtQAAABAEfXpiv0fKpfLWbRoUd7ylrdkwoQJSZLW1tYkSU1NTbfampqa/PSnP63UDB48OGedddYJNU9/vrW1NWPHjj3hO8eOHVupeabOzs50dnZW9js6Ok5zZAAAANB7+s2K/U033ZQf/OAH+Zd/+ZcTjpVKpW775XL5hLZnembNyeqf7TzLly+vvGivuro69fX1z2cYAAAAcEb1i2C/cOHCfPnLX863vvWtnHPOOZX22traJDlhVf3QoUOVVfza2tp0dXWlra3tWWt++ctfnvC9jz/++Al3Azxt2bJlaW9vr2z79+8//QEC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/PM//3NWrFiRgwcPZsKECVm5cmXe9ra39XW3oFAeeOCBXHLJJSe0X3vttVm3bt2Z7xDAHzDXwwtnrn9xEuwBAACgwDxjDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII90C/85Cc/SalUyu7du/u6KwBALzHfQ+8Q7IHTdt111+XKK6/s624AAL3IfA/9n2AP9Lpjx471dRcAgF5mvoe+I9gDz+lf//VfM3HixAwdOjSjR4/O9OnT83d/93e5++6786UvfSmlUimlUikPPPBA5Ra7/+f/+X8ybdq0DBkyJOvXr89TTz2VT3ziEznnnHNSVVWVN73pTdm8efMpv/Opp57K9ddfn9e85jX56U9/miT5yle+kkmTJmXIkCF51atelY9//OP53e9+d6b+GgDgRc18D8U1sK87APRvBw8ezHvf+96sWLEi73znO3P48OF8+9vfzt/8zd/kZz/7WTo6OnLXXXclSUaNGpVf/OIXSZKbb745t956a+66665UVVXln/7pn3LrrbfmM5/5TN785jfns5/9bObMmZO9e/emoaGh23d2dXVl3rx5+Y//+I9s3749Y8eOzX333Ze//uu/zv/4H/8jb33rW/Mf//Ef+eAHP5gk+Yd/+Icz+5cCAC8y5nsouDLAs2hpaSknKf/kJz854di1115b/su//Mtubfv27SsnKa9atapbe11dXflTn/pUt7YLLrigvGDBgm6f+/a3v12ePn16+eKLLy4/8cQTldq3vvWt5ebm5m6fv/fee8vjxo17IcMDAMrmeyg6K/bAszrvvPNy2WWXZeLEibn88sszc+bM/NVf/VXOOuusZ/3c+eefX/lzR0dHfvGLX+Tiiy/uVnPxxRfn//1//99ube9973tzzjnn5Bvf+EaGDRtWaW9pacmuXbvyqU99qtJ2/Pjx/Pa3v81vfvObbrUAwB/HfA/F5hl74FkNGDAgW7duzde//vW8/vWvz+rVq/Pa1742+/bte9bPDR8+/IS2UqnUbb9cLp/Q9o53vCM/+MEPsnPnzm7tTz31VD7+8Y9n9+7dle3hhx/OY489liFDhpzm6ACAxHwPRWfFHnhOpVIpF198cS6++OL8/d//fc4999xs2rQpgwcPzvHjx5/z8yNHjkxdXV22b9+et73tbZX2HTt25L/+1//arfbD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\n",
      "text/plain": [
       "<Figure size 1200x1200 with 4 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "fig, ax = plt.subplots(2,2, figsize=(12,12))\n",
    "\n",
    "sns.countplot(ax=ax[0,0], data=data_raw[data_raw.work_type == 'Private'], x='stroke')\n",
    "sns.countplot(ax=ax[0,1], data=data_raw[data_raw.work_type == 'Govt_job'], x='stroke')\n",
    "sns.countplot(ax=ax[1,0], data=data_raw[data_raw.work_type == 'Self-employed'], x='stroke')\n",
    "sns.countplot(ax=ax[1,1], data=data_raw[data_raw.work_type == 'Never_worked'], x='stroke')\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "e8d48d3a",
   "metadata": {},
   "source": [
    "В группе неработающих инсульта нет ;) И здесь мы можем вернуться к началу notebook, где приводилась статья, показывающая влияние переработки на риск возникновения инсульта. "
   ]
  },
  {
   "cell_type": "markdown",
   "id": "eb307227",
   "metadata": {},
   "source": [
    "## Зависимость от места проживания (город/деревня)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "id": "de8fe241",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAA/YAAAISCAYAAABmulR0AAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjUuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8qNh9FAAAACXBIWXMAAA9hAAAPYQGoP6dpAAAyqElEQVR4nO3de5DV5YHn/88JSIMOdATsbnolLJlBxwyscdDlYlS8BCSFjHE2ZsKG0RqDmVGxWDRmHSsGUwnUuOVlFyqOcYwa0TFbMyHGSaYjmogyiBrKXi/rsCaLI660GAPdotggnN8fKc4vLYoJNpx+4PWqOlWc73n68HyptE/e53s5lWq1Wg0AAABQpA/VewIAAADA3hP2AAAAUDBhDwAAAAUT9gAAAFAwYQ8AAAAFE/YAAABQMGEPAAAABRP2AAAAUDBhDwAAAAUT9gAAAFCwuob9okWLcsIJJ2Tw4MFpamrK2WefnbVr1/YYc/7556dSqfR4TJw4sceY7u7uzJ07N8OHD89hhx2WmTNn5qWXXuoxZtOmTZk9e3YaGxvT2NiY2bNnZ/Pmzft6FwEAAGCfqmvYr1ixIhdffHFWr16d5cuX5+23387UqVPzxhtv9Bh35plnZsOGDbXHj370ox6vz5s3L8uWLcs999yTlStXZsuWLZkxY0Z27NhRGzNr1qy0t7enra0tbW1taW9vz+zZs/fLfgIAAMC+UqlWq9V6T2KXV199NU1NTVmxYkVOPvnkJL8+Yr958+Z8//vff9ef6ezszBFHHJE777wzn/3sZ5MkL7/8ckaOHJkf/ehHmTZtWp577rl87GMfy+rVqzNhwoQkyerVqzNp0qT867/+a44++uj9sn8AAADQ2/rXewK/qbOzM0kydOjQHtsfeuihNDU15cMf/nBOOeWUfOMb30hTU1OSZM2aNdm+fXumTp1aG9/a2pqxY8dm1apVmTZtWh599NE0NjbWoj5JJk6cmMbGxqxatepdw767uzvd3d215zt37syvfvWrDBs2LJVKpVf3GwD2RrVazeuvv57W1tZ86ENum/NB7dy5My+//HIGDx5srQegT/ht1/o+E/bVajXz58/PJz7xiYwdO7a2ffr06fnMZz6TUaNGZd26dfnKV76S0047LWvWrElDQ0M6OjoyYMCAHH744T3er7m5OR0dHUmSjo6O2gcBv6mpqak25p0WLVqUa665phf3EAD2jfXr1+fII4+s9zSKt+uMPwDoa95vre8zYX/JJZfkqaeeysqVK3ts33V6fZKMHTs2xx9/fEaNGpUf/vCHOeecc97z/arVao9P29/tk/d3jvlNV155ZebPn1973tnZmY985CNZv359hgwZ8lvvFwDsK11dXRk5cmQGDx5c76kcEHb9O1rrAegrftu1vk+E/dy5c/ODH/wgDz/88PsecRgxYkRGjRqV559/PknS0tKSbdu2ZdOmTT2O2m/cuDGTJ0+ujXnllVd2e69XX301zc3N7/r3NDQ0pKGhYbftQ4YMsdgD0Kc4bbx37Pp3tNYD0Ne831pf1wvyqtVqLrnkknzve9/LT37yk4wePfp9f+a1117L+vXrM2LEiCTJ+PHjc8ghh2T58uW1MRs2bMgzzzxTC/tJkyals7Mzjz/+eG3MY489ls7OztoYAAAAKFFdj9hffPHFufvuu3Pvvfdm8ODBtevdGxsbM2jQoGzZsiULFizIn/7pn2bEiBF54YUX8td//dcZPnx4Pv3pT9fGXnDBBbnssssybNiwDB06NJdffnnGjRuXM844I0lyzDHH5Mwzz8ycOXNy8803J0kuvPDCzJgxwx3xAQAAKFpdw/6mm25KkkyZMqXH9ttuuy3nn39++vXrl6effjrf+c53snnz5owYMSKnnnpqvvvd7/a4xuCGG25I//79c+6552br1q05/fTTc/vtt6dfv361MXfddVcuvfTS2t3zZ86cmSVLluz7nQQAAIB9qE99j31f1tXVlcbGxnR2drruDoA+wdrUu/x7AtDX/LZrky+9BQAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICC9a/3BA5247/0nXpPAfZozX/783pPAaBo1nr6Oms9lM8RewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcA9plFixblhBNOyODBg9PU1JSzzz47a9eu7TGmWq1mwYIFaW1tzaBBgzJlypQ8++yzPcZ0d3dn7ty5GT58eA477LDMnDkzL730Uo8xmzZtyuzZs9PY2JjGxsbMnj07mzdv3te7CAB1J+wBgH1mxYoVufjii7N69eosX748b7/9dqZOnZo33nijNubaa6/N9ddfnyVLluSJJ55IS0tLPvnJT+b111+vjZk3b16WLVuWe+65JytXrsyWLVsyY8aM7NixozZm1qxZaW9vT1tbW9ra2tLe3p7Zs2fv1/0FgHroX+8JAAAHrra2th7Pb7vttjQ1NWXNmjU5+eSTU61Wc+ONN+aqq67KOeeckyS544470tzcnLvvvjtf/OIX09nZmVtvvTV33nlnzjjjjCTJ0qVLM3LkyDzwwAOZNm1annvuubS1tWX16tWZMGFCkuSWW27JpEmTsnbt2hx99NH7d8cBYD9yxB4A2G86OzuTJEOHDk2SrFu3Lh0dHZk6dWptTENDQ0455ZSsWrUqSbJmzZps3769x5jW1taMHTu2NubRRx9NY2NjLeqTZOLEiWlsbKyNeafu7u50dXX1eABAiYQ9ALBfVKvVzJ8/P5/4xCcyduzYJElHR0eSpLm5ucfY5ubm2msdHR0ZMGBADj/88D2OaWpq2u3vbGpqqo15p0WLFtWux29sbMzIkSM/2A4CQJ0IewBgv7jkkkvy1FNP5e///u93e61SqfR4Xq1Wd9v2Tu8c827j9/Q+V155ZTo7O2uP9evX/za7AQB9jrAHAPa5uXPn5gc/+EF++tOf5sgjj6xtb2lpSZLdjqpv3LixdhS/paUl27Zty6ZNm/Y45pVXXtnt73311Vd3Oxtgl4aGhgwZMqTHAwBKJOwBgH2mWq3mkksuyfe+97385Cc/yejRo3u8Pnr06LS0tGT58uW1bdu2bcuKFSsyefLkJMn48eNzyCGH9BizYcOGPPPMM7UxkyZNSmdnZx5//PHamMceeyydnZ21MQBwoHJXfABgn7n44otz99135957783gwYNrR+YbGxszaNCgVCqVzJs3LwsXLsyYMWMyZsyYLFy4MIceemhmzZpVG3vBBRfksssuy7BhwzJ06NBcfvnlGTduXO0u+cccc0zOPPPMzJkzJzfffHOS5MILL8yMGTPcER+AA56wBwD2mZtuuilJMmXKlB7bb7vttpx//vlJkiuuuCJbt27NRRddlE2bNmXChAm5//77M3jw4Nr4G264If3798+5556brVu35vTTT8/tt9+efv361cbcddddufTSS2t3z585c2aWLFmyb3cQAPqAup6Kv2jRopxwwgkZPHhwmpqacvbZZ2ft2rU9xlSr1SxYsCCtra0ZNGhQpkyZkmeffbbHmO7u7sydOzfDhw/PYYcdlpkzZ+all17qMWbTpk2ZPXt27c63s2fPzubNm/f1LgLAQa1arb7rY1fUJ7++6d2CBQuyYcOGvPXWW1mxYkXtrvm7DBw4MIsXL85rr72WN998M/fdd99ud7EfOnRoli5dWvvquqVLl+bDH/7wfthLAKivuob9ihUrcvHFF2f16tVZvnx53n777UydOjVvvPFGbcy1116b66+/PkuWLMkTTzyRlpaWfPKTn8zrr79eGzNv3rwsW7Ys99xzT1auXJktW7ZkxowZ2bFjR23MrFmz0t7enra2trS1taW9vT2zZ8/er/sLAAAAva2up+K3tbX1eH7bbbelqakpa9asycknn5xqtZobb7wxV111Vc4555wkyR133JHm5ubcfffd+eIXv5jOzs7ceuutufPOO2vX2S1dujQjR47MAw88kGnTpuW5555LW1tbVq9enQkTJiRJbrnllkyaNClr16517R0AAADF6lN3xe/s7Ezy61PpkmTdunXp6OioXSuX/PqraU455ZSsWrUqSbJmzZps3769x5jW1taMHTu2NubRRx9NY2NjLeqTZOLEiWlsbKyNeafu7u7aqXy7HgAAANDX9Jmwr1armT9/fj7xiU/Urqvbdefcd37/bHNzc+21jo6ODBgwIIcffvgexzQ1Ne32dzY1Ne32vbm7LFq0qHY9fmNj427X8QEAAEBf0GfC/pJLLslTTz2Vv//7v9/ttUql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r06/fv3y9NNP50/+5E9y1FFH5bzzzstRRx2VRx99NIMHD669xw033JCzzz475557bk488cQceuihue+++9KvX7/amLvuuivjxo3L1KlTM3Xq1PyH//Afcuedd+73/QWAeqjrzfN8ty0AHNimTJmSarX6nq//+Mc/ft/3GDhwYBYvXpzFixe/55ihQ4dm6dKlezVHAChdn7/G3nfbAgAAwHvr02Hvu20BAABgz/r099j7blsAAADYsz59xP6dfLctAAAA9FRU2PtuWwAAAOiprqfib9myJT//+c9rz3d9t+3QoUMzdOjQLFiwIH/6p3+aESNG5IUXXshf//Vfv+d32w4bNixDhw7N5Zdf/p7fbXvzzTcnSS688ELfbQsAAMABoa5h/7Of/Synnnpq7fmua9rPO++83HTTTXn66afzne98J5s3b86IESNy6qmn5rvf/e5u323bv3//nHvuudm6dWtOP/303H777bt9t+2ll15au3v+zJkzs2TJkv20lwAAALDv1DXsfbctAAAAfDBFXWMPAAAA9CTsAQAAoGDCHgAAAAom7AEAAKBgwh4AAAAKJuwBAACgYMIeAAAACibsAQAAoGDCHgAAAAom7AEAAKBgwh4AAAAKJuwBAACgYMIeAAAACibsAQAAoGDCHgAAAAom7AEAAKBgwh4AAAAKJuwBAACgYMIeAAAACibsAQAAoGDCHgAAAAom7AEAAKBgexX2p512WjZv3rzb9q6urpx22mkfdE4AQJ1Z6wGgHHsV9g899FC2bdu22/a33norjzzyyAeeFABQX9Z6AChH/99l8FNPPVX78//+3/87HR0dtec7duxIW1tb/t2/+3e9NzsAYL+y1gNAeX6nsP/4xz+eSqWSSqXyrqfhDRo0KIsXL+61yQEA+5e1HgDK8zuF/bp161KtVvPRj340jz/+eI444ojaawMGDEhTU1P69evX65MEAPYPaz0AlOd3CvtRo0YlSXbu3LlPJgMA1Je1HgDK8zuF/W/6P//n/+Shhx7Kxo0bd1v8r7766g88MQCgvqz1AFCGvQr7W265JX/1V3+V4cOHp6WlJZVKpfZapVKx2ANA4az1AFCOvQr7r3/96/nGN76RL3/5y709HwCgD7DWA0A59up77Ddt2pTPfOYzvT0XAKCPsNYDQDn2Kuw/85nP5P777+/tuQAAfYS1HgDKsVen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O2tjAOBA1mevsXdDHQAo35YtW9Le3p729vYkv17f29vb8+KLL6ZSqWTevHlZuHBhli1blmeeeSbnn39+Dj300MyaNStJ0tjYmAsuuCCXXXZZHnzwwTz55JP5/Oc/n3HjxtXukn/MMcfkzDPPzJw5c7J69eqsXr06c+bMyYwZM9wRH4CDQp/9urs93VDn3/7t32pj9uUNda655poPtA8AcLD72c9+llNPPbX2fP78+UmS8847L7fffnuuuOKKbN26NRdddFE2bdqUCRMm5P7778/gwYNrP3PDDTekf//+Offcc7N169acfvrpuf3229OvX7/amLvuuiuXXnpp7cP+mTNnvuelfgBwoOmzYb9LPW+os+v/fCRJV1eXu+UCwO9oypQpqVar7/l6pVLJggULsmDBgvccM3DgwCxevDiLFy9+zzFDhw7N0qVLP8hUAaBYffZUfDfUAQAAgPfXZ8PeDXUAAADg/dX1VPwtW7bk5z//ee35rhvqDB06NB/5yEdqN9QZM2ZMxowZk4ULF77nDXWGDRuWoUOH5vLLL3/PG+rcfPPNSZILL7zQDXUAAAA4INQ17N1QBwAAAD6YSnVPd7ShpqurK42Njens7OzV6+3Hf+k7vfZesC+s+W9/Xu8pAO9hX61NBytrPQcraz30Xb/t2tRnr7EHAAAA3p+wBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwDqasGCBalUKj0eLS0ttder1WoWLFiQ1tbWDBo0KFOmTMmzzz7b4z26u7szd+7cDB8+PIcddlhmzpyZl156aX/vCgDUhbAHAOruj/7oj7Jhw4ba4+mnn669du211+b666/PkiVL8sQTT6SlpSWf/OQn8/rrr9fGzJs3L8uWLcs999yTlStXZsuWLZkxY0Z27NhRj90BgP2qf70nAADQv3//Hkfpd6lWq7nxxhtz1VVX5ZxzzkmS3HHHHWlubs7dd9+dL37xi+ns7Mytt96aO++8M2eccUaSZOnSpRk5cmQeeOCBTJs2bb/uCwDsb336iL1T8wDg4PD888+ntbU1o0ePzp/92Z/l//7f/5skWbduXTo6OjJ16tTa2IaGhpxyyilZtWpVkmTNmjXZvn17jzGtra0ZO3Zsbcy76e7uTldXV48HAJSoT4d94tQ8ADjQTZgwId/5znfy4x//OLfccks6OjoyefLkvPbaa+no6EiSNDc39/iZ5ubm2msdHR0ZMGBADj/88Pcc824WLVqUxsbG2mPkyJG9vGcAsH/0+VPx63VqXnd3d7q7u2vPfYoPAPvG9OnTa38eN25cJk2alN///d/PHXfckYkTJyZJKpVKj5+pVqu7bXun9xtz5ZVXZv78+bXnXV1d4h6AIvX5I/b1ODUv8Sk+ANTLYYcdlnHjxuX555+vfbj/ziPvGzdurB3Fb2lpybZt27Jp06b3HPNuGhoaMmTIkB4PAChRnw77ep2al/z6U/zOzs7aY/369b24ZwDAe+nu7s5zzz2XESNGZPTo0Wlpacny5ctrr2/bti0rVqzI5MmTkyTjx4/PIYcc0mPMhg0b8swzz9TGAMCBrE+fil+vU/OSX3+K39DQsJczBwB+W5dffnnOOuusfOQjH8nGjRvz9a9/PV1dXTnvvPNSqVQyb968LFy4MGPGjMmYMWOycOHCHHrooZk1a1aSpLGxMRdccEEuu+yyDBs2LEOHDs3ll1+ecePG1S7FA4ADWZ8O+3f6zVPzzj777CS/Pio/YsSI2pj3OjXvN4/ab9y40Sf4ANBHvPTSS/nc5z6XX/7ylzniiCMyceLErF69OqNGjUqSXHHFFdm6dWsuuuiibNq0KRMmTMj999+fwYMH197jhhtuSP/+/XPuuedm69atOf3003P77benX79+9dotANhv+vSp+O/k1DwAOPDcc889efnll7Nt27b8v//3//KP//iP+djHPlZ7vVKpZMGCBdmwYUPeeuutrFixImPHju3xHgMHDszixYvz2muv5c0338x9993n/jgAHDT69BF7p+YBAADAnvXpsHdqHgAAAOxZnw77e+65Z4+v7zo1b8GCBe85ZtepeYsXL+7l2QEAAED9FXWNPQAAANCTsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKJiwBwAAgIIJewAAACiYsAcAAICCCXsAAAAomLAHAACAggl7AAAAKFj/ek8AoDe8+LVx9Z4C7NFHrn663lMAAA5Qwh4AACiCD/Lp6+r1Qb5T8QEAAKBgwh4AAAAKJuwBAACgYMIeAAAACibsAQAAoGDCHgAAAAom7AEAAKBgwh4AAAAKJuwBAACgYMIeAAAACibsAQAAoGDCHgAAAAom7AEAAKBgwh4AAAAKdlCF/Te/+c2MHj06AwcOzPjx4/PII4/Ue0oAQC+y1gNwMDpowv673/1u5s2bl6uuuipPPvlkTjrppEyfPj0vvvhivacGAPQCaz0AB6uDJuyvv/76XHDBBfnCF76QY445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\n",
      "text/plain": [
       "<Figure size 1200x600 with 2 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "fig, ax = plt.subplots(1,2, figsize=(12,6))\n",
    "\n",
    "sns.countplot(ax=ax[0], data=data_raw[data_raw.Residence_type == 'Urban'], x='stroke')\n",
    "sns.countplot(ax=ax[1], data=data_raw[data_raw.Residence_type == 'Rural'], x='stroke')\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "6be582b1",
   "metadata": {},
   "source": [
    "Мы видим, что сильной разницы между наличием инсульта у двух разных подгрупп нет. Значит, мое начальное предположение о том, что жизнь в деревне сопуствует более активному образу жизни и, соотвественно, у таких людей меньше риск инсульта, был неверен."
   ]
  },
  {
   "cell_type": "markdown",
   "id": "4ef9e0be",
   "metadata": {},
   "source": [
    "## Зависимость от того, был ли человек женат или нет"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "id": "79240ac2",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 1200x600 with 2 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "fig, ax = plt.subplots(1,2, figsize=(12,6))\n",
    "\n",
    "sns.countplot(ax=ax[0], data=data_raw[data_raw.ever_married == 'Yes'], x='stroke')\n",
    "sns.countplot(ax=ax[1], data=data_raw[data_raw.ever_married == 'No'], x='stroke')\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "2b227f64",
   "metadata": {},
   "source": [
    "Мы видим, что вероятность инсульта у тех, кто был женат выше, чем у тех, кто не был. "
   ]
  },
  {
   "cell_type": "markdown",
   "id": "2836c0f0",
   "metadata": {},
   "source": [
    "## Зависимость от пола"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "id": "07ccfb99",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAA/YAAAIOCAYAAAASrpaUAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjUuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8qNh9FAAAACXBIWXMAAA9hAAAPYQGoP6dpAABFRklEQVR4nO39f5TV1X0v/j8n/BiQwokDzq+PE0patDZwjcGEHyYRhfAjRWq0QUNKtDVoq8LiAjElriaYlcCNWUZ74cZrXEZUMHpvb0i0WhSiYiziD1KqWEtJihVXGDFmmBFDBoLn+0eW59sRUIMDM295PNZ6rzXvvV/nffZmZdx5zvu896kql8vlAAAAAIX0nq4eAAAAAHDoBHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDAenb1AIritddey89//vP0798/VVVVXT0cAEi5XM4rr7ySxsbGvOc9/lb/TlnrAehu3vZaX+Zt2bZtWzmJw+FwOBzd7ti2bVtXL5MHtWjRovKpp55a/r3f+73ycccdV/7TP/3T8r/92791qHnttdfKX/nKV8oNDQ3lPn36lE8//fTypk2bOtT8+te/Ll9++eXlgQMHlo855pjyWWedtd+8f/nLX5b//M//vDxgwIDygAEDyn/+539ebmlpedtjtdY7HA6Ho7seb7XWV5XL5XJ4S62trXnve9+bbdu2ZcCAAV09HABIW1tbmpqasnPnzpRKpa4ezgFNmjQp559/fj784Q/nN7/5Ta688so8/fTT+dd//df069cvSfKNb3wjX//617Ns2bKccMIJ+drXvpaHH344mzdvTv/+/ZMkf/3Xf5277747y5Yty8CBAzNv3rz88pe/zIYNG9KjR48kyeTJk/PCCy/kO9/5TpLk4osvzu///u/n7rvvfltjtdYD0N283bVesH+b2traUiqV0traarEHoFso4tr00ksvpba2NmvXrs3HP/7xlMvlNDY2Zs6cOfniF7+YJGlvb09dXV2+8Y1v5JJLLklra2uOO+643HbbbTnvvPOSJD//+c/T1NSUe++9NxMnTsyzzz6bP/7jP8769eszcuTIJMn69eszevTo/Nu//VtOPPHEtxxbEf89AXh3e7trkwfyAIAjprW1NUlSU1OTJNm6dWuam5szYcKESk11dXVO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woQJlbbGxsYMGzassmHOoWyqY0MdAHjndu3alY0bN2bjxo1Jkq1bt2bjxo15/vnnKzVtbW35v//3/x7wbv3PfvazfPWrX82TTz6Z5557Lvfee28+/elP55RTTslpp52WJDnppJMyadKkzJw5M+vXr8/69eszc+bMTJkyxR/vATgqdJtgXy6XM3fu3Hz0ox/NsGHDKu2TJ0/OihUr8sADD+Saa67JE088kTPPPDPt7e1JfrthTu/evXPsscd2uF5dXV1lw5xD2VRn8eLFlefxS6VSmpqaOmuqAHDUePLJJ3PKKafklFNOSZLMnTs3p5xySr785S9Xau64446Uy+V85jOf2e/1vXv3zo9+9KNMnDgxJ554YmbPnp0JEyZkzZo16dGjR6VuxYoVGT58eCZMmJAJEybkv/23/5bbbrvt8E8QALqBbrMr/uWXX56nnnoqjzzySIf28847r/LzsGHDcuqpp2bw4MG555579ts1979644Y5v+umOgsWLMjcuXMr521tbcI9APyOxo4dm3K5/KY1F198cS6++OID9jU1NWXt2rVv+T41NTVZvnz5IY0RAIquW9yxnzVrVu666648+OCDOf7449+0tqGhIYMHD+6wYc6ePXvS0tLSoW7Hjh2VDXMOZVMdG+oAAABQBF0a7Mvlci6//PJ8//vfzwMPPJAhQ4a85WtefvnlbNu2rbJhzogRI9KrV6/Kd9kmyfbt27Np06bKhjn/dVOd19lUBwAAgHeDLv0o/mWXXZbbb789P/zhD9O/f//K8+6lUil9+/bNrl27snDhwpx77rlpaGjIc889ly996UsZNGhQPvWpT1VqL7roosybNy8DBw5MTU1N5s+fn+HDh1d2yf+vm+rccMMNSX77sT+b6gAAAFB0XRrsr7/++iS/ff7uv7r55ptz4YUXpkePHnn66adz6623ZufOnWloaMgZZ5yRO++8M/3796/UX3vttenZs2emTZuW3bt3Z9y4cVm2bNl+m+q8vuFOkkydOjVLly49/JMEAACAw6hLg/1bbabTt2/f3HfffW95nT59+mTJkiVZsmTJQWtsqgMAAMC7UbfYPA8AAAA4NII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQ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8cX9rvXSSy+lrq7uoO9VXV2d6urqTp4BABRDV631AMDv7pCC/datWzt7HG/Lyy+/nG3btqWhoSFJMmLEiPTq1SurV6/OtGnTkiTbt2/Ppk2bcvXVVydJRo8endbW1jz++OP5yEc+kiR57LHH0traWgn/AEBHXbXWAwC/u0P+HvvOsGvXrvz0pz+tnG/dujUbN25MTU1NampqsnDhwpx77rlpaGjIc889ly996UsZNGhQPvWpTyVJSqVSLrroosybNy8DBw5MTU1N5s+fn+HDh1d2yT/ppJMyadKkzJw5MzfccEOS337d3ZQpU+yIDwAAQOEdUrD/y7/8yzft/+53v/u2rvPkk0/mjDPOqJy//kz7BRdckOuvvz5PP/10br311uzcuTMNDQ0544wzcuedd6Z///6V11x77bXp2bNnpk2blt27d2fcuHFZtmxZ5Tvsk2TFihWZPXt2Zff8qVOnZunSpW97vgBwtOmstf7hhx/ON7/5zWzYsCHbt2/PypUrc/bZZ1f6y+VyrrrqqnznO99JS0tLRo4cmf/1v/5XPvCBD1Rq2tvbM3/+/Hzve9+rrPXf/va3c/zxx1dqWlpaMnv27Nx1111JfrvWL1myJO9973vf/qQBoKAOKdi3tLR0ON+7d282bdqUnTt35swzz3zb1xk7dmzK5fJB+++77763vEafPn2yZMmSLFmy5KA1NTU1Wb58+dseFwAc7TprrX/11Vdz8skn5y/+4i9y7rnn7td/9dVX51vf+laWLVuWE044IV/72tfyiU98Ips3b678IX/OnDm5++67c8cdd2TgwIGZN29epkyZkg0bNlT+kD99+vS88MILWbVqVZLffjpvxowZufvuuw/1nwAACuOQgv3KlSv3a3vttddy6aWX5v3vf/87HhQA0LU6a62fPHlyJk+efMC+crmc6667LldeeWXl225uueWW1NXV5fbbb88ll1yS1tbW3HTTTbntttsqj9ktX748TU1NWbNmTSZOnJhnn302q1atyvr16zNy5MgkyY033pjRo0dn8+bNHr0D4F3vkL7H/oAXes978t//+3/Ptdde21mXBAC6kc5e67du3Zrm5ubKo3LJb7+V5vTTT8+6deuSJBs2bMjevXs71DQ2NmbYsGGVmkcffTSlUqkS6pNk1KhRKZVKlZoDaW9vT1tbW4cDAIqo04J9kvzsZz/Lb37zm868JADQjXTmWt/c3Jwk+339bF1dXaWvubk5vXv37vC1tgeqqa2t3e/6tbW1lZoDWbx4cUqlUuVoamp6R/MBgK5ySB/Ff32Tu9eVy+Vs374999xzTy644IJOGRgA0HWO5FpfVVW133u9se2N3lhzoPq3us6CBQs6zLOtrU24B6CQDinY//M//3OH8/e85z057rjjcs0117zlLroAQPd3JNb6+vr6JL+9497Q0FBp37FjR+Uufn19ffbs2ZOWlpYOd+137NiRMWPGVGpefPHF/a7/0ksv7fdpgP+quro61dXVnTIXAOhKhxTsH3zwwc4eBwDQjRyJtX7IkCGpr6/P6tWrc8oppyRJ9uzZk7Vr1+Yb3/hGkmTEiBHp1atXVq9enWnTpiVJtm/fnk2bNuXqq69OkowePTqtra15/PHH85GPfCRJ8thjj6W1tbUS/gHg3eyQgv3rXnrppWzevDlVVVU54YQTctxxx3XWuACAbuCdrvW7du3KT3/608r51q1bs3HjxtTU1OR973tf5syZk0WLFmXo0KEZOnRoFi1alGOOOSbTp09PkpRKpVx00UWZN29eBg4cmJqamsyfPz/Dhw+v7JJ/0kknZdKkSZk5c2ZuuOGGJL/9urspU6bYER+Ao8IhBftXX301s2bNyq233prXXnstSdKjR4987nOfy5IlS3LMMcd06iABgCOrs9b6J598MmeccUbl/PVn2i+44IIsW7YsV1xxRXbv3p1LL700LS0tGTlyZO6///7Kd9gnybXXXpuePXtm2rRp2b17d8aNG5dly5ZVvsM+SVasWJHZs2dXds+fOnVqli5d+o7/HQCgCKrK5XL5d33RJZdckjVr1mTp0qU57bTTkiSPPPJIZs+enU984hO5/vrrO32gXa2trS2lUimtra0ZMGBAp113xBdu7bRrweGw4Zuf6+ohAAdxuNamxFpvredoYq2H7uvtrk2HdMf+//2//5e///u/z9ixYyttn/zkJ9O3b99MmzbtXbnYA8DRxFoPAMVxSN9j/6tf/eqAu8zW1tbmV7/61TseFADQtaz1AFAchxTsR48ena985Sv59a9/XWnbvXt3rrrqqowePbrTBgcAdA1rPQAUxyF9FP+6667L5MmTc/zxx+fkk09OVVVVNm7cmOrq6tx///2dPUYA4Aiz1gNAcRxSsB8+fHi2bNmS5cuX59/+7d9SLpdz/vnn57Of/Wz69u3b2WMEAI4waz0AFMchBfvFixenrq4uM2fO7ND+3e9+Ny+99FK++MUvdsrgAICuYa0HgOI4pGfsb7jhhvzRH/3Rfu0f+MAH8r//9/9+x4MCALqWtR4AiuOQgn1zc3MaGhr2az/uuOOyffv2dzwoAKBrWesBoDgOKdg3NTXln/7pn/Zr/6d/+qc0Nja+40EBAF3LWg8AxXFIz9h//vOfz5w5c7J3796ceeaZSZIf/ehHueKKKzJv3rxOHSAAcORZ6wGgOA4p2F9xxRX55S9/mUsvvTR79uxJkvTp0ydf/OIXs2DBgk4dIABw5FnrAaA4DinYV1VV5Rvf+Eb+9m//Ns8++2z69u2boUOHprq6urPHBwB0AWs9ABTHIQX71/3e7/1ePvzhD3fWWACAbsZaDwDd3yFtngcAAAB0D4I9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9ANClfv/3fz9VVVX7HZdddlmS5MILL9yvb9SoUR2u0d7enlmzZmXQoEHp169fpk6dmhdeeKErpgMAR5xgDwB0qSeeeCLbt2+vHKtXr06SfPrTn67UTJo0qUPNvffe2+Eac+bMycqVK3PHHXfkkUceya5duzJlypTs27fviM4FALpCz64eAABwdDvuuOM6nP+P//E/8gd/8Ac5/fTTK23V1dWpr68/4OtbW1tz00035bbbbsv48eOTJMuXL09TU1PWrFmTiRMnHr7BA0A34I49ANBt7NmzJ8uXL89f/uVfpqqqqtL+0EMPpba2NieccEJmzpyZHTt2VPo2bNiQvXv3ZsKECZW2xsbGDBs2LOvWrTvoe7W3t6etra3DAQBFJNgDAN3GD37wg+zcuTMXXnhhpW3y5MlZsWJFHnjggVxzzTV54okncuaZZ6a9vT1J0tzcnN69e+fYY4/tcK26uro0Nzcf9L0WL16cUqlUOZqamg7LnADgcPNRfACg27jpppsyefLkNDY2VtrOO++8ys/Dhg3LqaeemsGDB+eee+7JOeecc9BrlcvlDnf932jBggWZO3du5bytrU24B6CQBHsAoFv4z//8z6xZsybf//7337SuoaEhgwcPzpYtW5Ik9fX12bNnT1paWjrctd+xY0fGjBlz0OtUV1enurq6cwYPAF3IR/EBgG7h5ptvTm1tbf7kT/7kTetefvnlbNu2LQ0NDUmSESNGpFevXpXd9JNk+/bt2bRp05sGewB4t3DHHgDocq+99lpuvvnmXHDBBenZ8///f0927dqVhQsX5txzz01DQ0Oee+65fOlLX8qgQYPyqU99KklSKpVy0UUXZd68eRk4cGBqamoyf/78DB8+vLJLPgC8mwn2AECXW7NmTZ5//vn85V/+ZYf2Hj165Omnn86tt96anTt3pqGhIWeccUbuvPPO9O/fv1J37bXXpmfPnpk2bVp2796dcePGZdmyZenRo8eRngoAHHGCPQDQ5SZMmJByubxfe9++fXPfffe95ev79OmTJUuWZMmSJYdjeADQrXnGHgAAAApMsAcAAIAC69Jg//DDD+ess85KY2Njqqqq8oMf/KBDf7lczsKFC9PY2Ji+fftm7NixeeaZZzrUtLe3Z9asWRk0aFD69euXqVOn5oUXXuhQ09LSkhkzZqRUKqVUKmXGjBnZuXPnYZ4dAAAAHH5dGuxfffXVnHzyyVm6dOkB+6+++up861vfytKlS/PEE0+kvr4+n/jEJ/LKK69UaubMmZOVK1fmjjvuyCOPPJJdu3ZlypQp2bdvX6Vm+vTp2bhxY1atWpVVq1Zl48aNmTFjxmGfHwAAABxuXbp53uTJkzN58uQD9pXL5Vx33XW58sorc8455yRJbrnlltTV1eX222/PJZdcktbW1tx000257bbbKl9ns3z58jQ1NWXNmjWZOHFinn322axatSrr16/PyJEjkyQ33nhjRo8enc2bN+fEE088MpMFAACAw6DbPmO/devWNDc3Z8KECZW26urqnH766Vm3bl2SZMOGDdm7d2+HmsbGxgwbNqxS8+ijj6ZUKlVCfZKMGjUqpVKpUnMg7e3taWtr63AAAABAd9Ntg31zc3OSpK6urkN7XV1dpa+5uTm9e/fOscce+6Y1tbW1+12/tra2UnMgixcvrjyTXyqV0tTU9I7mAwAAAIdDtw32r6uqqupwXi6X92t7ozfWHKj+ra6zYMGCtLa2Vo5t27b9jiMHAACAw6/bBvv6+vok2e+u+o4dOyp38evr67Nnz560tLS8ac2LL7643/Vfeuml/T4N8F9VV1dnwIABHQ4AAADobrptsB8yZEjq6+uzevXqStuePXuydu3ajBkzJkkyYsSI9OrVq0PN9u3bs2nTpkrN6NGj09ramscff7xS89hjj6W1tbVSAwAAAEXVpbvi79q1Kz/96U8r51u3bs3GjRtTU1OT973vfZkzZ04WLVqUoUOHZujQoVm0aFGOOeaYTJ8+PUlSKpVy0UUXZd68eRk4cGBqamoyf/78DB8+vLJL/kknnZRJkyZl5syZueGGG5IkF198caZMmWJHfAAAAAqvS4P9k08+mTPOOKNyPnfu3CTJBRdckGXLluWKK67I7t27c+mll6alpSUjR47M/fffn/79+1dec+2116Znz56ZNm1adu/enXHjxmXZsmXp0aNHpWbFihWZPXt2Zff8qVOnZunSpUdolgAAAHD4VJXL5XJXD6II2traUiqV0tra2qnP24/4wq2ddi04HDZ883NdPQTgIA7X2nS0stZztLLWQ/f1dtembvuMPQAAAPDWBHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAoEstXLgwVVVVHY76+vpKf7lczsKFC9PY2Ji+fftm7NixeeaZZzpco729PbNmzcqgQYPSr1+/TJ06NS+88MKRngoAdAnBHgDoch/4wAeyffv2yvH0009X+q6++up861vfytKlS/PEE0+kvr4+n/jEJ/LKK69UaubMmZOVK1fmjjvuyCOPPJJdu3ZlypQp2bdvX1dMBwCOqJ5dPQAAgJ49e3a4S/+6crmc6667LldeeWXOOeecJMktt9ySurq63H777bnkkkvS2tqam266KbfddlvGjx+fJFm+fHmampqyZs2aTJw48YjOBQCONHfsAYAut2XLljQ2NmbIkCE5//zz8x//8R9Jkq1bt6a5uTkTJkyo1FZXV+f000/PunXrkiQbNmzI3r17O9Q0NjZm2LBhlZoDaW9vT1tbW4cDAIpIsAcAutTIkSNz66235r777suNN96Y5ubmjBkzJi+//HKam5uTJHV1dR1eU1dXV+lrbm5O7969c+yxxx605kAWL16cUqlUOZqamjp5ZgBwZAj2AECXmjx5cs4999wMHz4848ePzz333JPktx+5f11VVVWH15TL5f3a3uitahYsWJDW1tbKsW3btncwCwDoOoI9ANCt9OvXL8OHD8+WLVsqz92/8c77jh07Knfx6+vrs2fPnrS0tBy05kCqq6szYMCADgcAFJFgDwB0K+3t7Xn22WfT0NCQIUOGpL6+PqtXr67079mzJ2vXrs2YMWOSJCNGjEivXr061Gzfvj2bNm2q1ADAu5ld8QGALjV//vycddZZed/73pcdO3bka1/7Wtra2nLBBRekqqoqc+bMyaJFizJ06NAMHTo0ixYtyjHHHJPp06cnSUqlUi666KLMmzcvAwcOTE1NTebPn1/5aD8AvNsJ9gBAl3rhhRfymc98Jr/4xS9y3HHHZdSoUVm/fn0GDx6cJLniiiuye/fuXHrppWlpacnIkSNz//33p3///pVrXHvttenZs2emTZuW3bt3Z9y4cVm2bFl69OjRVdMCgCNGsAcAutQdd9zxpv1VVVVZuHBhFi5ceNCaPn36ZMmSJVmyZEknjw4Auj/P2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBdetgv3DhwlRVVXU46uvrK/3lcjkLFy5MY2Nj+vbtm7Fjx+aZZ57pcI329vbMmjUrgwYNSr9+/TJ16tS88MILR3oqAAAAcFh062CfJB/4wAeyffv2yvH0009X+q6++up861vfytKlS/PEE0+kvr4+n/jEJ/LKK69UaubMmZOVK1fmjjvuyCOPPJJdu3ZlypQp2bdvX1dMBwAAADpVz64ewFvp2bNnh7v0ryuXy7nuuuty5ZVX5pxzzkmS3HLLLamrq8vtt9+eSy65JK2trbnpppty2223Zfz48UmS5cuXp6mpKWvWrMnEiROP6FwAAACgs3X7O/ZbtmxJY2NjhgwZkvPPPz//8R//kSTZunVrmpubM2HChEptdXV1Tj/99Kxbty5JsmHDhuzdu7dDTWNjY4YNG1apOZj29va0tbV1OAAAAKC76dbBfuTIkbn11ltz33335cYbb0xzc3PGjBmTl19+Oc3NzUmSurq6Dq+pq6ur9DU3N6d379459thjD1pzMIsXL06pVKocTU1NnTgzAAAA6BzdOthPnjw55557boYPH57x48fnnnvuSfLbj9y/rqqqqsNryuXyfm1v9HZqFixYkNbW1sqxbdu2Q5wFAAAAHD7dOti/Ub9+/TJ8+PBs2bKl8tz9G++879ixo3IXv76+Pnv27ElLS8tBaw6muro6AwYM6HAAAABAd1OoYN/e3p5nn302DQ0NGTJkSOrr67N69epK/549e7J27dqMGTMmSTJixIj06tWrQ8327duzadOmSg0AAAAUWbfeFX/+/Pk566yz8r73vS87duzI1772tbS1teWCCy5IVVVV5syZk0WLFmXo0KEZOnRoFi1alGOOOSbTp09PkpRKpVx00UWZN29eBg4cmJqamsyfP7/y0X4AAAAoum4d7F944YV85jOfyS9+8Yscd9xxGTVqVNavX5/BgwcnSa644ors3r07l156aVpaWjJy5Mjcf//96d+/f+Ua1157bXr27Jlp06Zl9+7dGTduXJYtW5YePXp01bQAAACg03TrYH/HHXe8aX9VVVUWLlyYhQsXHrSmT58+WbJkSZYsWdLJowMAAICuV6hn7AEAAICOBHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwC61OLFi/PhD384/fv3T21tbc4+++xs3ry5Q82FF16YqqqqDseoUaM61LS3t2fWrFkZNGhQ+vXrl6lTp+aFF144klMBgC4h2AMAXWrt2rW57LLLsn79+qxevTq/+c1vMmHChLz66qsd6iZNmpTt27dXjnvvvbdD/5w5c7Jy5crccccdeeSRR7Jr165MmTIl+/btO5LTAYAjrmdXDwAAOLqtWrWqw/nNN9+c2trabNiwIR//+Mcr7dXV1amvrz/gNVpbW3PTTTfltttuy/jx45Mky5cvT1NTU9asWZOJEyfu95r29va0t7dXztva2jpjOgBwxLljDwB0K62trUmSmpqaDu0PPfRQamtrc8IJJ2TmzJnZsWNHpW/Dhg3Zu3dvJkyYUGlrbGzMsGHDsm7dugO+z+LFi1MqlSpHU1PTYZgNABx+gj0A0G2Uy+XMnTs3H/3oRzNs2LBK++TJk7NixYo88MADueaaa/LEE0/kzDPPrNxxb25uTu/evXPsscd2uF5dXV2am5sP+F4LFixIa2tr5di2bdvhmxgAHEY+ig8AdBuXX355nnrqqTzyyCMd2s8777zKz8OGDcupp56awYMH55577sk555xz0OuVy+VUVVUdsK+6ujrV1dWdM3AA6ELu2AMA3cKsWbNy11135cEHH8zxxx//prUNDQ0ZPHhwtmzZkiSpr6/Pnj170tLS0qFux44dqaurO2xjBoDuQLAHALpUuVzO5Zdfnu9///t54IEHMmTIkLd8zcsvv5xt27aloaEhSTJixIj06tUrq1evrtRs3749mzZtypgxYw7b2AGgO/BRfACgS1122WW5/fbb88Mf/jD9+/evPBNfKpXSt2/f7Nq1KwsXLsy5556bhoaGPPfcc/nSl76UQYMG5VOf+lSl9qKLLsq8efMycODA1NTUZP78+Rk+fHhll3wAeLcS7AGALnX99dcnScaOHduh/eabb86FF16YHj165Omnn86tt96anTt3pqGhIWeccUbuvPPO9O/fv1J/7bXXpmfPnpk2bVp2796dcePGZdmyZenRo8eRnA4AHHGCPQDQpcrl8pv29+3bN/fdd99bXqdPnz5ZsmRJlixZ0llDA4BC8Iw9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFJhgDwAAAAUm2AMAAECBCfYAAABQYII9AAAAFFjPrh4AAADA2/H8V4d39RDgTb3vy093yfu6Yw8AAAAF5o498K7gL/h0d131F3wA4N3PHXsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACuyoCvbf/va3M2TIkPTp0ycjRozIj3/8464eEgDQiaz1AByNjppgf+edd2bOnDm58sor88///M/52Mc+lsmTJ+f555/v6qEBAJ3AWg/A0eqoCfbf+ta3ctFFF+Xzn/98TjrppFx33XVpamrK9ddf39VDAwA6gbUegKNVz64ewJGwZ8+ebNiwIX/zN3/ToX3ChAlZt27dAV/T3t6e9vb2ynlra2uSpK2trVPHtq99d6deDzpbZ/9v/nB55df7unoI8KYOx+/S69csl8udfu2isdbDoSvKWp9Y7+n+Ovv36e2u9UdFsP/FL36Rffv2pa6urkN7XV1dmpubD/iaxYsX56qrrtqvvamp6bCMEbqr0pK/6uohwLvD4tJhu/Qrr7ySUunwXb8IrPVw6Kz10IkO03r/Vmv9URHsX1dVVdXhvFwu79f2ugULFmTu3LmV89deey2//OUvM3DgwIO+hq7V1taWpqambNu2LQMGDOjq4UCh+X0qhnK5nFdeeSWNjY1dPZRuw1r/7ue/T9A5/C4Vw9td64+KYD9o0KD06NFjv7/Y79ixY7+/7L+uuro61dXVHdre+973Hq4h0okGDBjgP07QSfw+dX9H+53611nrjz7++wSdw+9S9/d21vqjYvO83r17Z8SIEVm9enWH9tWrV2fMmDFdNCoAoLNY6wE4mh0Vd+yTZO7cuZkxY0ZOPfXUjB49Ot/5znfy/PPP56/+yjNFAPBuYK0H4Gh11AT78847Ly+//HK++tWvZvv27Rk2bFjuvffeDB48uKuHRieprq7OV77ylf0+Vgn87vw+UUTW+qOD/z5B5/C79O5SVfYdOQAAAFBYR8Uz9gAAAPBuJdgDAABAgQn2AAAAUGCCPQAAABSYYM+7xre//e0MGTIkffr0yYgRI/LjH/+4q4cEhfPwww/nrLPOSmNjY6qqqvKDH/ygq4cEUGGth3fOWv/uJNjzrnDnnXdmzpw5ufLKK/PP//zP+djHPpbJkyfn+eef7+qhQaG8+uqrOfnkk7N06dKuHgpAB9Z66BzW+ncnX3fHu8LIkSPzoQ99KNdff32l7aSTTsrZZ5+dxYsXd+HIoLiqqqqycuXKnH322V09FABrPRwG1vp3D3fsKbw9e/Zkw4YNmTBhQof2CRMmZN26dV00KgCgs1jrAd6cYE/h/eIXv8i+fftSV1fXob2uri7Nzc1dNCoAoLNY6wHenGDPu0ZVVVWH83K5vF8bAFBc1nqAAxPsKbxBgwalR48e+/3FfseOHfv9ZR8AKB5rPcCbE+wpvN69e2fEiBFZvXp1h/bVq1dnzJgxXTQqAKCzWOsB3lzPrh4AdIa5c+dmxowZOfXUUzN69Oh85zvfyfPPP5+/+qu/6uqhQaHs2rUrP/3pTyvnW7duzcaNG1NTU5P3ve99XTgy4GhnrYfOYa1/d/J1d7xrfPvb387VV1+d7du3Z9iwYbn22mvz8Y9/vKuHBYXy0EMP5Ywzztiv/YILLsiyZcuO/IAA/gtrPbxz1vp3J8EeAAAACswz9gAAAFBggj0AAAAUmGAPAAAABSbYAwAAQIEJ9gAAAFBggj0AAAAUmGAPAAAABSbYAwAAQIEJ9kC38Nxzz6WqqiobN27s6qEAAIeJ9R4OD8EeOGQXXnhhzj777K4eBgBwGFnvofsT7IHDbu/evV09BADgMLPeQ9cR7IG39Pd///cZPnx4+vbtm4EDB2b8+PH5whe+kFtuuSU//OEPU1VVlaqqqjz00EOVj9j9n//zfzJ27Nj06dMny5cvz2uvvZavfvWrOf7441NdXZ0PfvCDWbVq1UHf87XXXsvMmTNzwgkn5D//8z+TJHfffXdGjBiRPn365P3vf3+uuuqq/OY3vzlS/wwA8K5mvYfi6tnVAwC6t+3bt+czn/lMrr766nzqU5/KK6+8kh//+Mf53Oc+l+effz5tbW25+eabkyQ1NTX5+c9/niT54he/mGuuuSY333xzqqur83d/93e55pprcsMNN+SUU07Jd7/73UydOjXPPPNMhg4d2uE99+zZk+nTp+dnP/tZHnnkkdTW1ua+++7Ln//5n+d//s//mY997GP52c9+losvvjhJ8pWvfOXI/qMAwLuM9R4KrgzwJjZs2FBOUn7uuef267vgggvKf/qnf9qhbevWreUk5euuu65De2NjY/nrX/96h7YPf/jD5UsvvbTD63784x+Xx48fXz7ttNPKO3furNR+7GMfKy9atKjD62+77bZyQ0PDO5keAFC23kPRuWMPvKmTTz4548aNy/DhwzNx4sRMmDAhf/Znf5Zjjz32TV936qmnVn5ua2vLz3/+85x22mkdak477bT8y7/8S4e2z3zmMzn++OPzox/9KMccc0ylfcOGDXniiSfy9a9/vdK2b9++/PrXv86vfvWrDrUAwO/Geg/F5hl74E316NEjq1evzj/+4z/mj//4j7NkyZKceOKJ2bp165u+rl+/fvu1VVVVdTgvl8v7tX3yk5/MU089lfXr13dof+2113LVVVdl48aNlePpp5/Oli1b0qdPn0OcHQCQWO+h6NyxB95SVVVVTjvttJx22mn58pe/nMGDB2flypXp3bt39u3b95avHzBgQBobG/PII4/k4x//eKV93bp1+chHPtKh9q//+q8zbNiwTJ06Nffcc09OP/30JMmHPvShbN68OX/4h3/YuZMDAJJY76HIBHvgTT322GP50Y9+lAkTJqS2tjaPPfZYXnrppZx00kn59a9/nfvuuy+bN2/OwIEDUyqVDnqdL3zhC/nKV76SP/iDP8gHP/jB3Hzzzdm4cWNWrFixX+2sWbOyb9++TJkyJf/4j/+Yj370o/nyl7+cKVOmpKmpKZ/+9Kfznve8J0899VSefvrpfO1rXzuc/wQA8K5nvYdiE+yBNzVgwIA8/PDDue6669LW1pbBgwfnmmuuyeTJk3PqqafmoYceyqmnnppdu3blwQcfzO///u8f8DqzZ89OW1tb5s2blx07duSP//iPc9ddd+23Q+7r5syZk9deey2f/OQns2rVqkycODH/8A//kK9+9au5+uqr06tXr/zRH/1RPv/5zx/G2QPA0cF6D8VWVS6Xy109CAAAAODQ2DwPAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDABHsAAAAoMMEeAAAACkywBwAAgAIT7AEAAKDA/n/s3ZmvvBAIBAAAAABJRU5ErkJggg==\n",
      "text/plain": [
       "<Figure size 1200x600 with 2 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "fig, ax = plt.subplots(1,2, figsize=(12,6))\n",
    "\n",
    "sns.countplot(ax=ax[0], data=data_raw[data_raw.gender == 'Female'], x='stroke')\n",
    "sns.countplot(ax=ax[1], data=data_raw[data_raw.gender == 'Male'], x='stroke')\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "4bf98008",
   "metadata": {},
   "source": [
    "Здесь также мы не видим разницы между группами наличия инсульта у мужчин и женщин"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "63b099f9",
   "metadata": {},
   "source": [
    "## Зависимость от статуса курения"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "id": "aec03a6f",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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f94+fuLECfXt29dh7s9+9jP16NFDo0eP1ocffqiBAwdKkvr06aOLFy/q61//unNPDgAAAGgmCPhAM/fxxx/r0KFDSkpKUvv27fXxxx/rP//5j7p166Z79+7pwIEDunjxosLCwuyfl6/PnDlztHjxYj311FPq3bu3MjIydPr0aW3btq3O3OnTp6umpkYjR47Uvn379Nxzz2nRokUaOXKkoqOj9f3vf18tWrTQmTNndPbsWb322muuXAIAAADAFAj4QDMXEhKiY8eOafXq1SovL1dMTIxWrlyp5ORkxcfH68iRI4qPj9ft27d1+PBhPfnkk/UeZ8aMGSovL9esWbNUUlKi7t27a+/evXW+Qf8Lqampqq2t1YgRI7R//34NHz5cf/zjH7Vs2TKtWLFCAQEB6tq1qyZNmuTCswcAAADMg2/RBwAAAADABPiSPQAAAAAATICADwAAAACACRDwAQAAAAAwAQI+AAAAAAAmQMAHAAAAAMAECPgAAAAAAJgAAR8AAAAAABMg4AMAAAAAYAIEfAAAAAAATICADwAAAACACRDwAQAAAAAwAQI+AAAAAAAm8D8rxwGH4oIS/AAAAABJRU5ErkJggg==\n",
      "text/plain": [
       "<Figure size 1200x1200 with 4 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "fig, ax = plt.subplots(2,2, figsize=(12,12))\n",
    "\n",
    "sns.countplot(ax=ax[0,0], data=data_raw[data_raw.smoking_status == 'formerly smoked'], x='stroke')\n",
    "sns.countplot(ax=ax[0,1], data=data_raw[data_raw.smoking_status == 'never smoked'], x='stroke')\n",
    "sns.countplot(ax=ax[1,0], data=data_raw[data_raw.smoking_status == 'smokes'], x='stroke')\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "1f6279ad",
   "metadata": {},
   "source": [
    "Опять же здесь разницы между лидьми с разными статусами курения мы не видим разницы"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "c689171e",
   "metadata": {},
   "source": [
    "# 4. Обработка категориальных признаков"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "39882072",
   "metadata": {},
   "source": [
    "## Обработка бинарных признаков"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "id": "3d59e683",
   "metadata": {},
   "outputs": [],
   "source": [
    "data_raw['ever_married'] = pd.factorize(data_raw['ever_married'])[0]\n",
    "data_raw['Residence_type'] = pd.factorize(data_raw['Residence_type'])[0]\n",
    "data_raw['heart_disease'] = pd.factorize(data_raw['heart_disease'])[0]\n",
    "data_raw['hypertension'] = pd.factorize(data_raw['hypertension'])[0]\n",
    "data_raw['gender'] = pd.factorize(data_raw['gender'])[0]"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "c811e537",
   "metadata": {},
   "source": [
    "## Обработка небинарных признаков"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "dc3b918d",
   "metadata": {},
   "source": [
    "Признаки 'work_type' и 'smoking_status' являются небинарными. Чтобы создать фиктивные переменные для переменной в кадре данных pandas, мы можем использовать функцию pandas.get_dummies()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "id": "67d65e1b",
   "metadata": {},
   "outputs": [],
   "source": [
    "Work_dummies = pd.get_dummies(data_raw['work_type']) # создаем фиктивные переменные \n",
    "Smoking_dummies = pd.get_dummies(data_raw['smoking_status'])\n",
    "\n",
    "data_raw = pd.concat((data_raw, Work_dummies), axis=1) # объединяем созданные фиктивные переменные\n",
    "data_raw = data_raw.drop(['work_type'], axis=1) # отбрасываем первый столбец фиктивной переменной\n",
    "data_raw = pd.concat((data_raw, Smoking_dummies), axis=1)\n",
    "data_raw = data_raw.drop(['smoking_status'], axis=1)\n",
    "# аналогично можно было сделать в одну строчку data_raw = pd.get_dummies(data_raw, columns=['work_type', 'smoking_status',], drop_first=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "id": "86cbdfb5",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>gender</th>\n",
       "      <th>age</th>\n",
       "      <th>hypertension</th>\n",
       "      <th>heart_disease</th>\n",
       "      <th>ever_married</th>\n",
       "      <th>Residence_type</th>\n",
       "      <th>avg_glucose_level</th>\n",
       "      <th>bmi</th>\n",
       "      <th>stroke</th>\n",
       "      <th>Govt_job</th>\n",
       "      <th>Never_worked</th>\n",
       "      <th>Private</th>\n",
       "      <th>Self-employed</th>\n",
       "      <th>children</th>\n",
       "      <th>Unknown</th>\n",
       "      <th>formerly smoked</th>\n",
       "      <th>never smoked</th>\n",
       "      <th>smokes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>0</td>\n",
       "      <td>67.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>228.69</td>\n",
       "      <td>36.6</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>0</td>\n",
       "      <td>80.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>105.92</td>\n",
       "      <td>32.5</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1</td>\n",
       "      <td>49.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>171.23</td>\n",
       "      <td>34.4</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>1</td>\n",
       "      <td>79.0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>174.12</td>\n",
       "      <td>24.0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>0</td>\n",
       "      <td>81.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>186.21</td>\n",
       "      <td>29.0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5104</th>\n",
       "      <td>1</td>\n",
       "      <td>13.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>103.08</td>\n",
       "      <td>18.6</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5106</th>\n",
       "      <td>1</td>\n",
       "      <td>81.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>125.20</td>\n",
       "      <td>40.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5107</th>\n",
       "      <td>1</td>\n",
       "      <td>35.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>82.99</td>\n",
       "      <td>30.6</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5108</th>\n",
       "      <td>0</td>\n",
       "      <td>51.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>166.29</td>\n",
       "      <td>25.6</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5109</th>\n",
       "      <td>1</td>\n",
       "      <td>44.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>85.28</td>\n",
       "      <td>26.2</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>4907 rows × 18 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "      gender   age  hypertension  heart_disease  ever_married  Residence_type  \\\n",
       "0          0  67.0             0              0             0               0   \n",
       "2          0  80.0             0              0             0               1   \n",
       "3          1  49.0             0              1             0               0   \n",
       "4          1  79.0             1              1             0               1   \n",
       "5          0  81.0             0              1             0               0   \n",
       "...      ...   ...           ...            ...           ...             ...   \n",
       "5104       1  13.0             0              1             1               1   \n",
       "5106       1  81.0             0              1             0               0   \n",
       "5107       1  35.0             0              1             0               1   \n",
       "5108       0  51.0             0              1             0               1   \n",
       "5109       1  44.0             0              1             0               0   \n",
       "\n",
       "      avg_glucose_level   bmi stroke  Govt_job  Never_worked  Private  \\\n",
       "0                228.69  36.6      1         0             0        1   \n",
       "2                105.92  32.5      1         0             0        1   \n",
       "3                171.23  34.4      1         0             0        1   \n",
       "4                174.12  24.0      1         0             0        0   \n",
       "5                186.21  29.0      1         0             0        1   \n",
       "...                 ...   ...    ...       ...           ...      ...   \n",
       "5104             103.08  18.6      0         0             0        0   \n",
       "5106             125.20  40.0      0         0             0        0   \n",
       "5107              82.99  30.6      0         0             0        0   \n",
       "5108             166.29  25.6      0         0             0        1   \n",
       "5109              85.28  26.2      0         1             0        0   \n",
       "\n",
       "      Self-employed  children  Unknown  formerly smoked  never smoked  smokes  \n",
       "0                 0         0        0                1             0       0  \n",
       "2                 0         0        0                0             1       0  \n",
       "3                 0         0        0                0             0       1  \n",
       "4                 1         0        0                0             1       0  \n",
       "5                 0         0        0                1             0       0  \n",
       "...             ...       ...      ...              ...           ...     ...  \n",
       "5104              0         1        1                0             0       0  \n",
       "5106              1         0        0                0             1       0  \n",
       "5107              1         0        0                0             1       0  \n",
       "5108              0         0        0                1             0       0  \n",
       "5109              0         0        1                0             0       0  \n",
       "\n",
       "[4907 rows x 18 columns]"
      ]
     },
     "execution_count": 30,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data_raw"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "2c01c453",
   "metadata": {},
   "source": [
    "Видим, что в таблице появились новые столбцы с фиктивными переменными."
   ]
  },
  {
   "cell_type": "markdown",
   "id": "05e16b05",
   "metadata": {},
   "source": [
    "# 5. Нормализация "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "id": "4d1cc97c",
   "metadata": {},
   "outputs": [],
   "source": [
    "y = data_raw['stroke']\n",
    "data_raw = data_raw.drop(['stroke'], axis = 1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 32,
   "id": "1fc8b439",
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>gender</th>\n",
       "      <th>age</th>\n",
       "      <th>hypertension</th>\n",
       "      <th>heart_disease</th>\n",
       "      <th>ever_married</th>\n",
       "      <th>Residence_type</th>\n",
       "      <th>avg_glucose_level</th>\n",
       "      <th>bmi</th>\n",
       "      <th>Govt_job</th>\n",
       "      <th>Never_worked</th>\n",
       "      <th>Private</th>\n",
       "      <th>Self-employed</th>\n",
       "      <th>children</th>\n",
       "      <th>Unknown</th>\n",
       "      <th>formerly smoked</th>\n",
       "      <th>never smoked</th>\n",
       "      <th>smokes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>0</td>\n",
       "      <td>67.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>228.69</td>\n",
       "      <td>36.6</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>0</td>\n",
       "      <td>80.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>105.92</td>\n",
       "      <td>32.5</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1</td>\n",
       "      <td>49.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>171.23</td>\n",
       "      <td>34.4</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>1</td>\n",
       "      <td>79.0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>174.12</td>\n",
       "      <td>24.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>0</td>\n",
       "      <td>81.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>186.21</td>\n",
       "      <td>29.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5104</th>\n",
       "      <td>1</td>\n",
       "      <td>13.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>103.08</td>\n",
       "      <td>18.6</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5106</th>\n",
       "      <td>1</td>\n",
       "      <td>81.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>125.20</td>\n",
       "      <td>40.0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5107</th>\n",
       "      <td>1</td>\n",
       "      <td>35.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>82.99</td>\n",
       "      <td>30.6</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5108</th>\n",
       "      <td>0</td>\n",
       "      <td>51.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>166.29</td>\n",
       "      <td>25.6</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5109</th>\n",
       "      <td>1</td>\n",
       "      <td>44.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>85.28</td>\n",
       "      <td>26.2</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>4907 rows × 17 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "      gender   age  hypertension  heart_disease  ever_married  Residence_type  \\\n",
       "0          0  67.0             0              0             0               0   \n",
       "2          0  80.0             0              0             0               1   \n",
       "3          1  49.0             0              1             0               0   \n",
       "4          1  79.0             1              1             0               1   \n",
       "5          0  81.0             0              1             0               0   \n",
       "...      ...   ...           ...            ...           ...             ...   \n",
       "5104       1  13.0             0              1             1               1   \n",
       "5106       1  81.0             0              1             0               0   \n",
       "5107       1  35.0             0              1             0               1   \n",
       "5108       0  51.0             0              1             0               1   \n",
       "5109       1  44.0             0              1             0               0   \n",
       "\n",
       "      avg_glucose_level   bmi  Govt_job  Never_worked  Private  Self-employed  \\\n",
       "0                228.69  36.6         0             0        1              0   \n",
       "2                105.92  32.5         0             0        1              0   \n",
       "3                171.23  34.4         0             0        1              0   \n",
       "4                174.12  24.0         0             0        0              1   \n",
       "5                186.21  29.0         0             0        1              0   \n",
       "...                 ...   ...       ...           ...      ...            ...   \n",
       "5104             103.08  18.6         0             0        0              0   \n",
       "5106             125.20  40.0         0             0        0              1   \n",
       "5107              82.99  30.6         0             0        0              1   \n",
       "5108             166.29  25.6         0             0        1              0   \n",
       "5109              85.28  26.2         1             0        0              0   \n",
       "\n",
       "      children  Unknown  formerly smoked  never smoked  smokes  \n",
       "0            0        0                1             0       0  \n",
       "2            0        0                0             1       0  \n",
       "3            0        0                0             0       1  \n",
       "4            0        0                0             1       0  \n",
       "5            0        0                1             0       0  \n",
       "...        ...      ...              ...           ...     ...  \n",
       "5104         1        1                0             0       0  \n",
       "5106         0        0                0             1       0  \n",
       "5107         0        0                0             1       0  \n",
       "5108         0        0                1             0       0  \n",
       "5109         0        1                0             0       0  \n",
       "\n",
       "[4907 rows x 17 columns]"
      ]
     },
     "execution_count": 32,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data_raw"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "id": "9b176bc1",
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>gender</th>\n",
       "      <th>age</th>\n",
       "      <th>hypertension</th>\n",
       "      <th>heart_disease</th>\n",
       "      <th>ever_married</th>\n",
       "      <th>Residence_type</th>\n",
       "      <th>avg_glucose_level</th>\n",
       "      <th>bmi</th>\n",
       "      <th>Govt_job</th>\n",
       "      <th>Never_worked</th>\n",
       "      <th>Private</th>\n",
       "      <th>Self-employed</th>\n",
       "      <th>children</th>\n",
       "      <th>Unknown</th>\n",
       "      <th>formerly smoked</th>\n",
       "      <th>never smoked</th>\n",
       "      <th>smokes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "      <td>4.907000e+03</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>-6.176704e-16</td>\n",
       "      <td>-8.312885e-16</td>\n",
       "      <td>-6.857273e-16</td>\n",
       "      <td>3.216705e-15</td>\n",
       "      <td>-1.719929e-15</td>\n",
       "      <td>7.286475e-16</td>\n",
       "      <td>7.164049e-15</td>\n",
       "      <td>-1.886452e-15</td>\n",
       "      <td>9.466422e-17</td>\n",
       "      <td>5.653495e-17</td>\n",
       "      <td>-1.212263e-16</td>\n",
       "      <td>-4.691128e-16</td>\n",
       "      <td>7.943287e-16</td>\n",
       "      <td>1.113753e-15</td>\n",
       "      <td>2.409593e-18</td>\n",
       "      <td>-5.534146e-17</td>\n",
       "      <td>-6.488707e-16</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "      <td>1.000000e+00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>-1.199911e+00</td>\n",
       "      <td>-1.897377e+00</td>\n",
       "      <td>-3.181057e-01</td>\n",
       "      <td>-4.380583e+00</td>\n",
       "      <td>-7.289820e-01</td>\n",
       "      <td>-9.851319e-01</td>\n",
       "      <td>-1.129705e+00</td>\n",
       "      <td>-2.367153e+00</td>\n",
       "      <td>-3.837571e-01</td>\n",
       "      <td>-6.710190e-02</td>\n",
       "      <td>-1.157470e+00</td>\n",
       "      <td>-4.330384e-01</td>\n",
       "      <td>-3.976161e-01</td>\n",
       "      <td>-6.577329e-01</td>\n",
       "      <td>-4.531149e-01</td>\n",
       "      <td>-7.785215e-01</td>\n",
       "      <td>-4.203601e-01</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>-1.199911e+00</td>\n",
       "      <td>-7.925055e-01</td>\n",
       "      <td>-3.181057e-01</td>\n",
       "      <td>2.282336e-01</td>\n",
       "      <td>-7.289820e-01</td>\n",
       "      <td>-9.851319e-01</td>\n",
       "      <td>-6.355003e-01</td>\n",
       "      <td>-6.867097e-01</td>\n",
       "      <td>-3.837571e-01</td>\n",
       "      <td>-6.710190e-02</td>\n",
       "      <td>-1.157470e+00</td>\n",
       "      <td>-4.330384e-01</td>\n",
       "      <td>-3.976161e-01</td>\n",
       "      <td>-6.577329e-01</td>\n",
       "      <td>-4.531149e-01</td>\n",
       "      <td>-7.785215e-01</td>\n",
       "      <td>-4.203601e-01</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>8.332254e-01</td>\n",
       "      <td>4.989243e-02</td>\n",
       "      <td>-3.181057e-01</td>\n",
       "      <td>2.282336e-01</td>\n",
       "      <td>-7.289820e-01</td>\n",
       "      <td>-9.851319e-01</td>\n",
       "      <td>-3.067434e-01</td>\n",
       "      <td>-1.011005e-01</td>\n",
       "      <td>-3.837571e-01</td>\n",
       "      <td>-6.710190e-02</td>\n",
       "      <td>8.637773e-01</td>\n",
       "      <td>-4.330384e-01</td>\n",
       "      <td>-3.976161e-01</td>\n",
       "      <td>-6.577329e-01</td>\n",
       "      <td>-4.531149e-01</td>\n",
       "      <td>-7.785215e-01</td>\n",
       "      <td>-4.203601e-01</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>8.332254e-01</td>\n",
       "      <td>7.592802e-01</td>\n",
       "      <td>-3.181057e-01</td>\n",
       "      <td>2.282336e-01</td>\n",
       "      <td>1.371496e+00</td>\n",
       "      <td>1.014886e+00</td>\n",
       "      <td>1.848724e-01</td>\n",
       "      <td>5.354312e-01</td>\n",
       "      <td>-3.837571e-01</td>\n",
       "      <td>-6.710190e-02</td>\n",
       "      <td>8.637773e-01</td>\n",
       "      <td>-4.330384e-01</td>\n",
       "      <td>-3.976161e-01</td>\n",
       "      <td>1.520064e+00</td>\n",
       "      <td>-4.531149e-01</td>\n",
       "      <td>1.284224e+00</td>\n",
       "      <td>-4.203601e-01</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>8.332254e-01</td>\n",
       "      <td>1.734688e+00</td>\n",
       "      <td>3.142969e+00</td>\n",
       "      <td>2.282336e-01</td>\n",
       "      <td>1.371496e+00</td>\n",
       "      <td>1.014886e+00</td>\n",
       "      <td>3.746386e+00</td>\n",
       "      <td>8.746690e+00</td>\n",
       "      <td>2.605284e+00</td>\n",
       "      <td>1.489967e+01</td>\n",
       "      <td>8.637773e-01</td>\n",
       "      <td>2.308793e+00</td>\n",
       "      <td>2.514476e+00</td>\n",
       "      <td>1.520064e+00</td>\n",
       "      <td>2.206496e+00</td>\n",
       "      <td>1.284224e+00</td>\n",
       "      <td>2.378428e+00</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "             gender           age  hypertension  heart_disease  ever_married  \\\n",
       "count  4.907000e+03  4.907000e+03  4.907000e+03   4.907000e+03  4.907000e+03   \n",
       "mean  -6.176704e-16 -8.312885e-16 -6.857273e-16   3.216705e-15 -1.719929e-15   \n",
       "std    1.000000e+00  1.000000e+00  1.000000e+00   1.000000e+00  1.000000e+00   \n",
       "min   -1.199911e+00 -1.897377e+00 -3.181057e-01  -4.380583e+00 -7.289820e-01   \n",
       "25%   -1.199911e+00 -7.925055e-01 -3.181057e-01   2.282336e-01 -7.289820e-01   \n",
       "50%    8.332254e-01  4.989243e-02 -3.181057e-01   2.282336e-01 -7.289820e-01   \n",
       "75%    8.332254e-01  7.592802e-01 -3.181057e-01   2.282336e-01  1.371496e+00   \n",
       "max    8.332254e-01  1.734688e+00  3.142969e+00   2.282336e-01  1.371496e+00   \n",
       "\n",
       "       Residence_type  avg_glucose_level           bmi      Govt_job  \\\n",
       "count    4.907000e+03       4.907000e+03  4.907000e+03  4.907000e+03   \n",
       "mean     7.286475e-16       7.164049e-15 -1.886452e-15  9.466422e-17   \n",
       "std      1.000000e+00       1.000000e+00  1.000000e+00  1.000000e+00   \n",
       "min     -9.851319e-01      -1.129705e+00 -2.367153e+00 -3.837571e-01   \n",
       "25%     -9.851319e-01      -6.355003e-01 -6.867097e-01 -3.837571e-01   \n",
       "50%     -9.851319e-01      -3.067434e-01 -1.011005e-01 -3.837571e-01   \n",
       "75%      1.014886e+00       1.848724e-01  5.354312e-01 -3.837571e-01   \n",
       "max      1.014886e+00       3.746386e+00  8.746690e+00  2.605284e+00   \n",
       "\n",
       "       Never_worked       Private  Self-employed      children       Unknown  \\\n",
       "count  4.907000e+03  4.907000e+03   4.907000e+03  4.907000e+03  4.907000e+03   \n",
       "mean   5.653495e-17 -1.212263e-16  -4.691128e-16  7.943287e-16  1.113753e-15   \n",
       "std    1.000000e+00  1.000000e+00   1.000000e+00  1.000000e+00  1.000000e+00   \n",
       "min   -6.710190e-02 -1.157470e+00  -4.330384e-01 -3.976161e-01 -6.577329e-01   \n",
       "25%   -6.710190e-02 -1.157470e+00  -4.330384e-01 -3.976161e-01 -6.577329e-01   \n",
       "50%   -6.710190e-02  8.637773e-01  -4.330384e-01 -3.976161e-01 -6.577329e-01   \n",
       "75%   -6.710190e-02  8.637773e-01  -4.330384e-01 -3.976161e-01  1.520064e+00   \n",
       "max    1.489967e+01  8.637773e-01   2.308793e+00  2.514476e+00  1.520064e+00   \n",
       "\n",
       "       formerly smoked  never smoked        smokes  \n",
       "count     4.907000e+03  4.907000e+03  4.907000e+03  \n",
       "mean      2.409593e-18 -5.534146e-17 -6.488707e-16  \n",
       "std       1.000000e+00  1.000000e+00  1.000000e+00  \n",
       "min      -4.531149e-01 -7.785215e-01 -4.203601e-01  \n",
       "25%      -4.531149e-01 -7.785215e-01 -4.203601e-01  \n",
       "50%      -4.531149e-01 -7.785215e-01 -4.203601e-01  \n",
       "75%      -4.531149e-01  1.284224e+00 -4.203601e-01  \n",
       "max       2.206496e+00  1.284224e+00  2.378428e+00  "
      ]
     },
     "execution_count": 33,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data_stand = (data_raw - data_raw.mean(axis = 0))/data_raw.std(axis = 0)\n",
    "x = data_stand\n",
    "data_stand.describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "id": "69fe4f5c",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>gender</th>\n",
       "      <th>age</th>\n",
       "      <th>hypertension</th>\n",
       "      <th>heart_disease</th>\n",
       "      <th>ever_married</th>\n",
       "      <th>Residence_type</th>\n",
       "      <th>avg_glucose_level</th>\n",
       "      <th>bmi</th>\n",
       "      <th>Govt_job</th>\n",
       "      <th>Never_worked</th>\n",
       "      <th>Private</th>\n",
       "      <th>Self-employed</th>\n",
       "      <th>children</th>\n",
       "      <th>Unknown</th>\n",
       "      <th>formerly smoked</th>\n",
       "      <th>never smoked</th>\n",
       "      <th>smokes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>-1.199911</td>\n",
       "      <td>1.069637</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>-4.380583</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>-0.985132</td>\n",
       "      <td>2.777336</td>\n",
       "      <td>0.981003</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>0.863777</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>2.206496</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>-0.420360</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>-1.199911</td>\n",
       "      <td>1.646015</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>-4.380583</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>1.014886</td>\n",
       "      <td>0.013797</td>\n",
       "      <td>0.459047</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>0.863777</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>-0.453115</td>\n",
       "      <td>1.284224</td>\n",
       "      <td>-0.420360</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>0.833225</td>\n",
       "      <td>0.271576</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>-0.985132</td>\n",
       "      <td>1.483918</td>\n",
       "      <td>0.700929</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>0.863777</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>-0.453115</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>2.378428</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>0.833225</td>\n",
       "      <td>1.601678</td>\n",
       "      <td>3.142969</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>1.014886</td>\n",
       "      <td>1.548971</td>\n",
       "      <td>-0.623056</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>-1.157470</td>\n",
       "      <td>2.308793</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>-0.453115</td>\n",
       "      <td>1.284224</td>\n",
       "      <td>-0.420360</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>-1.199911</td>\n",
       "      <td>1.690352</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>-0.985132</td>\n",
       "      <td>1.821116</td>\n",
       "      <td>0.013475</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>0.863777</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>2.206496</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>-0.420360</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5104</th>\n",
       "      <td>0.833225</td>\n",
       "      <td>-1.324546</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>1.371496</td>\n",
       "      <td>1.014886</td>\n",
       "      <td>-0.050131</td>\n",
       "      <td>-1.310511</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>-1.157470</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>2.514476</td>\n",
       "      <td>1.520064</td>\n",
       "      <td>-0.453115</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>-0.420360</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5106</th>\n",
       "      <td>0.833225</td>\n",
       "      <td>1.690352</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>-0.985132</td>\n",
       "      <td>0.447788</td>\n",
       "      <td>1.413845</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>-1.157470</td>\n",
       "      <td>2.308793</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>-0.453115</td>\n",
       "      <td>1.284224</td>\n",
       "      <td>-0.420360</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5107</th>\n",
       "      <td>0.833225</td>\n",
       "      <td>-0.349138</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>1.014886</td>\n",
       "      <td>-0.502354</td>\n",
       "      <td>0.217165</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>-1.157470</td>\n",
       "      <td>2.308793</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>-0.453115</td>\n",
       "      <td>1.284224</td>\n",
       "      <td>-0.420360</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5108</th>\n",
       "      <td>-1.199911</td>\n",
       "      <td>0.360250</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>1.014886</td>\n",
       "      <td>1.372719</td>\n",
       "      <td>-0.419366</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>0.863777</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>2.206496</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>-0.420360</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5109</th>\n",
       "      <td>0.833225</td>\n",
       "      <td>0.049892</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>-0.985132</td>\n",
       "      <td>-0.450807</td>\n",
       "      <td>-0.342983</td>\n",
       "      <td>2.605284</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>-1.157470</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>1.520064</td>\n",
       "      <td>-0.453115</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>-0.420360</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>4907 rows × 17 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "        gender       age  hypertension  heart_disease  ever_married  \\\n",
       "0    -1.199911  1.069637     -0.318106      -4.380583     -0.728982   \n",
       "2    -1.199911  1.646015     -0.318106      -4.380583     -0.728982   \n",
       "3     0.833225  0.271576     -0.318106       0.228234     -0.728982   \n",
       "4     0.833225  1.601678      3.142969       0.228234     -0.728982   \n",
       "5    -1.199911  1.690352     -0.318106       0.228234     -0.728982   \n",
       "...        ...       ...           ...            ...           ...   \n",
       "5104  0.833225 -1.324546     -0.318106       0.228234      1.371496   \n",
       "5106  0.833225  1.690352     -0.318106       0.228234     -0.728982   \n",
       "5107  0.833225 -0.349138     -0.318106       0.228234     -0.728982   \n",
       "5108 -1.199911  0.360250     -0.318106       0.228234     -0.728982   \n",
       "5109  0.833225  0.049892     -0.318106       0.228234     -0.728982   \n",
       "\n",
       "      Residence_type  avg_glucose_level       bmi  Govt_job  Never_worked  \\\n",
       "0          -0.985132           2.777336  0.981003 -0.383757     -0.067102   \n",
       "2           1.014886           0.013797  0.459047 -0.383757     -0.067102   \n",
       "3          -0.985132           1.483918  0.700929 -0.383757     -0.067102   \n",
       "4           1.014886           1.548971 -0.623056 -0.383757     -0.067102   \n",
       "5          -0.985132           1.821116  0.013475 -0.383757     -0.067102   \n",
       "...              ...                ...       ...       ...           ...   \n",
       "5104        1.014886          -0.050131 -1.310511 -0.383757     -0.067102   \n",
       "5106       -0.985132           0.447788  1.413845 -0.383757     -0.067102   \n",
       "5107        1.014886          -0.502354  0.217165 -0.383757     -0.067102   \n",
       "5108        1.014886           1.372719 -0.419366 -0.383757     -0.067102   \n",
       "5109       -0.985132          -0.450807 -0.342983  2.605284     -0.067102   \n",
       "\n",
       "       Private  Self-employed  children   Unknown  formerly smoked  \\\n",
       "0     0.863777      -0.433038 -0.397616 -0.657733         2.206496   \n",
       "2     0.863777      -0.433038 -0.397616 -0.657733        -0.453115   \n",
       "3     0.863777      -0.433038 -0.397616 -0.657733        -0.453115   \n",
       "4    -1.157470       2.308793 -0.397616 -0.657733        -0.453115   \n",
       "5     0.863777      -0.433038 -0.397616 -0.657733         2.206496   \n",
       "...        ...            ...       ...       ...              ...   \n",
       "5104 -1.157470      -0.433038  2.514476  1.520064        -0.453115   \n",
       "5106 -1.157470       2.308793 -0.397616 -0.657733        -0.453115   \n",
       "5107 -1.157470       2.308793 -0.397616 -0.657733        -0.453115   \n",
       "5108  0.863777      -0.433038 -0.397616 -0.657733         2.206496   \n",
       "5109 -1.157470      -0.433038 -0.397616  1.520064        -0.453115   \n",
       "\n",
       "      never smoked    smokes  \n",
       "0        -0.778522 -0.420360  \n",
       "2         1.284224 -0.420360  \n",
       "3        -0.778522  2.378428  \n",
       "4         1.284224 -0.420360  \n",
       "5        -0.778522 -0.420360  \n",
       "...            ...       ...  \n",
       "5104     -0.778522 -0.420360  \n",
       "5106      1.284224 -0.420360  \n",
       "5107      1.284224 -0.420360  \n",
       "5108     -0.778522 -0.420360  \n",
       "5109     -0.778522 -0.420360  \n",
       "\n",
       "[4907 rows x 17 columns]"
      ]
     },
     "execution_count": 34,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "x"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "56713232",
   "metadata": {},
   "source": [
    "# 6. Разбиение на обучающую и тестовую выборку"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "13ea3411",
   "metadata": {},
   "source": [
    "Разобьем данные на обучающую и тестовую выборки в пропорции 4:1 (80% - обучающая выборка, 20% - тестовая):"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 113,
   "id": "c65f4faf",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "(3925, 17) (982, 17)\n"
     ]
    }
   ],
   "source": [
    "from sklearn.model_selection import train_test_split\n",
    "x_train, x_test, y_train, y_test = train_test_split(x, y, test_size = 0.2, random_state = 73)\n",
    "\n",
    "print(x_train.shape , x_test.shape)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 114,
   "id": "3633f494",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "3038    0\n",
       "4706    0\n",
       "1051    0\n",
       "3481    0\n",
       "2211    0\n",
       "       ..\n",
       "2224    0\n",
       "3177    0\n",
       "2253    0\n",
       "255     0\n",
       "4730    0\n",
       "Name: stroke, Length: 982, dtype: category\n",
       "Categories (2, int64): [0, 1]"
      ]
     },
     "execution_count": 114,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "y_test"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "11b70e1b",
   "metadata": {},
   "source": [
    "# 7. Классификация"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 37,
   "id": "2e6b7059",
   "metadata": {},
   "outputs": [],
   "source": [
    "from xgboost import XGBClassifier\n",
    "from sklearn.neighbors import KNeighborsClassifier\n",
    "from sklearn.ensemble import RandomForestClassifier\n",
    "from sklearn import svm\n",
    "from sklearn.svm import SVC\n",
    "\n",
    "from sklearn.model_selection import cross_val_score\n",
    "import sklearn.metrics as metrics\n",
    "from sklearn.metrics import mean_absolute_error ,mean_squared_error, median_absolute_error,confusion_matrix,accuracy_score,r2_score\n",
    "from sklearn.tree import DecisionTreeClassifier\n",
    "from sklearn.ensemble import ExtraTreesClassifier"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 38,
   "id": "8b3c62f2",
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>gender</th>\n",
       "      <th>age</th>\n",
       "      <th>hypertension</th>\n",
       "      <th>heart_disease</th>\n",
       "      <th>ever_married</th>\n",
       "      <th>Residence_type</th>\n",
       "      <th>avg_glucose_level</th>\n",
       "      <th>bmi</th>\n",
       "      <th>Govt_job</th>\n",
       "      <th>Never_worked</th>\n",
       "      <th>Private</th>\n",
       "      <th>Self-employed</th>\n",
       "      <th>children</th>\n",
       "      <th>Unknown</th>\n",
       "      <th>formerly smoked</th>\n",
       "      <th>never smoked</th>\n",
       "      <th>smokes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>68</th>\n",
       "      <td>-1.199911</td>\n",
       "      <td>0.714943</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>-0.985132</td>\n",
       "      <td>-0.429422</td>\n",
       "      <td>0.140782</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>0.863777</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>2.206496</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>-0.420360</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>28</th>\n",
       "      <td>-1.199911</td>\n",
       "      <td>1.158311</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>-4.380583</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>-0.985132</td>\n",
       "      <td>2.024155</td>\n",
       "      <td>-0.075639</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>-1.157470</td>\n",
       "      <td>2.308793</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>-0.453115</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>2.378428</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2108</th>\n",
       "      <td>0.833225</td>\n",
       "      <td>-0.925516</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>1.371496</td>\n",
       "      <td>-0.985132</td>\n",
       "      <td>-0.715973</td>\n",
       "      <td>1.579343</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>0.863777</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>-0.453115</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>2.378428</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3743</th>\n",
       "      <td>0.833225</td>\n",
       "      <td>0.138566</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>-0.985132</td>\n",
       "      <td>0.130399</td>\n",
       "      <td>-0.712171</td>\n",
       "      <td>2.605284</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>-1.157470</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>-0.453115</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>2.378428</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3163</th>\n",
       "      <td>-1.199911</td>\n",
       "      <td>-0.836842</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>1.014886</td>\n",
       "      <td>-0.709670</td>\n",
       "      <td>-0.954053</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>0.863777</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>-0.453115</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>2.378428</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>364</th>\n",
       "      <td>-1.199911</td>\n",
       "      <td>-0.393475</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>-0.985132</td>\n",
       "      <td>0.735014</td>\n",
       "      <td>0.790044</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>0.863777</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>1.520064</td>\n",
       "      <td>-0.453115</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>-0.420360</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4608</th>\n",
       "      <td>-1.199911</td>\n",
       "      <td>0.714943</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>1.014886</td>\n",
       "      <td>-0.808939</td>\n",
       "      <td>-0.253868</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>0.863777</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>2.206496</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>-0.420360</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>438</th>\n",
       "      <td>-1.199911</td>\n",
       "      <td>0.448923</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>1.014886</td>\n",
       "      <td>0.255553</td>\n",
       "      <td>-0.050178</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>0.863777</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>2.206496</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>-0.420360</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4194</th>\n",
       "      <td>0.833225</td>\n",
       "      <td>-0.393475</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>-0.985132</td>\n",
       "      <td>-0.650244</td>\n",
       "      <td>-0.164754</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>0.863777</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>-0.657733</td>\n",
       "      <td>-0.453115</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>2.378428</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>179</th>\n",
       "      <td>-1.199911</td>\n",
       "      <td>1.690352</td>\n",
       "      <td>-0.318106</td>\n",
       "      <td>0.228234</td>\n",
       "      <td>-0.728982</td>\n",
       "      <td>-0.985132</td>\n",
       "      <td>2.429108</td>\n",
       "      <td>-0.355713</td>\n",
       "      <td>-0.383757</td>\n",
       "      <td>-0.067102</td>\n",
       "      <td>0.863777</td>\n",
       "      <td>-0.433038</td>\n",
       "      <td>-0.397616</td>\n",
       "      <td>1.520064</td>\n",
       "      <td>-0.453115</td>\n",
       "      <td>-0.778522</td>\n",
       "      <td>-0.420360</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>3925 rows × 17 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "        gender       age  hypertension  heart_disease  ever_married  \\\n",
       "68   -1.199911  0.714943     -0.318106       0.228234     -0.728982   \n",
       "28   -1.199911  1.158311     -0.318106      -4.380583     -0.728982   \n",
       "2108  0.833225 -0.925516     -0.318106       0.228234      1.371496   \n",
       "3743  0.833225  0.138566     -0.318106       0.228234     -0.728982   \n",
       "3163 -1.199911 -0.836842     -0.318106       0.228234     -0.728982   \n",
       "...        ...       ...           ...            ...           ...   \n",
       "364  -1.199911 -0.393475     -0.318106       0.228234     -0.728982   \n",
       "4608 -1.199911  0.714943     -0.318106       0.228234     -0.728982   \n",
       "438  -1.199911  0.448923     -0.318106       0.228234     -0.728982   \n",
       "4194  0.833225 -0.393475     -0.318106       0.228234     -0.728982   \n",
       "179  -1.199911  1.690352     -0.318106       0.228234     -0.728982   \n",
       "\n",
       "      Residence_type  avg_glucose_level       bmi  Govt_job  Never_worked  \\\n",
       "68         -0.985132          -0.429422  0.140782 -0.383757     -0.067102   \n",
       "28         -0.985132           2.024155 -0.075639 -0.383757     -0.067102   \n",
       "2108       -0.985132          -0.715973  1.579343 -0.383757     -0.067102   \n",
       "3743       -0.985132           0.130399 -0.712171  2.605284     -0.067102   \n",
       "3163        1.014886          -0.709670 -0.954053 -0.383757     -0.067102   \n",
       "...              ...                ...       ...       ...           ...   \n",
       "364        -0.985132           0.735014  0.790044 -0.383757     -0.067102   \n",
       "4608        1.014886          -0.808939 -0.253868 -0.383757     -0.067102   \n",
       "438         1.014886           0.255553 -0.050178 -0.383757     -0.067102   \n",
       "4194       -0.985132          -0.650244 -0.164754 -0.383757     -0.067102   \n",
       "179        -0.985132           2.429108 -0.355713 -0.383757     -0.067102   \n",
       "\n",
       "       Private  Self-employed  children   Unknown  formerly smoked  \\\n",
       "68    0.863777      -0.433038 -0.397616 -0.657733         2.206496   \n",
       "28   -1.157470       2.308793 -0.397616 -0.657733        -0.453115   \n",
       "2108  0.863777      -0.433038 -0.397616 -0.657733        -0.453115   \n",
       "3743 -1.157470      -0.433038 -0.397616 -0.657733        -0.453115   \n",
       "3163  0.863777      -0.433038 -0.397616 -0.657733        -0.453115   \n",
       "...        ...            ...       ...       ...              ...   \n",
       "364   0.863777      -0.433038 -0.397616  1.520064        -0.453115   \n",
       "4608  0.863777      -0.433038 -0.397616 -0.657733         2.206496   \n",
       "438   0.863777      -0.433038 -0.397616 -0.657733         2.206496   \n",
       "4194  0.863777      -0.433038 -0.397616 -0.657733        -0.453115   \n",
       "179   0.863777      -0.433038 -0.397616  1.520064        -0.453115   \n",
       "\n",
       "      never smoked    smokes  \n",
       "68       -0.778522 -0.420360  \n",
       "28       -0.778522  2.378428  \n",
       "2108     -0.778522  2.378428  \n",
       "3743     -0.778522  2.378428  \n",
       "3163     -0.778522  2.378428  \n",
       "...            ...       ...  \n",
       "364      -0.778522 -0.420360  \n",
       "4608     -0.778522 -0.420360  \n",
       "438      -0.778522 -0.420360  \n",
       "4194     -0.778522  2.378428  \n",
       "179      -0.778522 -0.420360  \n",
       "\n",
       "[3925 rows x 17 columns]"
      ]
     },
     "execution_count": 38,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "x_train"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 39,
   "id": "97cc9ae5",
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "68      1\n",
       "28      1\n",
       "2108    0\n",
       "3743    0\n",
       "3163    0\n",
       "       ..\n",
       "364     0\n",
       "4608    0\n",
       "438     0\n",
       "4194    0\n",
       "179     1\n",
       "Name: stroke, Length: 3925, dtype: category\n",
       "Categories (2, int64): [0, 1]"
      ]
     },
     "execution_count": 39,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "y_train"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "54075194",
   "metadata": {},
   "source": [
    "##### Воспользуюсь GridSearchCV для подбора оптимальных параметров для различных методов машинного обучения"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f395eec7",
   "metadata": {},
   "source": [
    "##### Используемые параметры сеток выбраны с учетом первичных запусков с более широким диапазоном значений. Столь узкий диапазон был выбран для демонстрации и с целью дальнейшей экономии времени при повторном запуске кода."
   ]
  },
  {
   "cell_type": "markdown",
   "id": "1a1b7e0e",
   "metadata": {},
   "source": [
    "## KNN"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 40,
   "id": "2312bae3",
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Best hyperparameters are: {'n_neighbors': 6}\n",
      "Best score is: 0.9549044585987261\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n"
     ]
    }
   ],
   "source": [
    "from sklearn.model_selection import GridSearchCV\n",
    "from sklearn.metrics import confusion_matrix\n",
    "from sklearn.neighbors import KNeighborsClassifier\n",
    "\n",
    "nnb = [3, 4, 5, 6, 7, 8, 9, 10]\n",
    "\n",
    "knn = KNeighborsClassifier()\n",
    "model_grid = GridSearchCV(knn, param_grid = {'n_neighbors': nnb}, cv=5) # автоматический подбор параметров для модели машинного обучения\n",
    "model_grid.fit(x_train, y_train)\n",
    "\n",
    "print('Best hyperparameters are: '+str(model_grid.best_params_))\n",
    "print('Best score is: '+str(model_grid.best_score_))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 41,
   "id": "730a8157",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Best hyperparameters are: {'n_neighbors': 6}\n",
      "Best score is: 0.9549044585987261\n"
     ]
    }
   ],
   "source": [
    "print('Best hyperparameters are: '+str(model_grid.best_params_))\n",
    "print('Best score is: '+str(model_grid.best_score_))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "de8c735a",
   "metadata": {},
   "source": [
    "## XGB"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "34d6a031",
   "metadata": {},
   "source": [
    "Extreme Gradient Boosting - экстремальный градиентный бустинг.\n",
    "\n",
    "Значения по умолчанию для XGBClassifier:\n",
    "\n",
    "    max_depth=3 \n",
    "    learning_rate=0.1\n",
    "    n_estimators=100\n",
    "    silent=True\n",
    "    objective='binary:logistic'\n",
    "    бустер='gbtree'\n",
    "    n_jobs=1\n",
    "    nthread=Нет\n",
    "    гамма=0\n",
    "    min_child_weight=1\n",
    "    max_delta_step=0\n",
    "    подвыборка=1\n",
    "    colsample_bytree=1\n",
    "    colsample_bylevel=1\n",
    "    reg_alpha=0\n",
    "    reg_lambda=1\n",
    "    scale_pos_weight=1\n",
    "    base_score=0.5\n",
    "    random_state=0\n",
    "    seed=Нет\n",
    "    отсутствует=Нет\n",
    "\n",
    "\n",
    "Рассмотрю поиск оптимальных гиперпараметров таких как:\n",
    "\n",
    "    Количество деревьев\n",
    "\n",
    "По умолчанию количество деревьев является небольшим. Модель расширенного дерева строится последовательно, где каждое новое дерево пытается моделировать и исправлять ошибки, допущенные последовательностью предыдущих деревьев. Модель быстро достигает точки убывающей отдачи. \n",
    "\n",
    "    Размера деревьев (количество слоев/глубина)\n",
    "\n",
    "Определяет количество уровней в каждом дереве. Ожидается, что неглубокие деревья будут иметь низкую производительность, потому что они фиксируют мало деталей проблемы. Более глубокие деревья, как правило, фиксируют слишком много деталей. Разумные значения находятся в диапазоне от 1 до 10 или 20\n",
    "\n",
    "    Скорость обучения (learning_rate)\n",
    "\n",
    "Скорость обучения контролирует вклад каждого дерева в ансамбль. Разумные значения меньше 1,0 и немного больше 0,0 (например, 1e-8)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 42,
   "id": "bcf9056e",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Best hyperparameters are: {'learning_rate': 0.0001, 'max_depth': 1, 'n_estimators': 10}\n",
      "Best score is: 0.9546498054323203\n",
      "XGBClassifier(base_score=0.5, booster='gbtree', callbacks=None,\n",
      "              colsample_bylevel=1, colsample_bynode=1, colsample_bytree=1,\n",
      "              early_stopping_rounds=None, enable_categorical=False,\n",
      "              eval_metric=None, feature_types=None, gamma=0, gpu_id=-1,\n",
      "              grow_policy='depthwise', importance_type=None,\n",
      "              interaction_constraints='', learning_rate=0.0001, max_bin=256,\n",
      "              max_cat_threshold=64, max_cat_to_onehot=4, max_delta_step=0,\n",
      "              max_depth=1, max_leaves=0, min_child_weight=1, missing=nan,\n",
      "              monotone_constraints='()', n_estimators=10, n_jobs=0,\n",
      "              num_parallel_tree=1, predictor='auto', random_state=0, ...)\n"
     ]
    }
   ],
   "source": [
    "import xgboost as xgb\n",
    "\n",
    "clf1 = xgb.XGBClassifier()\n",
    "\n",
    "param_dist = {\n",
    "        'n_estimators': [10, 20, 30, 40, 50, 70, 80], \n",
    "        'max_depth': [1, 2, 5],\n",
    "        'learning_rate': [0.0001,0.001, 0.01, 0.1, 0.2]\n",
    "        }\n",
    "\n",
    "grid = GridSearchCV(clf1, param_dist,cv = 3)\n",
    "\n",
    "grid_XGB = grid.fit(x_train,y_train)\n",
    "\n",
    "# Вернуться к лучшему тренеру\n",
    "best_estimator = grid_XGB.best_estimator_\n",
    "\n",
    "print('Best hyperparameters are: '+str(grid_XGB.best_params_))\n",
    "print('Best score is: '+str(grid_XGB.best_score_))\n",
    "print(best_estimator)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "70ae64a5",
   "metadata": {},
   "source": [
    "## Random Forest"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "9eb34423",
   "metadata": {},
   "source": [
    "Значения по умолчанию для Random Forest:\n",
    "\n",
    "    n_estimatorsint = 100\n",
    "    criterion{“gini”, “entropy”, “log_loss”}, default=”gini”\n",
    "    max_depth = None\n",
    "    min_samples_splitint = 2\n",
    "    min_samples_leafint=1\n",
    "    bootstrap = True\n",
    "...\n",
    "см. https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html\n",
    "\n",
    "Рассмотрю поиск оптимальных гиперпараметров таких как:\n",
    "\n",
    "    n_estimators – число деревьев в лесу\n",
    "    \n",
    "    max_depth – глубина дерева\n",
    "    \n",
    "    min_samples_leaf – минимальное число объектов в листе. У этого параметра есть понятная интерпретация: скажем, если он   равен 5, то дерево будет порождать только те классифицирующие правила, которые верны как минимум для 5 объектов\n",
    "    \n",
    "    bootstrap- используются ли образцы начальной загрузки при построении деревьев. Если значение равно False, для построения каждого дерева используется весь набор данных."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 43,
   "id": "1b8be40c",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Best hyperparameters are: {'bootstrap': False, 'max_depth': 5, 'min_samples_leaf': 1, 'n_estimators': 3}\n",
      "Best score is: 0.9549044585987261\n"
     ]
    }
   ],
   "source": [
    "from sklearn.model_selection import GridSearchCV\n",
    "from sklearn.metrics import confusion_matrix\n",
    "from sklearn.neighbors import KNeighborsClassifier\n",
    "from sklearn import ensemble\n",
    "\n",
    "rf = ensemble.RandomForestClassifier()\n",
    "\n",
    "param_grid = {'n_estimators': [3, 10, 30, 50, 70, 80, 100], \n",
    "              'max_depth': [None, 1, 3, 5, 10],\n",
    "              'bootstrap': [False],\n",
    "              'min_samples_leaf':[1,2,3, 4]}\n",
    "\n",
    "\n",
    "grid = GridSearchCV(rf, param_grid=param_grid, cv=5, scoring='accuracy')\n",
    "grid_RF = grid.fit(x_train,y_train)\n",
    "\n",
    "print('Best hyperparameters are: '+str(grid_RF.best_params_))\n",
    "print('Best score is: '+str(grid_RF.best_score_))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f4d0bcfa",
   "metadata": {},
   "source": [
    "## SVM"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "ad357527",
   "metadata": {},
   "source": [
    "Машина опорных векторов\n",
    " \n",
    "Рассмотрю поиск оптимальных гиперпараметров таких как:\n",
    "    \n",
    "    C - параметр регуляризации\n",
    "    gamma - коэффициент функции ядра (по умолчанию автоматически выбирается)\n",
    "    kernel - этот параметр определяет тип ядра, который будет использоваться в алгоритме.\n",
    "    \n",
    "Основным параметром здесь является kernel"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 44,
   "id": "3c76e06e",
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Fitting 5 folds for each of 40 candidates, totalling 200 fits\n",
      "[CV 1/5] END ......C=0.001, gamma=4, kernel=rbf;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ......C=0.001, gamma=4, kernel=rbf;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ......C=0.001, gamma=4, kernel=rbf;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ......C=0.001, gamma=4, kernel=rbf;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ......C=0.001, gamma=4, kernel=rbf;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END ...C=0.001, gamma=4, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ...C=0.001, gamma=4, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ...C=0.001, gamma=4, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ...C=0.001, gamma=4, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ...C=0.001, gamma=4, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END ......C=0.001, gamma=3, kernel=rbf;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ......C=0.001, gamma=3, kernel=rbf;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ......C=0.001, gamma=3, kernel=rbf;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ......C=0.001, gamma=3, kernel=rbf;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ......C=0.001, gamma=3, kernel=rbf;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END ...C=0.001, gamma=3, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ...C=0.001, gamma=3, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ...C=0.001, gamma=3, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ...C=0.001, gamma=3, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ...C=0.001, gamma=3, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END ......C=0.001, gamma=2, kernel=rbf;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ......C=0.001, gamma=2, kernel=rbf;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ......C=0.001, gamma=2, kernel=rbf;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ......C=0.001, gamma=2, kernel=rbf;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ......C=0.001, gamma=2, kernel=rbf;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END ...C=0.001, gamma=2, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ...C=0.001, gamma=2, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ...C=0.001, gamma=2, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ...C=0.001, gamma=2, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ...C=0.001, gamma=2, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END ....C=0.001, gamma=1.5, kernel=rbf;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ....C=0.001, gamma=1.5, kernel=rbf;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ....C=0.001, gamma=1.5, kernel=rbf;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ....C=0.001, gamma=1.5, kernel=rbf;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ....C=0.001, gamma=1.5, kernel=rbf;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END .C=0.001, gamma=1.5, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END .C=0.001, gamma=1.5, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END .C=0.001, gamma=1.5, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END .C=0.001, gamma=1.5, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END .C=0.001, gamma=1.5, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END ......C=0.005, gamma=4, kernel=rbf;, score=0.954 total time=   0.1s\n",
      "[CV 2/5] END ......C=0.005, gamma=4, kernel=rbf;, score=0.954 total time=   0.2s\n",
      "[CV 3/5] END ......C=0.005, gamma=4, kernel=rbf;, score=0.954 total time=   0.1s\n",
      "[CV 4/5] END ......C=0.005, gamma=4, kernel=rbf;, score=0.955 total time=   0.1s\n",
      "[CV 5/5] END ......C=0.005, gamma=4, kernel=rbf;, score=0.955 total time=   0.2s\n",
      "[CV 1/5] END ...C=0.005, gamma=4, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ...C=0.005, gamma=4, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ...C=0.005, gamma=4, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ...C=0.005, gamma=4, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ...C=0.005, gamma=4, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END ......C=0.005, gamma=3, kernel=rbf;, score=0.954 total time=   0.1s\n",
      "[CV 2/5] END ......C=0.005, gamma=3, kernel=rbf;, score=0.954 total time=   0.1s\n",
      "[CV 3/5] END ......C=0.005, gamma=3, kernel=rbf;, score=0.954 total time=   0.1s\n",
      "[CV 4/5] END ......C=0.005, gamma=3, kernel=rbf;, score=0.955 total time=   0.1s\n",
      "[CV 5/5] END ......C=0.005, gamma=3, kernel=rbf;, score=0.955 total time=   0.1s\n",
      "[CV 1/5] END ...C=0.005, gamma=3, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ...C=0.005, gamma=3, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ...C=0.005, gamma=3, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ...C=0.005, gamma=3, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ...C=0.005, gamma=3, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END ......C=0.005, gamma=2, kernel=rbf;, score=0.954 total time=   0.1s\n",
      "[CV 2/5] END ......C=0.005, gamma=2, kernel=rbf;, score=0.954 total time=   0.1s\n",
      "[CV 3/5] END ......C=0.005, gamma=2, kernel=rbf;, score=0.954 total time=   0.1s\n",
      "[CV 4/5] END ......C=0.005, gamma=2, kernel=rbf;, score=0.955 total time=   0.1s\n",
      "[CV 5/5] END ......C=0.005, gamma=2, kernel=rbf;, score=0.955 total time=   0.1s\n",
      "[CV 1/5] END ...C=0.005, gamma=2, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ...C=0.005, gamma=2, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ...C=0.005, gamma=2, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ...C=0.005, gamma=2, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ...C=0.005, gamma=2, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END ....C=0.005, gamma=1.5, kernel=rbf;, score=0.954 total time=   0.1s\n",
      "[CV 2/5] END ....C=0.005, gamma=1.5, kernel=rbf;, score=0.954 total time=   0.1s\n",
      "[CV 3/5] END ....C=0.005, gamma=1.5, kernel=rbf;, score=0.954 total time=   0.1s\n",
      "[CV 4/5] END ....C=0.005, gamma=1.5, kernel=rbf;, score=0.955 total time=   0.1s\n",
      "[CV 5/5] END ....C=0.005, gamma=1.5, kernel=rbf;, score=0.955 total time=   0.1s\n",
      "[CV 1/5] END .C=0.005, gamma=1.5, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END .C=0.005, gamma=1.5, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END .C=0.005, gamma=1.5, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END .C=0.005, gamma=1.5, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END .C=0.005, gamma=1.5, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END .......C=0.01, gamma=4, kernel=rbf;, score=0.954 total time=   0.3s\n",
      "[CV 2/5] END .......C=0.01, gamma=4, kernel=rbf;, score=0.954 total time=   0.3s\n",
      "[CV 3/5] END .......C=0.01, gamma=4, kernel=rbf;, score=0.954 total time=   0.3s\n",
      "[CV 4/5] END .......C=0.01, gamma=4, kernel=rbf;, score=0.955 total time=   0.3s\n",
      "[CV 5/5] END .......C=0.01, gamma=4, kernel=rbf;, score=0.955 total time=   0.3s\n",
      "[CV 1/5] END ....C=0.01, gamma=4, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ....C=0.01, gamma=4, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ....C=0.01, gamma=4, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ....C=0.01, gamma=4, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ....C=0.01, gamma=4, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END .......C=0.01, gamma=3, kernel=rbf;, score=0.954 total time=   0.3s\n",
      "[CV 2/5] END .......C=0.01, gamma=3, kernel=rbf;, score=0.954 total time=   0.3s\n",
      "[CV 3/5] END .......C=0.01, gamma=3, kernel=rbf;, score=0.954 total time=   0.2s\n",
      "[CV 4/5] END .......C=0.01, gamma=3, kernel=rbf;, score=0.955 total time=   0.3s\n",
      "[CV 5/5] END .......C=0.01, gamma=3, kernel=rbf;, score=0.955 total time=   0.3s\n",
      "[CV 1/5] END ....C=0.01, gamma=3, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ....C=0.01, gamma=3, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ....C=0.01, gamma=3, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ....C=0.01, gamma=3, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ....C=0.01, gamma=3, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END .......C=0.01, gamma=2, kernel=rbf;, score=0.954 total time=   0.2s\n"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "[CV 2/5] END .......C=0.01, gamma=2, kernel=rbf;, score=0.954 total time=   0.2s\n",
      "[CV 3/5] END .......C=0.01, gamma=2, kernel=rbf;, score=0.954 total time=   0.2s\n",
      "[CV 4/5] END .......C=0.01, gamma=2, kernel=rbf;, score=0.955 total time=   0.2s\n",
      "[CV 5/5] END .......C=0.01, gamma=2, kernel=rbf;, score=0.955 total time=   0.2s\n",
      "[CV 1/5] END ....C=0.01, gamma=2, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ....C=0.01, gamma=2, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ....C=0.01, gamma=2, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ....C=0.01, gamma=2, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ....C=0.01, gamma=2, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END .....C=0.01, gamma=1.5, kernel=rbf;, score=0.954 total time=   0.2s\n",
      "[CV 2/5] END .....C=0.01, gamma=1.5, kernel=rbf;, score=0.954 total time=   0.2s\n",
      "[CV 3/5] END .....C=0.01, gamma=1.5, kernel=rbf;, score=0.954 total time=   0.2s\n",
      "[CV 4/5] END .....C=0.01, gamma=1.5, kernel=rbf;, score=0.955 total time=   0.2s\n",
      "[CV 5/5] END .....C=0.01, gamma=1.5, kernel=rbf;, score=0.955 total time=   0.2s\n",
      "[CV 1/5] END ..C=0.01, gamma=1.5, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ..C=0.01, gamma=1.5, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ..C=0.01, gamma=1.5, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ..C=0.01, gamma=1.5, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ..C=0.01, gamma=1.5, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END .......C=0.05, gamma=4, kernel=rbf;, score=0.954 total time=   0.5s\n",
      "[CV 2/5] END .......C=0.05, gamma=4, kernel=rbf;, score=0.954 total time=   0.5s\n",
      "[CV 3/5] END .......C=0.05, gamma=4, kernel=rbf;, score=0.954 total time=   0.5s\n",
      "[CV 4/5] END .......C=0.05, gamma=4, kernel=rbf;, score=0.955 total time=   0.5s\n",
      "[CV 5/5] END .......C=0.05, gamma=4, kernel=rbf;, score=0.955 total time=   0.5s\n",
      "[CV 1/5] END ....C=0.05, gamma=4, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ....C=0.05, gamma=4, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ....C=0.05, gamma=4, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ....C=0.05, gamma=4, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ....C=0.05, gamma=4, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END .......C=0.05, gamma=3, kernel=rbf;, score=0.954 total time=   0.4s\n",
      "[CV 2/5] END .......C=0.05, gamma=3, kernel=rbf;, score=0.954 total time=   0.4s\n",
      "[CV 3/5] END .......C=0.05, gamma=3, kernel=rbf;, score=0.954 total time=   0.4s\n",
      "[CV 4/5] END .......C=0.05, gamma=3, kernel=rbf;, score=0.955 total time=   0.5s\n",
      "[CV 5/5] END .......C=0.05, gamma=3, kernel=rbf;, score=0.955 total time=   0.4s\n",
      "[CV 1/5] END ....C=0.05, gamma=3, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ....C=0.05, gamma=3, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ....C=0.05, gamma=3, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ....C=0.05, gamma=3, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ....C=0.05, gamma=3, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END .......C=0.05, gamma=2, kernel=rbf;, score=0.954 total time=   0.4s\n",
      "[CV 2/5] END .......C=0.05, gamma=2, kernel=rbf;, score=0.954 total time=   0.4s\n",
      "[CV 3/5] END .......C=0.05, gamma=2, kernel=rbf;, score=0.954 total time=   0.4s\n",
      "[CV 4/5] END .......C=0.05, gamma=2, kernel=rbf;, score=0.955 total time=   0.4s\n",
      "[CV 5/5] END .......C=0.05, gamma=2, kernel=rbf;, score=0.955 total time=   0.4s\n",
      "[CV 1/5] END ....C=0.05, gamma=2, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ....C=0.05, gamma=2, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ....C=0.05, gamma=2, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ....C=0.05, gamma=2, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ....C=0.05, gamma=2, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END .....C=0.05, gamma=1.5, kernel=rbf;, score=0.954 total time=   0.3s\n",
      "[CV 2/5] END .....C=0.05, gamma=1.5, kernel=rbf;, score=0.954 total time=   0.3s\n",
      "[CV 3/5] END .....C=0.05, gamma=1.5, kernel=rbf;, score=0.954 total time=   0.3s\n",
      "[CV 4/5] END .....C=0.05, gamma=1.5, kernel=rbf;, score=0.955 total time=   0.4s\n",
      "[CV 5/5] END .....C=0.05, gamma=1.5, kernel=rbf;, score=0.955 total time=   0.3s\n",
      "[CV 1/5] END ..C=0.05, gamma=1.5, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ..C=0.05, gamma=1.5, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ..C=0.05, gamma=1.5, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ..C=0.05, gamma=1.5, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ..C=0.05, gamma=1.5, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END ........C=0.1, gamma=4, kernel=rbf;, score=0.954 total time=   0.6s\n",
      "[CV 2/5] END ........C=0.1, gamma=4, kernel=rbf;, score=0.954 total time=   0.6s\n",
      "[CV 3/5] END ........C=0.1, gamma=4, kernel=rbf;, score=0.954 total time=   0.5s\n",
      "[CV 4/5] END ........C=0.1, gamma=4, kernel=rbf;, score=0.955 total time=   0.5s\n",
      "[CV 5/5] END ........C=0.1, gamma=4, kernel=rbf;, score=0.955 total time=   0.5s\n",
      "[CV 1/5] END .....C=0.1, gamma=4, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END .....C=0.1, gamma=4, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END .....C=0.1, gamma=4, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END .....C=0.1, gamma=4, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END .....C=0.1, gamma=4, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END ........C=0.1, gamma=3, kernel=rbf;, score=0.954 total time=   0.5s\n",
      "[CV 2/5] END ........C=0.1, gamma=3, kernel=rbf;, score=0.954 total time=   0.6s\n",
      "[CV 3/5] END ........C=0.1, gamma=3, kernel=rbf;, score=0.954 total time=   0.5s\n",
      "[CV 4/5] END ........C=0.1, gamma=3, kernel=rbf;, score=0.955 total time=   0.5s\n",
      "[CV 5/5] END ........C=0.1, gamma=3, kernel=rbf;, score=0.955 total time=   0.5s\n",
      "[CV 1/5] END .....C=0.1, gamma=3, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END .....C=0.1, gamma=3, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END .....C=0.1, gamma=3, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END .....C=0.1, gamma=3, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END .....C=0.1, gamma=3, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END ........C=0.1, gamma=2, kernel=rbf;, score=0.954 total time=   0.5s\n",
      "[CV 2/5] END ........C=0.1, gamma=2, kernel=rbf;, score=0.954 total time=   0.5s\n",
      "[CV 3/5] END ........C=0.1, gamma=2, kernel=rbf;, score=0.954 total time=   0.5s\n",
      "[CV 4/5] END ........C=0.1, gamma=2, kernel=rbf;, score=0.955 total time=   0.5s\n",
      "[CV 5/5] END ........C=0.1, gamma=2, kernel=rbf;, score=0.955 total time=   0.5s\n",
      "[CV 1/5] END .....C=0.1, gamma=2, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END .....C=0.1, gamma=2, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END .....C=0.1, gamma=2, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END .....C=0.1, gamma=2, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END .....C=0.1, gamma=2, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 1/5] END ......C=0.1, gamma=1.5, kernel=rbf;, score=0.954 total time=   0.4s\n",
      "[CV 2/5] END ......C=0.1, gamma=1.5, kernel=rbf;, score=0.954 total time=   0.4s\n",
      "[CV 3/5] END ......C=0.1, gamma=1.5, kernel=rbf;, score=0.954 total time=   0.4s\n",
      "[CV 4/5] END ......C=0.1, gamma=1.5, kernel=rbf;, score=0.955 total time=   0.5s\n",
      "[CV 5/5] END ......C=0.1, gamma=1.5, kernel=rbf;, score=0.955 total time=   0.5s\n",
      "[CV 1/5] END ...C=0.1, gamma=1.5, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 2/5] END ...C=0.1, gamma=1.5, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 3/5] END ...C=0.1, gamma=1.5, kernel=linear;, score=0.954 total time=   0.0s\n",
      "[CV 4/5] END ...C=0.1, gamma=1.5, kernel=linear;, score=0.955 total time=   0.0s\n",
      "[CV 5/5] END ...C=0.1, gamma=1.5, kernel=linear;, score=0.955 total time=   0.0s\n",
      "Best hyperparameters are: {'C': 0.001, 'gamma': 4, 'kernel': 'rbf'}\n",
      "Best score is: 0.9546496815286625\n"
     ]
    }
   ],
   "source": [
    "from sklearn.model_selection import GridSearchCV\n",
    "from sklearn import svm\n",
    "from sklearn.svm import SVC\n",
    "  \n",
    "# defining parameter range\n",
    "param_grid = {'C': [0.001,0.005, 0.01, 0.05, 0.1], \n",
    "              'gamma': [4, 3, 2, 1.5],\n",
    "              'kernel': ['rbf', 'linear']} \n",
    "  \n",
    "grid = GridSearchCV(svm.SVC(), param_grid, refit = True, verbose = 3)\n",
    "grid_SVM = grid.fit(x_train,y_train)\n",
    "\n",
    "print('Best hyperparameters are: '+str(grid_SVM.best_params_))\n",
    "print('Best score is: '+str(grid_SVM.best_score_))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "d614ffbf",
   "metadata": {},
   "source": [
    "## DecisionTreeClassifier"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "cbd9086a",
   "metadata": {},
   "source": [
    "    max_features — максимальное число признаков, по которым ищется лучшее разбиение в дереве (это нужно потому, что при большом количестве признаков будет \"дорого\" искать лучшее (по критерию типа прироста информации) разбиение среди всех признаков)\n",
    "\n",
    "    min_samples_leaf \n",
    "    max_depth"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 45,
   "id": "a3df2f5a",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Best hyperparameters are: {'max_depth': 3, 'max_features': 5, 'min_samples_leaf': 3}\n",
      "Best score is: 0.9549044585987261\n"
     ]
    }
   ],
   "source": [
    "from sklearn.model_selection import GridSearchCV\n",
    "from sklearn.metrics import confusion_matrix\n",
    "from sklearn.neighbors import KNeighborsClassifier\n",
    "from sklearn import ensemble\n",
    "from sklearn.tree import DecisionTreeClassifier\n",
    "\n",
    "dtc = DecisionTreeClassifier()\n",
    "\n",
    "param_grid = { 'max_depth': [None, 1, 3, 5, 10],\n",
    "              'min_samples_leaf':[1,2,3, 4],\n",
    "              'max_features': [1,3,5]}\n",
    "\n",
    "\n",
    "grid = GridSearchCV(dtc, param_grid=param_grid, cv=5, scoring='accuracy')\n",
    "grid_dtc = grid.fit(x_train,y_train)\n",
    "\n",
    "print('Best hyperparameters are: '+str(grid_dtc.best_params_))\n",
    "print('Best score is: '+str(grid_dtc.best_score_))\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "3fbff54a",
   "metadata": {},
   "source": [
    "## ExtraTreesClassifier"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 46,
   "id": "34c4e21d",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Best hyperparameters are: {'max_depth': None, 'max_features': 1, 'min_samples_leaf': 3, 'n_estimators': 3}\n",
      "Best score is: 0.9549044585987263\n"
     ]
    }
   ],
   "source": [
    "from sklearn.model_selection import GridSearchCV\n",
    "from sklearn.metrics import confusion_matrix\n",
    "from sklearn.neighbors import KNeighborsClassifier\n",
    "from sklearn import ensemble\n",
    "from sklearn.tree import DecisionTreeClassifier\n",
    "\n",
    "ert = ExtraTreesClassifier()\n",
    "\n",
    "param_grid = {'n_estimators': [3, 10, 30, 50, 70, 80, 100],\n",
    "              'max_depth': [None, 1, 3, 5, 10],\n",
    "              'min_samples_leaf':[1,2,3, 4],\n",
    "              'max_features': [1,3,5]}\n",
    "\n",
    "\n",
    "grid = GridSearchCV(ert, param_grid=param_grid, cv=5, scoring='accuracy')\n",
    "grid_ert = grid.fit(x_train,y_train)\n",
    "\n",
    "print('Best hyperparameters are: '+str(grid_ert.best_params_))\n",
    "print('Best score is: '+str(grid_ert.best_score_))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "cbd39bc3",
   "metadata": {},
   "source": [
    "## Составлю таблицы с результатами обучения с оптимальными гиперпараметрами и с дефолтными параметрами"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 47,
   "id": "513995fb",
   "metadata": {},
   "outputs": [],
   "source": [
    "from xgboost import XGBClassifier\n",
    "from sklearn.neighbors import KNeighborsClassifier\n",
    "from sklearn.ensemble import RandomForestClassifier\n",
    "from sklearn import svm\n",
    "from sklearn.svm import SVC\n",
    "\n",
    "from sklearn.model_selection import cross_val_score\n",
    "import sklearn.metrics as metrics\n",
    "from sklearn.metrics import mean_absolute_error ,mean_squared_error, median_absolute_error,confusion_matrix,accuracy_score,r2_score\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "def Classifier_grid(x_train, y_train, x_test, y_test):\n",
    "\n",
    "    svmс = svm.SVC(C=0.001, gamma=4, kernel='rbf')\n",
    "    KN = KNeighborsClassifier(n_neighbors = 6)\n",
    "    XGB = XGBClassifier(learning_rate=0.0001, max_depth=1, min_child_weight=5, n_estimators=10)\n",
    "    RFC = RandomForestClassifier(bootstrap=False, max_features=1, min_samples_leaf=3, n_estimators=50, max_depth=1)\n",
    "    dtc = DecisionTreeClassifier(max_depth=1, max_features=1, min_samples_leaf=1)\n",
    "    ert = ExtraTreesClassifier(max_depth=1, max_features=1, min_samples_leaf=1)\n",
    "\n",
    "    logs = []\n",
    "\n",
    "\n",
    "    li = [KN,RFC,XGB,svmс,dtc,ert]\n",
    "    d = {}\n",
    "    for i in li:\n",
    "        i.fit(x_train, y_train)\n",
    "        \n",
    "        y_pred_test = i.predict(x_test)\n",
    "        y_pred_train = i.predict(x_train)\n",
    "        \n",
    "        log = {\"name\": i, \"score test\": i.score(x_test,y_test), \n",
    "               \"score train\": i.score(x_train,y_train),\n",
    "               \"MAE test\": metrics.mean_absolute_error(y_test, y_pred_test),\n",
    "               \"MAE train\": metrics.mean_absolute_error(y_train, y_pred_train),\n",
    "               \"RMSE test\": np.sqrt(metrics.mean_squared_error(y_test, y_pred_test)),\n",
    "               \"RMSE train\": np.sqrt(metrics.mean_squared_error(y_train, y_pred_train))}\n",
    "        logs.append(log)\n",
    "        print(i,\":\", i.score(x_test,y_test))\n",
    "    return logs "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 48,
   "id": "1e550c90",
   "metadata": {},
   "outputs": [],
   "source": [
    "from xgboost import XGBClassifier\n",
    "from sklearn.neighbors import KNeighborsClassifier\n",
    "from sklearn.ensemble import RandomForestClassifier\n",
    "from sklearn import svm\n",
    "from sklearn.svm import SVC\n",
    "\n",
    "from sklearn.model_selection import cross_val_score\n",
    "import sklearn.metrics as metrics\n",
    "from sklearn.metrics import mean_absolute_error ,mean_squared_error, median_absolute_error,confusion_matrix,accuracy_score,r2_score\n",
    "from sklearn.tree import DecisionTreeClassifier\n",
    "from sklearn.ensemble import ExtraTreesClassifier\n",
    "\n",
    "\n",
    "def Classifier(x_train, y_train, x_test, y_test):\n",
    "    \n",
    "    svmс = svm.SVC()\n",
    "    KNR = KNeighborsClassifier()\n",
    "    XGB = XGBClassifier()\n",
    "    RFC = RandomForestClassifier()\n",
    "    dtc = DecisionTreeClassifier()\n",
    "    ert = ExtraTreesClassifier()\n",
    "\n",
    "    logs = []\n",
    "    li = [KNR,RFC,XGB,svmс, dtc,ert]\n",
    "    d = {}\n",
    "    for i in li:\n",
    "        i.fit(x_train, y_train)\n",
    "        \n",
    "        y_pred_test = i.predict(x_test)\n",
    "        y_pred_train = i.predict(x_train)\n",
    "        \n",
    "        log = {\"name\": i, \"score test\": i.score(x_test,y_test), \n",
    "               \"score train\": i.score(x_train,y_train),\n",
    "               \"MAE test\": metrics.mean_absolute_error(y_test, y_pred_test),\n",
    "               \"MAE train\": metrics.mean_absolute_error(y_train, y_pred_train),\n",
    "               \"RMSE test\": np.sqrt(metrics.mean_squared_error(y_test, y_pred_test)),\n",
    "               \"RMSE train\": np.sqrt(metrics.mean_squared_error(y_train, y_pred_train))}\n",
    "        logs.append(log)\n",
    "        print(i,\":\", i.score(x_test,y_test))\n",
    "    return logs "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 49,
   "id": "f318f437",
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "KNeighborsClassifier() : 0.9694501018329938\n",
      "RandomForestClassifier() : 0.9674134419551935\n",
      "XGBClassifier(base_score=0.5, booster='gbtree', callbacks=None,\n",
      "              colsample_bylevel=1, colsample_bynode=1, colsample_bytree=1,\n",
      "              early_stopping_rounds=None, enable_categorical=False,\n",
      "              eval_metric=None, feature_types=None, gamma=0, gpu_id=-1,\n",
      "              grow_policy='depthwise', importance_type=None,\n",
      "              interaction_constraints='', learning_rate=0.300000012,\n",
      "              max_bin=256, max_cat_threshold=64, max_cat_to_onehot=4,\n",
      "              max_delta_step=0, max_depth=6, max_leaves=0, min_child_weight=1,\n",
      "              missing=nan, monotone_constraints='()', n_estimators=100,\n",
      "              n_jobs=0, num_parallel_tree=1, predictor='auto', random_state=0, ...) : 0.9613034623217923\n",
      "SVC() : 0.9694501018329938\n",
      "DecisionTreeClassifier() : 0.9287169042769857\n",
      "ExtraTreesClassifier() : 0.960285132382892\n"
     ]
    }
   ],
   "source": [
    "ml = Classifier(x_train, y_train, x_test, y_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 50,
   "id": "2f0ab056",
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "KNeighborsClassifier(n_neighbors=6) : 0.9694501018329938\n",
      "RandomForestClassifier(bootstrap=False, max_depth=1, max_features=1,\n",
      "                       min_samples_leaf=3, n_estimators=50) : 0.9694501018329938\n",
      "XGBClassifier(base_score=0.5, booster='gbtree', callbacks=None,\n",
      "              colsample_bylevel=1, colsample_bynode=1, colsample_bytree=1,\n",
      "              early_stopping_rounds=None, enable_categorical=False,\n",
      "              eval_metric=None, feature_types=None, gamma=0, gpu_id=-1,\n",
      "              grow_policy='depthwise', importance_type=None,\n",
      "              interaction_constraints='', learning_rate=0.0001, max_bin=256,\n",
      "              max_cat_threshold=64, max_cat_to_onehot=4, max_delta_step=0,\n",
      "              max_depth=1, max_leaves=0, min_child_weight=5, missing=nan,\n",
      "              monotone_constraints='()', n_estimators=10, n_jobs=0,\n",
      "              num_parallel_tree=1, predictor='auto', random_state=0, ...) : 0.9694501018329938\n",
      "SVC(C=0.001, gamma=4) : 0.9694501018329938\n",
      "DecisionTreeClassifier(max_depth=1, max_features=1) : 0.9694501018329938\n",
      "ExtraTreesClassifier(max_depth=1, max_features=1) : 0.9694501018329938\n"
     ]
    }
   ],
   "source": [
    "ml_grid = Classifier_grid(x_train, y_train, x_test, y_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 51,
   "id": "4c90b035",
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Model</th>\n",
       "      <th>Score(training)</th>\n",
       "      <th>Score(test)</th>\n",
       "      <th>MAE test</th>\n",
       "      <th>MAE train</th>\n",
       "      <th>RMSE test</th>\n",
       "      <th>RMSE train</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>KNeighbors classification</td>\n",
       "      <td>0.955414</td>\n",
       "      <td>0.969450</td>\n",
       "      <td>0.030550</td>\n",
       "      <td>0.044586</td>\n",
       "      <td>0.174785</td>\n",
       "      <td>0.211154</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>RandomForest classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.967413</td>\n",
       "      <td>0.032587</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.180517</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>XGB classification</td>\n",
       "      <td>0.997962</td>\n",
       "      <td>0.961303</td>\n",
       "      <td>0.038697</td>\n",
       "      <td>0.002038</td>\n",
       "      <td>0.196714</td>\n",
       "      <td>0.045147</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>SVC classification</td>\n",
       "      <td>0.955159</td>\n",
       "      <td>0.969450</td>\n",
       "      <td>0.030550</td>\n",
       "      <td>0.044841</td>\n",
       "      <td>0.174785</td>\n",
       "      <td>0.211756</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Decision Tree classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.928717</td>\n",
       "      <td>0.071283</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.266989</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>Extra Trees classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.960285</td>\n",
       "      <td>0.039715</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.199286</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                          Model  Score(training)  Score(test)  MAE test  \\\n",
       "0     KNeighbors classification         0.955414     0.969450  0.030550   \n",
       "1   RandomForest classification         1.000000     0.967413  0.032587   \n",
       "2            XGB classification         0.997962     0.961303  0.038697   \n",
       "3            SVC classification         0.955159     0.969450  0.030550   \n",
       "4  Decision Tree classification         1.000000     0.928717  0.071283   \n",
       "5    Extra Trees classification         1.000000     0.960285  0.039715   \n",
       "\n",
       "   MAE train  RMSE test  RMSE train  \n",
       "0   0.044586   0.174785    0.211154  \n",
       "1   0.000000   0.180517    0.000000  \n",
       "2   0.002038   0.196714    0.045147  \n",
       "3   0.044841   0.174785    0.211756  \n",
       "4   0.000000   0.266989    0.000000  \n",
       "5   0.000000   0.199286    0.000000  "
      ]
     },
     "execution_count": 51,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "def regr_result(l):\n",
    "    models = [('KNeighbors classification', l[0]['score train'], l[0]['score test'],  l[0]['MAE test'], l[0]['MAE train'], l[0]['RMSE test'], l[0]['RMSE train']),\n",
    "              ('RandomForest classification',  l[1]['score train'], l[1]['score test'],  l[1]['MAE test'], l[1]['MAE train'], l[1]['RMSE test'], l[1]['RMSE train']),\n",
    "              ('XGB classification',  l[2]['score train'], l[2]['score test'], l[2]['MAE test'], l[2]['MAE train'], l[2]['RMSE test'], l[2]['RMSE train']),\n",
    "              ('SVC classification',  l[3]['score train'], l[3]['score test'], l[3]['MAE test'], l[3]['MAE train'], l[3]['RMSE test'], l[3]['RMSE train']),\n",
    "              ('Decision Tree classification', l[4]['score train'], l[4]['score test'], l[4]['MAE test'], l[4]['MAE train'], l[4]['RMSE test'], l[4]['RMSE train']),\n",
    "              ('Extra Trees classification', l[5]['score train'], l[5]['score test'], l[5]['MAE test'], l[5]['MAE train'], l[5]['RMSE test'], l[5]['RMSE train'])]\n",
    "    predict = pd.DataFrame(data = models, columns=['Model', 'Score(training)', 'Score(test)', 'MAE test', 'MAE train', 'RMSE test', 'RMSE train'])\n",
    "    return predict\n",
    "resultML=regr_result(ml)\n",
    "resultML"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 52,
   "id": "55ab3fa6",
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Model</th>\n",
       "      <th>Score(training)</th>\n",
       "      <th>Score(test)</th>\n",
       "      <th>MAE test</th>\n",
       "      <th>MAE train</th>\n",
       "      <th>RMSE test</th>\n",
       "      <th>RMSE train</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>KNeighbors classification</td>\n",
       "      <td>0.955924</td>\n",
       "      <td>0.96945</td>\n",
       "      <td>0.03055</td>\n",
       "      <td>0.044076</td>\n",
       "      <td>0.174785</td>\n",
       "      <td>0.209944</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>RandomForest classification</td>\n",
       "      <td>0.954650</td>\n",
       "      <td>0.96945</td>\n",
       "      <td>0.03055</td>\n",
       "      <td>0.045350</td>\n",
       "      <td>0.174785</td>\n",
       "      <td>0.212956</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>XGB classification</td>\n",
       "      <td>0.954650</td>\n",
       "      <td>0.96945</td>\n",
       "      <td>0.03055</td>\n",
       "      <td>0.045350</td>\n",
       "      <td>0.174785</td>\n",
       "      <td>0.212956</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>SVC classification</td>\n",
       "      <td>0.954650</td>\n",
       "      <td>0.96945</td>\n",
       "      <td>0.03055</td>\n",
       "      <td>0.045350</td>\n",
       "      <td>0.174785</td>\n",
       "      <td>0.212956</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Decision Tree classification</td>\n",
       "      <td>0.954650</td>\n",
       "      <td>0.96945</td>\n",
       "      <td>0.03055</td>\n",
       "      <td>0.045350</td>\n",
       "      <td>0.174785</td>\n",
       "      <td>0.212956</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>Extra Trees classification</td>\n",
       "      <td>0.954650</td>\n",
       "      <td>0.96945</td>\n",
       "      <td>0.03055</td>\n",
       "      <td>0.045350</td>\n",
       "      <td>0.174785</td>\n",
       "      <td>0.212956</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                          Model  Score(training)  Score(test)  MAE test  \\\n",
       "0     KNeighbors classification         0.955924      0.96945   0.03055   \n",
       "1   RandomForest classification         0.954650      0.96945   0.03055   \n",
       "2            XGB classification         0.954650      0.96945   0.03055   \n",
       "3            SVC classification         0.954650      0.96945   0.03055   \n",
       "4  Decision Tree classification         0.954650      0.96945   0.03055   \n",
       "5    Extra Trees classification         0.954650      0.96945   0.03055   \n",
       "\n",
       "   MAE train  RMSE test  RMSE train  \n",
       "0   0.044076   0.174785    0.209944  \n",
       "1   0.045350   0.174785    0.212956  \n",
       "2   0.045350   0.174785    0.212956  \n",
       "3   0.045350   0.174785    0.212956  \n",
       "4   0.045350   0.174785    0.212956  \n",
       "5   0.045350   0.174785    0.212956  "
      ]
     },
     "execution_count": 52,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "resultML_GRIDD = regr_result(ml_grid)\n",
    "resultML_GRIDD"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "0005ce51",
   "metadata": {},
   "source": [
    "Из приведенных выше таблиц видно, что подбор параметров позволил улучшить данные на тестовой выборке. Помимо этого подбор гиперпараметров позволил избавиться от переобучения в Random Forest, Decision Tree и Extra Trees classifications"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "4ca142c0",
   "metadata": {},
   "source": [
    "###### *Однако, меня смущают совпадение RMSE, MEA Score(test) после подбора гиперпараметров. Я пыталась играться с разными пармаметрами, но это не привело к сильному изменению Score(test). Если у Вас будет комментарий по этому моменту - буду благодарна. "
   ]
  },
  {
   "cell_type": "markdown",
   "id": "21eb8758",
   "metadata": {},
   "source": [
    "# 8. Классификация с помощью нейронной сети"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 53,
   "id": "268c75b1",
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.neural_network import MLPClassifier\n",
    "from sklearn.metrics import accuracy_score"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "68ebde9f",
   "metadata": {},
   "source": [
    "## Подбор оптимального параметра alpha (1 слой и 100 нейронов)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 54,
   "id": "1bbf0efd",
   "metadata": {},
   "outputs": [],
   "source": [
    "def training(x_train, x_test, y_train, y_test , test_err, train_err, train_acc, test_acc, HiddenLayerSizes, AlphaArr):\n",
    "\n",
    "    for alpha in alpha_arr:\n",
    "        mlp_model = MLPClassifier(hidden_layer_sizes, alpha = alpha, solver = 'lbfgs', activation = 'logistic', \n",
    "                                  max_iter=10000, random_state = 73)\n",
    "        mlp_model.fit(x_train, y_train)\n",
    "\n",
    "        y_train_pred = mlp_model.predict(x_train)\n",
    "        y_test_pred = mlp_model.predict(x_test)\n",
    "\n",
    "        train_err.append(1 - mlp_model.score(x_train, y_train))\n",
    "        test_err.append(1 - mlp_model.score(x_test, y_test))\n",
    "        \n",
    "        train_acc.append(accuracy_score(y_train, y_train_pred))\n",
    "        test_acc.append(accuracy_score(y_test, y_test_pred))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 55,
   "id": "b1eb7f31",
   "metadata": {},
   "outputs": [],
   "source": [
    "test_err = []\n",
    "train_err = []\n",
    "train_acc = []\n",
    "test_acc = []  \n",
    "\n",
    "hidden_layer_sizes = (100,)\n",
    "alpha_arr = np.logspace(-3, 2, 21)\n",
    "\n",
    "training(x_train, x_test, y_train, y_test , test_err, train_err, train_acc, test_acc, hidden_layer_sizes, alpha_arr)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "50c4d5e8",
   "metadata": {},
   "source": [
    "##### Посмотрим, как меняется ошибка в зависимости от гиперпараметра:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 56,
   "id": "1320b126",
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.legend.Legend at 0x22eb5aaee20>"
      ]
     },
     "execution_count": 56,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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+eOPPzBmzBi0b98eHh4e8PX1BQBkZmZWuE1QUJDufePGjXHPPfcgPT1dV+bu7q5LlgCgZcuWuHTpku7zpUuXEBYWhrvvvhuenp7w9PTE9evXKz0mETkWtjARkV0ZMmQIfHx8sHLlSrRq1QolJSXo2rUrCgsLq7QflUqle+/s7FzuOyGE7vOECRNw+fJlREdHo23btnB1dUVQUFCVj0lE9osJExHZjStXriA9PR2ffPIJgoODAQA//vij0e1++ukntGnTBgDw999/49SpU+jUqZPJx01OTkZMTAwGDRoEAMjKykJubm41zoCI7BUTJiKyG40aNUKTJk3w6aefomXLlsjMzMTMmTONbjd//nw0adIEXl5emD17Npo2bYqhQ4eafNyOHTvi888/R2BgIPLz8/H666+jbt26NTgTIrI3HMNERHajTp062Lx5M44cOYKuXbsiIiICixcvNrrdu+++i6lTpyIgIADZ2dnYsWMHXFxcTD7u6tWr8ffff+Pee+/F2LFjMWXKFDRv3rwmp0JEdkYlSnfUExE5kL179+Lhhx/G33//zeVPiKhG2MJEREREZAQTJiIiIiIj2CVHREREZARbmIiIiIiMYMJEREREZAQTJiIiIiIjmDARERERGcGEiYiIiMgIJkxERERERjBhIiIiIjKCCRMRERGREf8Pyux7Q7zVAVwAAAAASUVORK5CYII=\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.semilogx(alpha_arr, train_err, 'b-o', label = 'train')\n",
    "plt.semilogx(alpha_arr, test_err, 'r-o', label = 'test')\n",
    "plt.xlim([np.min(alpha_arr), np.max(alpha_arr)])\n",
    "plt.title('Error vs. alpha')\n",
    "plt.xlabel('alpha')\n",
    "plt.ylabel('error')\n",
    "plt.legend()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "07f68bbe",
   "metadata": {},
   "source": [
    "##### Как меняется качество модели в зависимости от гиперпараметра:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 57,
   "id": "5c462cf9",
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.legend.Legend at 0x22eb5a5e9d0>"
      ]
     },
     "execution_count": 57,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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YSIiIiKqABMmIiIiogowYSIiIiKqABMmIiIiogowYSIiIiKqABMmIiIiogowYSIiu3H27FmoVCocO3bM6PesXr0aderUMVtMRGQfmDARERERVYAJExEREVEFmDARkU3ZuXMnunXrhjp16qBevXro168f/vzzT4Nl9+7dC5VKhW+//RZt2rSBi4sLQkND8euvv5Yqu2vXLgQFBaF27dp45JFHkJmZqXvt8OHD6NmzJ7y9veHp6YmHHnoIP//8s9mukYisDxMmIrIpN27cwJQpU3D48GHs2bMHDg4OGDx4MIqLi8t8zyuvvIIPPvgAhw8fRoMGDTBgwAAUFhbqXr958yY++OADrFu3Dvv370daWhpefvll3evXrl3DmDFjkJiYiJ9++gn33Xcf+vTpg2vXrpn1WonIejgqHQARUWUMHTpU7/nKlSvRoEEDpKSkoHbt2gbfM2PGDPTs2RMAsGbNGvj6+mLLli147LHHAACFhYX49NNPcc899wAAnn/+eURHR+ve//DDD+sdb+nSpfDy8sK+ffvQr18/k10bEVkv1jARkU35888/MXLkSDRr1gweHh5o2rQpACAtLa3M93Tu3Fn3uG7dumjRogV+++033T43NzddsgQAjRo1wsWLF3XPL168iAkTJqB58+bw9PSEp6cnrl+/Xu45ici+sIaJiGxK//794efnh+XLl6Nx48YoLi5GcHAwCgoKKnUclUqle6zRaEq9JoTQPR87diwuXbqEBQsWICAgAM7OzujcuXOlz0lEtosJExHZjMuXL+O3337D0qVLERYWBgD44YcfKnzfTz/9BH9/fwDAlStXcPr0abRs2dLo8yYmJmLx4sXo06cPACA9PR3Z2dlVuAIislVMmIjIZnh5eaFevXpYtmwZGjVqhLS0NEybNq3C90VHR6NevXrw8fHB66+/Dm9vbwwaNMjo8957771Yt24dOnTogNzcXLzyyitwdXWtxpUQka1hHyYishkODg6IjY1FcnIygoOD8eKLL2Lu3LkVvu+9997D5MmTERISgszMTGzduhVOTk5GnzcmJgZXrlxBu3btMGrUKEyaNAkNGjSozqUQkY1RiTsb6omI7MjevXsRHh6OK1eucPkTIqoW1jARERERVYAJExEREVEF2CRHREREVAHWMBERERFVgAkTERERUQWYMBERERFVgAkTERERUQWYMBERERFVgAkTERERUQWYMBERERFVgAkTERERUQX+H4L15G0MQj10AAAAAElFTkSuQmCC\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.semilogx(alpha_arr, train_acc, 'r-o', label = 'train')\n",
    "plt.semilogx(alpha_arr, test_acc, 'b-o', label = 'test')\n",
    "plt.xlim([np.min(alpha_arr), np.max(alpha_arr)])\n",
    "plt.title('Accuracy vs. alpha')\n",
    "plt.xlabel('alpha')\n",
    "plt.ylabel('Accuracy')\n",
    "plt.legend()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "9a8fd248",
   "metadata": {},
   "source": [
    "По данной картинке видно, что при изменениии alpha точность на обучающей выборке изменяется от 1 до ~0.95 т.е при маленьких значениях альфы у нас происходило переобучение"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "0915077e",
   "metadata": {},
   "source": [
    "##### Минимальное значение ошибки:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 58,
   "id": "3e564240",
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "ERR train =  0.0 \t ERR test =  0.03054989816700615\n",
      "score train =  1.0 \t score test =  0.9694501018329938\n"
     ]
    }
   ],
   "source": [
    "print('ERR train = ', np.min(train_err), '\\t', 'ERR test = ', np.min(test_err))\n",
    "print('score train = ', 1-np.min(train_err), '\\t', 'score test = ', 1-np.min(test_err))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "23e9587a",
   "metadata": {},
   "source": [
    "##### Оптимальное значение alpha:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 59,
   "id": "d550453d",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Оптимальное значение параметра:  1.7782794100389228\n"
     ]
    }
   ],
   "source": [
    "alpha_opt = alpha_arr[test_err == np.min(test_err)]\n",
    "alpha_opt = alpha_opt[0]\n",
    "\n",
    "print(\"Оптимальное значение параметра: \", alpha_opt)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "a3fa0546",
   "metadata": {},
   "source": [
    "##### Повторим обучение при найденном оптимальном значении alpha:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 60,
   "id": "90a5b648",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " Ошибка на обучающей выборке:  0.04509554140127392 \n",
      " Ошибка на тестовой выборке:  0.03054989816700615\n"
     ]
    }
   ],
   "source": [
    "mlp_model = MLPClassifier(alpha = alpha_opt, hidden_layer_sizes = (100,),\n",
    "                          solver = 'lbfgs', activation = 'logistic', random_state = 73)\n",
    "mlp_model.fit(x_train, y_train)\n",
    "\n",
    "y_train_pred = mlp_model.predict(x_train)\n",
    "y_test_pred = mlp_model.predict(x_test)\n",
    "\n",
    "print(\" Ошибка на обучающей выборке: \", 1 - mlp_model.score(x_train, y_train), '\\n',\n",
    "      \"Ошибка на тестовой выборке: \",1 - mlp_model.score(x_test, y_test))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "68398326",
   "metadata": {},
   "source": [
    "## Подбор оптимального числа нейронов на первом слое при ранее найденном alpha"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 61,
   "id": "797286e5",
   "metadata": {},
   "outputs": [],
   "source": [
    "alpha_arr = np.linspace(1, 101, 50).astype(int)\n",
    "test_err = []\n",
    "train_err = []\n",
    "train_acc = []\n",
    "test_acc = []\n",
    "\n",
    "for alpha in alpha_arr:\n",
    "    mlp_model = MLPClassifier(alpha = alpha_opt, hidden_layer_sizes = (alpha,), \n",
    "                              solver = 'lbfgs', activation = 'logistic', max_iter=1000, random_state = 73)\n",
    "    mlp_model.fit(x_train, y_train)\n",
    "\n",
    "    y_train_pred = mlp_model.predict(x_train)\n",
    "    y_test_pred = mlp_model.predict(x_test)\n",
    "    \n",
    "    train_err.append(1 - mlp_model.score(x_train, y_train))\n",
    "    test_err.append(1 - mlp_model.score(x_test, y_test))\n",
    "    train_acc.append(accuracy_score(y_train, y_train_pred))\n",
    "    test_acc.append(accuracy_score(y_test, y_test_pred))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 62,
   "id": "e33aa107",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.legend.Legend at 0x22ebc7bbb50>"
      ]
     },
     "execution_count": 62,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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Hh6OJUuWqFLepEmTcOnSJezcuVP2Nq+//jr++c9/IicnB66urrh06ZKiuh16nqgePXrgp59+alDFREREZMWOHUDXrsB99wFPPin927WrlN7MlZeX4/HHH8dzzz2ndVNkURREvf7665g9ezZ2796NgoICTkJJRESkhh07gMceA86fN0+/cEFKt1MgNWnSJGRkZODdd9+FTqeDTqfD2bNn8f333yM2NhZt27aFn58fxo8fj+LiYtN2H330EXr06AEPDw94e3vjwQcfxNWrV/HKK6/gww8/xCeffGIq74svvqi3HQsXLsSsWbPQo0cPu/RTbYoGlj/00EMAgBEjRpgNJDfO8WQwGNRpHRERUVMmBHDtmry8BgMwY4a0jbVydDpg5kzgwQfl3dpr3VraRoZ3330Xp0+fRlhYGJKTk//XHAMGDhyIKVOm4O2338b169eRlJSEJ554Ap9//jkKCgowduxYLF68GI8++iguX76MgwcPQgiB2bNnIzc3F6WlpVi3bh0ANHgctSNSFEQdOHBA7XYQERE1P9euAW3bqlOWENIVKk9PefmvXAFumoKoNp6ennB1dUXr1q3h7+8PAHj55ZcRERGBRYsWmfJ98MEHCAoKwunTp3HlyhVUVlZi1KhRpgfCal5B8vDwQFlZmam85kjxb+e1atUKa9aswQsvvIBu3bph4MCByMvLg5OdB74RERGR/WVlZeHAgQNo27ataQkNDQUA/Pjjj+jVqxceeOAB9OjRA48//jjWrFmD33//XeNWNy5FQdT27dsxZMgQeHh4IDs72zSR5eXLl80iViIiohatdWvpipCcJS1NXplpafLKa926QU2vqqrC8OHDkZOTY7b88MMPGDBgAJycnJCeno7PPvsMd911F5YtW4Y777wTZ86caVC9TYmiIOq1117DqlWrsGbNGrOZwvv164d///vfqjWOiIioSdPppFtqcpaYGKBz59rHMel0QFCQlE9OeTb+xq2rq6vZmOaIiAicPHkSXbt2Rbdu3cwW4y+V6HQ69O/fHwsXLkR2djZcXV3x8ccfWy2vOVIURJ06dQoDBgywSG/fvr3iOR2IiIhaNCcn4N13pf/fHAAZXy9ZYrf5orp27YpvvvkGZ8+eRXFxMaZNm4bffvsNY8eOxZEjR/DTTz9h7969mDx5MgwGA7755hssWrQIR48eRV5eHnbs2IFf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\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.plot(alpha_arr, train_err, 'b-o', label = 'train_1')\n",
    "plt.plot(alpha_arr, test_err, 'r-o', label = 'test_1')\n",
    "plt.xlim([np.min(alpha_arr), np.max(alpha_arr)])\n",
    "plt.title('Error vs. neurons')\n",
    "plt.xlabel('neurons')\n",
    "plt.ylabel('error')\n",
    "plt.legend()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 63,
   "id": "b90391d4",
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.legend.Legend at 0x22ebc811d60>"
      ]
     },
     "execution_count": 63,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAlEAAAHFCAYAAADSY6wWAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjUuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8qNh9FAAAACXBIWXMAAA9hAAAPYQGoP6dpAABtEElEQVR4nO3dfVxUVf4H8M8wDE8KiCKIgmCbDxhpCoRCtZqJqZj2qG1pZmtZpKDbppTmyq+kNF3zCUVFsfIhTTcr3KQ0H2I3gtQyFSw1SEHCFDQNcDi/P+7OwDgDzFwu3AE+79frvnTunHvOuQ8z8+Xcc87VCCEEiIiIiMgmDmpXgIiIiKg5YhBFREREJAODKCIiIiIZGEQRERERycAgioiIiEgGBlFEREREMjCIIiIiIpKBQRQRERGRDAyiiIiIiGRgEEXUQi1duhQajQYhISFqV4WIqEViEEXUQqWmpgIAfvjhB3z99dcq14aIqOVhEEXUAmVnZ+Po0aMYOXIkAGDdunUq16h2165dU7sKZMH169fVrgKR3WMQRdQCGYKmN998E5GRkdiyZYvFYOXcuXN49tlnERAQACcnJ3Tu3BmPPPIILly4YExz+fJl/O1vf8Mtt9wCZ2dn+Pj4YMSIETh58iQA4Msvv4RGo8GXX35pkvfZs2eh0WiwYcMG47qJEyeibdu2+P777xEdHQ13d3cMGTIEAJCRkYHRo0fD398fLi4uuPXWW/Hcc8+hpKTErN4nT57E448/Dl9fXzg7O6Nr166YMGECysvLcfbsWTg6OiIpKclsuwMHDkCj0WDbtm0Wj9uvv/4KJycnzJkzx2KZGo0GS5cuBSAFfy+99BK6desGFxcXtG/fHmFhYdi8ebPFvOtiOFZvv/02Fi9ejG7duqFt27YYOHAg/vvf/5qlz87OxgMPPID27dvDxcUF/fr1wwcffGCS5h//+Ac0Go3Zths2bIBGo8HZs2eN64KCghATE4MdO3agX79+cHFxwbx58wAAx44dw+jRo+Hl5QUXFxfccccdSEtLM8nTcA1s3rwZr776Kjp37gwPDw/cd999yM3Ntfl4EDUXjmpXgIiUdf36dWzevBnh4eEICQnBpEmT8Ne//hXbtm3DU089ZUx37tw5hIeHo7KyEq+88gr69OmDixcv4rPPPsOlS5fg6+uLK1eu4K677sLZs2cxc+ZMRERE4OrVqzhw4AAKCwvRq1cvm+tXUVGBBx54AM899xxmzZqFGzduAAB++uknDBw4EH/961/h6emJs2fPYvHixbjrrrvw/fffQ6fTAQCOHj2Ku+66C97e3khMTET37t1RWFiIXbt2oaKiAkFBQXjggQewatUqvPzyy9Bqtcayly9fjs6dO+PBBx+0WLeOHTsiJiYGaWlpmDdvHhwcqv/OXL9+PZycnPDEE08AAGbMmIF3330Xr7/+Ovr164fff/8dx44dw8WLF20+JgYrVqxAr169sGTJEgDAnDlzMGLECJw5cwaenp4AgH379uH+++9HREQEVq1aBU9PT2zZsgVjx47FtWvXMHHiRFllf/vttzhx4gRmz56Nbt26oU2bNsjNzUVkZCR8fHywdOlSdOjQAe+99x4mTpyICxcu4OWXXzbJ45VXXkFUVBTWrl2LsrIyzJw5E6NGjcKJEydMzgNRiyGIqEXZuHGjACBWrVolhBDiypUrom3btuLuu+82STdp0iSh0+nE8ePHa80rMTFRABAZGRm1ptm3b58AIPbt22ey/syZMwKAWL9+vXHdU089JQCI1NTUOvehqqpKVFZWip9//lkAEB999JHxvXvvvVe0a9dOFBcX11unnTt3GtedO3dOODo6innz5tVZ9q5duwQAsWfPHuO6GzduiM6dO4uHH37YuC4kJESMGTOmzrysZThWt99+u7hx44ZxfVZWlgAgNm/ebFzXq1cv0a9fP1FZWWmSR0xMjPDz8xN6vV4IIcTcuXOFpa/49evXCwDizJkzxnWBgYFCq9WK3Nxck7Tjxo0Tzs7OIj8/32T98OHDhZubm7h8+bIQovp4jxgxwiTdBx98IACI//znPzYcDaLmg7fziFqYdevWwdXVFePGjQMAtG3bFo8++igOHjyIU6dOGdPt3r0bgwcPRnBwcK157d69Gz169MB9992naB0ffvhhs3XFxcWYMmUKAgIC4OjoCJ1Oh8DAQADAiRMnAEi30Pbv34/HHnsMHTt2rDX/QYMGoW/fvlixYoVx3apVq6DRaPDss8/WWbfhw4ejU6dOWL9+vXHdZ599hvPnz2PSpEnGdXfeeSd2796NWbNm4csvv1SkD9HIkSNNWmz69OkDAPj5558BAD/++CNOnjxpbA27ceOGcRkxYgQKCwtl3z7r06cPevToYbJu7969GDJkCAICAkzW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hjlz5uCFF15AcXExOnfujOeeew6vvfZak+07ERERNW987ItMnCeKiIio+WkR80QRERERNWcMooiIiIhkYBBFREREJAODKCIiIiIZGEQRERERycAgioiIiEgGBlFEREREMjCIIiIiIpKBQRQRERGRDAyiiIiIiGRgEEVEREQkA4MoIiIiIhkYRBERERHJwCCKiIiISAYGUUREREQyMIgiIiIikoFBFBEREZEMDKKIiIiIZGAQRURERCQDgygiIiIiGRhEEREREcnAIIqIiIhIBgZRRERERDIwiCIiIiKSgUEUERERkQwMooiIiIhkYBBFREREJAODKCIiIiIZGEQRERERycAgioiIiEgGBlFEREREMjCIIiIiIpKBQRQRERGRDAyiiIiIiGRQPYhauXIlunXrBhcXF4SGhuLgwYN1pl+xYgWCg4Ph6uqKnj17YuPGjWZpLl++jNjYWPj5+cHFxQXBwcFIT083SXPu3Dk8+eST6NChA9zc3HDHHXcgJydH0X0jIiKilstRzcK3bt2K+Ph4rFy5ElFRUVi9ejWGDx+O48ePo2vXrmbpk5OTkZCQgDVr1iA8PBxZWVmYPHkyvLy8MGrUKABARUUFhg4dCh8fH2zfvh3+/v4oKCiAu7u7MZ9Lly4hKioKgwcPxu7du+Hj44OffvoJ7dq1a6pdJyIiomZOI4QQahUeERGB/v37Izk52bguODgYY8aMQVJSkln6yMhIREVFYeHChcZ18fHxyM7OxqFDhwAAq1atwsKFC3Hy5EnodDqL5c6aNQtfffVVva1edSkrK4OnpydKS0vh4eEhOx8iIiJqOkr+fqt2O6+iogI5OTmIjo42WR8dHY3MzEyL25SXl8PFxcVknaurK7KyslBZWQkA2LVrFwYOHIjY2Fj4+voiJCQE8+fPh16vN26za9cuhIWF4dFHH4WPjw/69euHNWvW1Fnf8vJylJWVmSxERETUeqkWRJWUlECv18PX19dkva+vL4qKiixuM2zYMKxduxY5OTkQQiA7OxupqamorKxESUkJAOD06dPYvn079Ho90tPTMXv2bCxatAhvvPGGMZ/Tp08jOTkZ3bt3x2effYYpU6Zg2rRpFvtXGSQlJcHT09O4BAQEKHAUiIiIqLlStU8UAGg0GpPXQgizdQZz5sxBUVERBgwYACEEfH19MXHiRCxYsABarRYAUFVV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0qUL4uLiMHPmzKbePSIiImrBVJ0nqjnjPFFERETNT4uYJ4qIiIioOWMQRURERCQDgygiIiIiGRhEEREREcnAIIqIiIhIBgZRRERERDIwiCIiIiKSgUEUERERkQwMooiIiIhksDmICgoKQmJiosnjWIiIiIhaG5uDqL/97W/46KOPcMstt2Do0KHYsmULysvLG6NuRERERHbL5iBq6tSpyMnJQU5ODnr37o1p06bBz88PL774Ir799tvGqCMRERGR3WnwA4grKyuxcuVKzJw5E5WVlQgJCUFcXByefvppaDQapeppd/gAYiIiouZHyd9vR7kbVlZWYufOnVi/fj0yMjIwYMAAPPPMMzh//jxeffVVfP7559i0aVODKkdERERkr2wOor799lusX78emzdvhlarxfjx4/HPf/4TvXr1MqaJjo7GPffco2hFiYiIWouqqipUVFSoXY1mSafTQavVNklZNgdR4eHhGDp0KJKTkzFmzBjodDqzNL1798a4ceMUqSAREVFrUlFRgTNnzqCqqkrtqjRb7dq1Q6dOnRq9W5HNQdTp06cRGBhYZ5o2bdpg/fr1sitFRETUGgkhUFhYCK1Wi4CAADg4cDpHWwghcO3aNRQXFwMA/Pz8GrU8m4Oo4uJiFBUVISIiwmT9119/Da1Wi7CwMMUqR0RE1JrcuHED165dQ+fOneHm5qZ2dZolV1dXAFK84uPj06i39mwOcWNjY1FQUGC2/ty5c4iNjVWkUkRERK2RXq8HADg5Oalck+bNEIBWVlY2ajk2B1HHjx9H//79zdb369cPx48fV6RSRERErVlLniKoKTTV8bM5iHJ2dsaFCxfM1hcWFsLRUfaMCURERETNis1B1NChQ5GQkIDS0lLjusuXL+OVV17B0KFDFa0cERERtT5BQUFYsmSJ2tWol81NR4sWLcI999yDwMBA9OvXDwBw5MgR+Pr64t1331W8gkRERGQjvR44eBAoLAT8/IC77wYaee6kQYMG4Y477lAk+Pnmm2/Qpk2bhleqkdkcRHXp0gXfffcd3n//fRw9ehSurq54+umn8fjjj1ucM4qIiIia0I4dQFwc8Msv1ev8/YF33gEeeki1agkhoNfrrer607FjxyaoUcPJmoCiTZs2ePbZZ7FixQq8/fbbmDBhAgMoIiIite3YATzyiGkABQDnzknrd+xolGInTpyI/fv345133oFGo4FGo8GGDRug0Wjw2WefISwsDM7Ozjh48CB++uknjB49Gr6+vmjbti3Cw8Px+eefm+R38+08jUaDtWvX4sEHH4Sbmxu6d++OXbt2Ncq+2EJ2T/Djx48jPz/fbFr6Bx54oMGVIiIiIgBCANeuWZdWrwemTZO2sZSPRiO1UN13n3W39tzcpG2s8M477yAvLw8hISFITEwEAPzwww8AgJdffhlvv/02brnlFrRr1w6//PILRowYgddffx0uLi5IS0vDqFGjkJubi65du9Zaxrx587BgwQIsXLgQy5YtwxNPPIGff/4Z7du3t6qOjUHWjOUPPvggvv/+e2g0Goj/nSzDcELDHBdERETUQNeuAW3bKpOXEFILlaendemvXgWs7Jfk6ekJJycnuLm5oVOnTgCAkydPAgASExNNBp516NABffv2Nb5+/fXXsXPnTuzatQsvvvhirWVMnDgRjz/+OABg/vz5WLZsGbKysnD//fdbtz+NwObbeXFxcejWrRsuXLgANzc3/PDDDzhw4ADCwsLw5ZdfNkIViYiIqLm6+Ukmv//+O15++WX07t0b7dq1Q9u2bXHy5Enk5+fXmU+fPn2M/2/Tpg3c3d2Nj3dRi80tUf/5z3+wd+9edOzYEQ4ODnBwcMBdd92FpKQkTJs2DYcPH26MehIREbU+bm5Si5A1DhwARoyoP116OnDPPdaVrYCbR9n9/e9/x2effYa3334bt956K1xdXfHII4+YdQ+62c19rzUajeoPabY5iNLr9Wj7v6ZFb29vnD9/Hj179kRgYCByc3MVryAREVGrpdFYfUsN0dHSKLxz5yz3i9JopPejoxtlugMnJyeruvQcPHgQEydOxIMPPggAuHr1Ks6ePat4fZqCzbfzQkJC8N133wEAIiIisGDBAnz11VdITEzELbfcongFiYiIyAparTSNAWDeIdzwesmSRpsvKigoCF9//TXOnj2LkpKSWluJbr31VuzYsQNHjhzB0aNH8Ze//EX1FiW5bA6iZs+ebdzZ119/HT///DPuvvtupKenY+nSpYpXkIiIiKz00EPA9u1Aly6m6/39pfWNOE/USy+9BK1Wi969e6Njx4619nH65z//CS8vL0RGRmLUqFEYNmyYxWfyNgcaISy1+dnmt99+g5eXV6t6YGJZWRk8PT1RWloKDw8PtatDREQtwB9/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qsTcuXNFp06dhLOzs7jnnnvE999/r16lW4mbgyieh6b18ccfi5CQEOHs7Cx69eolUlJSTN7n+WgaZWVlIi4uTnTt2lW4uLiIW265Rbz66quivLzcmIbnonHs27fP4u/DU089JYSw7rhfv35dvPjii6J9+/bC1dVVxMTEiPz8fJvrohFCCNntZkREREStFPtEEREREcnAIIqIiIhIBgZRRERERDIwiCIiIiKSgUEUERERkQwMooiIiIhkYBBFREREJAODKCIiIiIZGEQRERERycAgiojIBhUVFWpXgYjsBIMoImq2Bg0ahGnTpuHll19G+/bt0alTJ/zjH/8wvl9aWopnn30WPj4+8PDwwL333oujR48a3584cSLGjBljkmd8fDwGDRpkUsaLL76IGTNmwNvbG0OHDgUA7N+/H3feeSecnZ3h5+eHWbNm4caNG1bXjYiaPwZRRNSspaWloU2bNvj666+xYMECJCYmIiMjA0IIjBw5EkVFRUhPT0dOTg769++PIUOG4LfffrO5DEdHR3z11VdYvXo1zp07hxEjRiA8PBxHjx5FcnIy1q1bh9dff92quhFRy+CodgWIiBqiT58+mDt3LgCge/fuWL58Ob744gtotVp8//33KC4uhrOzMwDg7bffxr/+9S9s374dzz77rNVl3HrrrViwYIHx9auvvoqAgAAsX74cGo0GvXr1wvnz5zFz5ky89tprcHBwqLNuhtYsImreGEQRUbPWp08fk9d+fn4oLi5GTk4Orl69ig4dOpi8f/36dfz00082lREWFmby+sSJExg4cCA0Go1xXVRUFK5evYpffvkFXbt2rbNuRNQyMIgiomZNp9OZvNZoNKiqqkJVVRX8/Pzw5Zdfmm3Trl07AICDgwOEECbvVVZWmqVv06aNyWshhEkAZVhnKL++uhFRy8AgiohapP79+6OoqAiOjo4ICgqymKZjx444duyYybojR46YBT836927Nz788EOTYCozMxPu7u7o0qWLIvUnIvvHjuVE1CLdd999GDhwIMaMGYPPPvsMZ8+eRWZmJmbPno3s7GwAwL333ovs7Gxs3LgRp06dwty5c82CKkteeOEFFBQUYOrUqTh58iQ++ugjzJ07FzNmzDD2hyKilo+fdiJqkTQaDdLT03HPPfdg0qRJ6NGjB8aNG4ezZ8/C19cXADBs2DDMmTMHL7/8MsLDw3HlyhVMmDCh3ry7dOmC9PR0ZGVloW/fvpgyZQqeeeYZzJ49u7F3i4jsiEbc3CGAiIiIiOrFligiIiIiGRhEEREREcnAIIqIiIhIBgZRRERERDIwiCIiIiKSgUEUERERkQwMooiIiIhkYBBFREREJAODKCIiIiIZGEQRERERycAgioiIiEgGBlFEREREMvw/WOSgVpmymHoAAAAASUVORK5CYII=\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.plot(alpha_arr, train_acc, 'r-o', label = 'train')\n",
    "plt.plot(alpha_arr, test_acc, 'b-o', label = 'test')\n",
    "plt.xlim([np.min(alpha_arr), np.max(alpha_arr)])\n",
    "plt.title('Accuracy vs. neuron')\n",
    "plt.xlabel('neuron')\n",
    "plt.ylabel('Accuracy')\n",
    "plt.legend()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "2e7dd91d",
   "metadata": {},
   "source": [
    "##### Минимальное значение ошибки:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 64,
   "id": "e60a839f",
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "ERR train =  0.04433121019108277 \t ERR test =  0.03054989816700615\n",
      "score train =  0.9556687898089172 \t score test =  0.9694501018329938\n"
     ]
    }
   ],
   "source": [
    "print('ERR train = ', np.min(train_err), '\\t', 'ERR test = ', np.min(test_err))\n",
    "print('score train = ', 1-np.min(train_err), '\\t', 'score test = ', 1-np.min(test_err))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "e626f3db",
   "metadata": {},
   "source": [
    "##### Оптимальное значение количества нейронов на первом слое:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 65,
   "id": "5362f823",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Оптимальное значение количества нейронов на первом слое:  1\n"
     ]
    }
   ],
   "source": [
    "n_opt = alpha_arr[test_err == np.min(test_err)]\n",
    "\n",
    "n_opt = n_opt[0]\n",
    "print(\"Оптимальное значение количества нейронов на первом слое: \", n_opt)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "426ad001",
   "metadata": {},
   "source": [
    "### Повторим обучение при найденном значении количества нейронов на первом слое:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 66,
   "id": "05e4e393",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " Ошибка на обучающей выборке:  0.045350318471337525 \n",
      " Ошибка на тестовой выборке:  0.03054989816700615\n"
     ]
    }
   ],
   "source": [
    "mlp_model = MLPClassifier(alpha = alpha_opt, hidden_layer_sizes = (n_opt,),\n",
    "                          solver = 'lbfgs', activation = 'logistic', random_state = 73)\n",
    "mlp_model.fit(x_train, y_train)\n",
    "\n",
    "y_train_pred = mlp_model.predict(x_train)\n",
    "y_test_pred = mlp_model.predict(x_test)\n",
    "\n",
    "print(\" Ошибка на обучающей выборке: \", 1 - mlp_model.score(x_train, y_train), '\\n',\n",
    "      \"Ошибка на тестовой выборке: \",1 - mlp_model.score(x_test, y_test))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "069de4f1",
   "metadata": {},
   "source": [
    "## Подбор оптимального числа нейронов на втором слое при ранее найденном alpha и числе нейронов на первом слое"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 67,
   "id": "80a17b82",
   "metadata": {},
   "outputs": [],
   "source": [
    "alpha_arr = np.linspace(1, 101, 50).astype(int)\n",
    "test_err = []\n",
    "train_err = []\n",
    "train_acc = []\n",
    "test_acc = []\n",
    "\n",
    "\n",
    "for alpha in alpha_arr:\n",
    "    mlp_model = MLPClassifier(alpha = alpha_opt, hidden_layer_sizes = (n_opt,alpha), \n",
    "                              solver = 'lbfgs', activation = 'logistic', max_iter=1000, random_state = 73)\n",
    "    mlp_model.fit(x_train, y_train)\n",
    "\n",
    "    y_train_pred = mlp_model.predict(x_train)\n",
    "    y_test_pred = mlp_model.predict(x_test)\n",
    "    \n",
    "    train_err.append(np.mean(y_train != y_train_pred))\n",
    "    test_err.append(np.mean(y_test != y_test_pred))\n",
    "    train_acc.append(accuracy_score(y_train, y_train_pred))\n",
    "    test_acc.append(accuracy_score(y_test, y_test_pred))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "4af78a84",
   "metadata": {
    "scrolled": true
   },
   "source": [
    "##### Минимальные ошибки на обучающей и тестовой выборках:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 68,
   "id": "ccf0a49d",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "ERR min train =  0.04535031847133758 \t ERR min test =  0.03054989816700611\n",
      "score train =  0.9546496815286625 \t score test =  0.9694501018329938\n"
     ]
    }
   ],
   "source": [
    "print('ERR min train = ', np.min(train_err), '\\t', 'ERR min test = ', np.min(test_err))\n",
    "print('score train = ', 1-np.min(train_err), '\\t', 'score test = ', 1-np.min(test_err))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f991cc02",
   "metadata": {},
   "source": [
    "##### Оптимальное значение количества нейронов на втором слое:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 69,
   "id": "3ec163ab",
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Оптимальное значение количества нейронов на втором слое:  1\n"
     ]
    }
   ],
   "source": [
    "n_opt_2 = alpha_arr[test_err == np.min(test_err)]\n",
    "\n",
    "n_opt_2 = n_opt_2[0]\n",
    "print(\"Оптимальное значение количества нейронов на втором слое: \", n_opt_2)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "2d85076a",
   "metadata": {},
   "source": [
    "### Повторим обучение"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 70,
   "id": "730a07ad",
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " Ошибка на обучающей выборке:  0.045350318471337525 \n",
      " Ошибка на тестовой выборке:  0.03054989816700615\n",
      "score train =  0.9546496815286625 \t score test =  0.9694501018329938\n"
     ]
    }
   ],
   "source": [
    "mlp_model = MLPClassifier(alpha = alpha_opt, hidden_layer_sizes = (n_opt, n_opt_2),\n",
    "                          solver = 'lbfgs', activation = 'logistic', random_state = 73)\n",
    "mlp_model.fit(x_train, y_train)\n",
    "\n",
    "y_train_pred = mlp_model.predict(x_train)\n",
    "y_test_pred = mlp_model.predict(x_test)\n",
    "\n",
    "print(\" Ошибка на обучающей выборке: \", 1 - mlp_model.score(x_train, y_train), '\\n',\n",
    "      \"Ошибка на тестовой выборке: \",1 - mlp_model.score(x_test, y_test))\n",
    "print('score train = ', 1-np.min(train_err), '\\t', 'score test = ', 1-np.min(test_err))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "b362d710",
   "metadata": {},
   "source": [
    "Вспомним результаты из таблицы resultML_GRIDD"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 71,
   "id": "5102b621",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Model</th>\n",
       "      <th>Score(training)</th>\n",
       "      <th>Score(test)</th>\n",
       "      <th>MAE test</th>\n",
       "      <th>MAE train</th>\n",
       "      <th>RMSE test</th>\n",
       "      <th>RMSE train</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>KNeighbors classification</td>\n",
       "      <td>0.955924</td>\n",
       "      <td>0.96945</td>\n",
       "      <td>0.03055</td>\n",
       "      <td>0.044076</td>\n",
       "      <td>0.174785</td>\n",
       "      <td>0.209944</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>RandomForest classification</td>\n",
       "      <td>0.954650</td>\n",
       "      <td>0.96945</td>\n",
       "      <td>0.03055</td>\n",
       "      <td>0.045350</td>\n",
       "      <td>0.174785</td>\n",
       "      <td>0.212956</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>XGB classification</td>\n",
       "      <td>0.954650</td>\n",
       "      <td>0.96945</td>\n",
       "      <td>0.03055</td>\n",
       "      <td>0.045350</td>\n",
       "      <td>0.174785</td>\n",
       "      <td>0.212956</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>SVC classification</td>\n",
       "      <td>0.954650</td>\n",
       "      <td>0.96945</td>\n",
       "      <td>0.03055</td>\n",
       "      <td>0.045350</td>\n",
       "      <td>0.174785</td>\n",
       "      <td>0.212956</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Decision Tree classification</td>\n",
       "      <td>0.954650</td>\n",
       "      <td>0.96945</td>\n",
       "      <td>0.03055</td>\n",
       "      <td>0.045350</td>\n",
       "      <td>0.174785</td>\n",
       "      <td>0.212956</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>Extra Trees classification</td>\n",
       "      <td>0.954650</td>\n",
       "      <td>0.96945</td>\n",
       "      <td>0.03055</td>\n",
       "      <td>0.045350</td>\n",
       "      <td>0.174785</td>\n",
       "      <td>0.212956</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                          Model  Score(training)  Score(test)  MAE test  \\\n",
       "0     KNeighbors classification         0.955924      0.96945   0.03055   \n",
       "1   RandomForest classification         0.954650      0.96945   0.03055   \n",
       "2            XGB classification         0.954650      0.96945   0.03055   \n",
       "3            SVC classification         0.954650      0.96945   0.03055   \n",
       "4  Decision Tree classification         0.954650      0.96945   0.03055   \n",
       "5    Extra Trees classification         0.954650      0.96945   0.03055   \n",
       "\n",
       "   MAE train  RMSE test  RMSE train  \n",
       "0   0.044076   0.174785    0.209944  \n",
       "1   0.045350   0.174785    0.212956  \n",
       "2   0.045350   0.174785    0.212956  \n",
       "3   0.045350   0.174785    0.212956  \n",
       "4   0.045350   0.174785    0.212956  \n",
       "5   0.045350   0.174785    0.212956  "
      ]
     },
     "execution_count": 71,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "resultML_GRIDD"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "ef8a129c",
   "metadata": {},
   "source": [
    "##### Вывод:\n",
    "\n",
    "Результаты ошибок на обучающей и тестовой выборках с помощью нейронной сети и с помощью различных методов, которые указаны в таблице resultML_GRID, имеют идентичные результаты для теста (до 5 знака после запятой) и для train"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "b2107c9f",
   "metadata": {},
   "source": [
    "# *Балансировка данных "
   ]
  },
  {
   "cell_type": "markdown",
   "id": "7687c13d",
   "metadata": {},
   "source": [
    "##### В 3 пункте я показала, что данные являются несбалансированными. Это может приводить к ошибкам в обучении моделей"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "08db4ab8",
   "metadata": {},
   "source": [
    "Обратим внимание на то, что выводится через одну колонку, когда я вызываю classification_report(y_test, predictions)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 74,
   "id": "3e303e1b",
   "metadata": {
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "from sklearn.metrics import classification_report, confusion_matrix\n",
    "import xgboost as xgb\n",
    "\n",
    "clf1 = xgb.XGBClassifier()\n",
    "\n",
    "param_dist = {\n",
    "        'n_estimators': [10, 20, 30, 40, 50, 70, 80], \n",
    "        'max_depth': [1, 2, 5],\n",
    "        'learning_rate': [0.0001,0.001, 0.01, 0.1, 0.2]\n",
    "        }\n",
    "\n",
    "grid = GridSearchCV(clf1, param_dist,cv = 3)\n",
    "grid_XGB = grid.fit(x_train,y_train)\n",
    "\n",
    "predictions = grid_XGB.predict(x_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 75,
   "id": "939707b9",
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "              precision    recall  f1-score   support\n",
      "\n",
      "           0       0.97      1.00      0.98       952\n",
      "           1       0.00      0.00      0.00        30\n",
      "\n",
      "    accuracy                           0.97       982\n",
      "   macro avg       0.48      0.50      0.49       982\n",
      "weighted avg       0.94      0.97      0.95       982\n",
      "\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\metrics\\_classification.py:1318: UndefinedMetricWarning: Precision and F-score are ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.\n",
      "  _warn_prf(average, modifier, msg_start, len(result))\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\metrics\\_classification.py:1318: UndefinedMetricWarning: Precision and F-score are ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.\n",
      "  _warn_prf(average, modifier, msg_start, len(result))\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\metrics\\_classification.py:1318: UndefinedMetricWarning: Precision and F-score are ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.\n",
      "  _warn_prf(average, modifier, msg_start, len(result))\n"
     ]
    }
   ],
   "source": [
    "print(classification_report(y_test, predictions))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f973edb6",
   "metadata": {},
   "source": [
    "Обратите внимание, что отзыв и точность для класса 1 всегда равны 0. Это означает, что классификатор всегда классифицирует все в один класс (класс 0)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "89370009",
   "metadata": {},
   "source": [
    "##### Я предлагаю исправить точный классификатор, результаты которого мы видели до пункта \"Балансировка данных\" :)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "23fbebb0",
   "metadata": {},
   "source": [
    "## Проведем балансировку данных"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 115,
   "id": "dae7b73b",
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:xlabel='0', ylabel='count'>"
      ]
     },
     "execution_count": 115,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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tXLlSpWXl9vPI5EIUQQAQB+VFFeIlixZot/85jf6/e9/ryFDhtx0NicnR8OGDdPp06clSR6PR21tbWpqaoqba2xslNvttmcuXLjQ4VgXL160Z67ldDqVmZkZ9wAAAH1TQoMoFovpySef1H//93/rnXfe0fDhw7/2Zy5duqRz584pJydHkpSfn69+/fqpurranmloaNDx48dVWFgoSfL7/QqHwzp8+LA9c+jQIYXDYXsGAACYK6FvmT3xxBN67bXX9MYbbygjI8O+n8eyLKWnp6ulpUVr1qzRo48+qpycHH3yySdatWqVsrOz9fDDD9uz8+bN07JlyzRo0CBlZWVp+fLlysvLsz91Nnr0aE2bNk3z58/X5s2bJUkLFixQSUkJnzADAACJDaJNmzZJksaPHx+3/dVXX9XcuXOVkpKiY8eOafv27WpublZOTo4mTJig3bt3KyMjw57fsGGDUlNTNXPmTLW2tmrSpEnatm2bUlJS7Jldu3Zp6dKl9qfRSktLtXHjxu4/SQAAkPQSGkSxWOym+9PT0/W73/3ua4/Tv39/vfTSS3rppZduOJOVlaWdO3d+4zUCAIC+LyluqgYAAEgkgggAABiPIAIAAMYjiAAAgPEIIgAAYDyCCAAAGI8gAgAAxiOIAACA8QgiAABgPIIIAAAYjyACAADGI4gAAIDxCCIAAGA8gggAABiPIAIAAMYjiAAAgPEIIgAAYDyCCAAAGI8gAgAAxiOIAACA8QgiAABgPIIIAAAYjyACAADGI4gAAIDxCCIAAGA8gggAABivU0E0ceJENTc3d9geiUQ0ceLE210TAABAj+pUEO3bt09tbW0dtv/lL3/Re++9d9uLAgAA6Emp32T4gw8+sP/84YcfKhQK2c/b29sVDAb193//9123OgAAgB7wjYLoH//xH+VwOORwOK771lh6erpeeumlLlscAABAT/hGQXTmzBnFYjF961vf0uHDhzV48GB7X1pamlwul1JSUrp8kQAAAN3pGwXRsGHDJElffPFFtywGAAAgEb5REH3V//7v/2rfvn1qbGzsEEhPP/30bS8MAACgp3QqiLZs2aIf/vCHys7OlsfjkcPhsPc5HA6CCAAA9CqdCqJnn31WP/vZz/TUU0919XoAAAB6XKe+h6ipqUnf+973unotAAAACdGpIPre976nvXv33vaLV1RU6P7771dG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\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "from imblearn.over_sampling import SMOTE\n",
    "smote = SMOTE(sampling_strategy=1.0)\n",
    "x_train, y_train = smote.fit_resample(x_train, y_train.values.ravel())\n",
    "x_train = pd.DataFrame(x_train)\n",
    "y_train = pd.DataFrame(y_train)\n",
    "\n",
    "(x_train.shape,y_train.shape)\n",
    "sns.countplot(x = y_train[0], data = y_train)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "4f527e62",
   "metadata": {},
   "source": [
    "Вновь запущу Classifier() и посмотрю, что выдаст мне эта функция на сбалансированных данных"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 77,
   "id": "f1995596",
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:198: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples,), for example using ravel().\n",
      "  return self._fit(X, y)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\AppData\\Local\\Temp\\ipykernel_10976\\814339181.py:27: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples,), for example using ravel().\n",
      "  i.fit(x_train, y_train)\n"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "KNeighborsClassifier() : 0.8197556008146639\n",
      "RandomForestClassifier() : 0.9093686354378818\n",
      "XGBClassifier(base_score=0.5, booster='gbtree', callbacks=None,\n",
      "              colsample_bylevel=1, colsample_bynode=1, colsample_bytree=1,\n",
      "              early_stopping_rounds=None, enable_categorical=False,\n",
      "              eval_metric=None, feature_types=None, gamma=0, gpu_id=-1,\n",
      "              grow_policy='depthwise', importance_type=None,\n",
      "              interaction_constraints='', learning_rate=0.300000012,\n",
      "              max_bin=256, max_cat_threshold=64, max_cat_to_onehot=4,\n",
      "              max_delta_step=0, max_depth=6, max_leaves=0, min_child_weight=1,\n",
      "              missing=nan, monotone_constraints='()', n_estimators=100,\n",
      "              n_jobs=0, num_parallel_tree=1, predictor='auto', random_state=0, ...) : 0.9439918533604889\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\utils\\validation.py:993: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples, ), for example using ravel().\n",
      "  y = column_or_1d(y, warn=True)\n"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "SVC() : 0.8024439918533605\n",
      "DecisionTreeClassifier() : 0.869653767820774\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\AppData\\Local\\Temp\\ipykernel_10976\\814339181.py:27: DataConversionWarning: A column-vector y was passed when a 1d array was expected. Please change the shape of y to (n_samples,), for example using ravel().\n",
      "  i.fit(x_train, y_train)\n"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "ExtraTreesClassifier() : 0.9103869653767821\n"
     ]
    }
   ],
   "source": [
    "ml_balance = Classifier(x_train, y_train, x_test, y_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 78,
   "id": "0069a9d9",
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Model</th>\n",
       "      <th>Score(training)</th>\n",
       "      <th>Score(test)</th>\n",
       "      <th>MAE test</th>\n",
       "      <th>MAE train</th>\n",
       "      <th>RMSE test</th>\n",
       "      <th>RMSE train</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>KNeighbors classification</td>\n",
       "      <td>0.946891</td>\n",
       "      <td>0.819756</td>\n",
       "      <td>0.180244</td>\n",
       "      <td>0.053109</td>\n",
       "      <td>0.424552</td>\n",
       "      <td>0.230454</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>RandomForest classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.909369</td>\n",
       "      <td>0.090631</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.301050</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>XGB classification</td>\n",
       "      <td>0.998132</td>\n",
       "      <td>0.943992</td>\n",
       "      <td>0.056008</td>\n",
       "      <td>0.001868</td>\n",
       "      <td>0.236660</td>\n",
       "      <td>0.043222</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>SVC classification</td>\n",
       "      <td>0.902455</td>\n",
       "      <td>0.802444</td>\n",
       "      <td>0.197556</td>\n",
       "      <td>0.097545</td>\n",
       "      <td>0.444473</td>\n",
       "      <td>0.312321</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Decision Tree classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.869654</td>\n",
       "      <td>0.130346</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.361035</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>Extra Trees classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.910387</td>\n",
       "      <td>0.089613</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.299354</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                          Model  Score(training)  Score(test)  MAE test  \\\n",
       "0     KNeighbors classification         0.946891     0.819756  0.180244   \n",
       "1   RandomForest classification         1.000000     0.909369  0.090631   \n",
       "2            XGB classification         0.998132     0.943992  0.056008   \n",
       "3            SVC classification         0.902455     0.802444  0.197556   \n",
       "4  Decision Tree classification         1.000000     0.869654  0.130346   \n",
       "5    Extra Trees classification         1.000000     0.910387  0.089613   \n",
       "\n",
       "   MAE train  RMSE test  RMSE train  \n",
       "0   0.053109   0.424552    0.230454  \n",
       "1   0.000000   0.301050    0.000000  \n",
       "2   0.001868   0.236660    0.043222  \n",
       "3   0.097545   0.444473    0.312321  \n",
       "4   0.000000   0.361035    0.000000  \n",
       "5   0.000000   0.299354    0.000000  "
      ]
     },
     "execution_count": 78,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "resultML_balance = regr_result(ml_balance)\n",
    "resultML_balance"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "fddabfc8",
   "metadata": {},
   "source": [
    "По выше приведенной таблице видно, что балансировка данных \"испортила\" предсказание. Однако это связано с тем, что раньше модель предсказывала только один класс, а после балансировки данных предсказание происходит как о наличии инсульта, так и о его отсутвии (см. ниже)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 116,
   "id": "b7f0cd1c",
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "              precision    recall  f1-score   support\n",
      "\n",
      "           0       0.97      0.96      0.97       952\n",
      "           1       0.05      0.07      0.06        30\n",
      "\n",
      "    accuracy                           0.93       982\n",
      "   macro avg       0.51      0.51      0.51       982\n",
      "weighted avg       0.94      0.93      0.94       982\n",
      "\n"
     ]
    }
   ],
   "source": [
    "import xgboost as xgb\n",
    "\n",
    "clf1 = xgb.XGBClassifier()\n",
    "\n",
    "param_dist = {\n",
    "        'n_estimators': [70, 80, 100, 150], \n",
    "        'max_depth': [2, 5,7, 9, 11],\n",
    "        'learning_rate': [ 0.1, 0.2, 0.3, 0.5]\n",
    "        }\n",
    "\n",
    "grid = GridSearchCV(clf1, param_dist,cv = 3)\n",
    "grid_XGB = grid.fit(x_train,y_train)\n",
    "\n",
    "predictions = grid_XGB.predict(x_test)\n",
    "print(classification_report(y_test, predictions))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "6449ab69",
   "metadata": {
    "scrolled": false
   },
   "source": [
    "##### Как я сказала выше, после балансировки модель начинает классифицировать в оба класса, что мы и видем при вызове (classification_report(y_test, predictions)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "17c8cdc4",
   "metadata": {},
   "source": [
    "# 7* Классификация для сбалансированных данных"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "cdb075fe",
   "metadata": {},
   "source": [
    "## Далее провожу подбор оптимальных гиперпараметров по аналогии с тем, что было сделано для несбалансированных данных"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "cc3bd5f4",
   "metadata": {},
   "source": [
    "Я упущу момент подбора гиперпараметров, дабы не отклоняться от главной идеи. Поиск был полностью аналогичен тому, который был выше с сохранением используемых параметров по которым строится сетка\n",
    "\n",
    "Подбор гиперпараметров привел к следующим результатам:\n",
    "    \n",
    "    svmс = svm.SVC(C=3, gamma=1.5, kernel='rbf')\n",
    "    KN = KNeighborsClassifier(n_neighbors = 4)\n",
    "    XGB = XGBClassifier( max_depth=9, learning_rate=0.3,n_estimators=100)\n",
    "    RFC = RandomForestClassifier(max_depth=None, bootstrap=False, min_samples_leaf=1, n_estimators=85, max_features=1)\n",
    "    dtc = DecisionTreeClassifier(max_depth=None, max_features=1, min_samples_leaf=1)\n",
    "    ert = ExtraTreesClassifier(max_depth=None, max_features=1, min_samples_leaf=1, n_estimators=70)\n",
    "\n",
    "Эти параметры используются в ф-и ClassifierGridBalance(), которая будет определна ниже"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "dc1c5ace",
   "metadata": {},
   "source": [
    "### Функция с оптимальными гиперпараметрами для сбалансированных данных"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 80,
   "id": "6231d866",
   "metadata": {},
   "outputs": [],
   "source": [
    "def ClassifierGridBalance(x_train, y_train, x_test, y_test):\n",
    "\n",
    "    svmс = svm.SVC(C=3, gamma=1.5, kernel='rbf')\n",
    "    KN = KNeighborsClassifier(n_neighbors = 4)\n",
    "    XGB = XGBClassifier( max_depth=9, learning_rate=0.3,n_estimators=100)\n",
    "    RFC = RandomForestClassifier(max_depth=None, bootstrap=False, min_samples_leaf=1, n_estimators=85, max_features=1)\n",
    "    dtc = DecisionTreeClassifier(max_depth=None, max_features=1, min_samples_leaf=1)\n",
    "    ert = ExtraTreesClassifier(max_depth=None, max_features=1, min_samples_leaf=1, n_estimators=70)\n",
    "\n",
    "    logs = []\n",
    "\n",
    "\n",
    "    li = [KN,RFC,XGB,svmс,dtc,ert]\n",
    "    d = {}\n",
    "    for i in li:\n",
    "        i.fit(x_train, y_train.values.ravel())\n",
    "        \n",
    "        y_pred_test = i.predict(x_test)\n",
    "        y_pred_train = i.predict(x_train)\n",
    "        \n",
    "        log = {\"name\": i, \"score test\": i.score(x_test,y_test), \n",
    "               \"score train\": i.score(x_train,y_train.values),\n",
    "               \"MAE test\": metrics.mean_absolute_error(y_test, y_pred_test),\n",
    "               \"MAE train\": metrics.mean_absolute_error(y_train, y_pred_train),\n",
    "               \"RMSE test\": np.sqrt(metrics.mean_squared_error(y_test, y_pred_test)),\n",
    "               \"RMSE train\": np.sqrt(metrics.mean_squared_error(y_train, y_pred_train))}\n",
    "        logs.append(log)\n",
    "        print(i,\":\", i.score(x_test,y_test))\n",
    "    return logs "
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f3f3800f",
   "metadata": {},
   "source": [
    "##### Выведу таблицу с результатами с помощью функции regr_result(), которую я определяла ранее"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 81,
   "id": "447800f2",
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neighbors\\_classification.py:228: FutureWarning: Unlike other reduction functions (e.g. `skew`, `kurtosis`), the default behavior of `mode` typically preserves the axis it acts along. In SciPy 1.11.0, this behavior will change: the default value of `keepdims` will become False, the `axis` over which the statistic is taken will be eliminated, and the value None will no longer be accepted. Set `keepdims` to True or False to avoid this warning.\n",
      "  mode, _ = stats.mode(_y[neigh_ind, k], axis=1)\n"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "KNeighborsClassifier(n_neighbors=4) : 0.8645621181262729\n",
      "RandomForestClassifier(bootstrap=False, max_features=1, n_estimators=85) : 0.9226069246435845\n",
      "XGBClassifier(base_score=0.5, booster='gbtree', callbacks=None,\n",
      "              colsample_bylevel=1, colsample_bynode=1, colsample_bytree=1,\n",
      "              early_stopping_rounds=None, enable_categorical=False,\n",
      "              eval_metric=None, feature_types=None, gamma=0, gpu_id=-1,\n",
      "              grow_policy='depthwise', importance_type=None,\n",
      "              interaction_constraints='', learning_rate=0.3, max_bin=256,\n",
      "              max_cat_threshold=64, max_cat_to_onehot=4, max_delta_step=0,\n",
      "              max_depth=9, max_leaves=0, min_child_weight=1, missing=nan,\n",
      "              monotone_constraints='()', n_estimators=100, n_jobs=0,\n",
      "              num_parallel_tree=1, predictor='auto', random_state=0, ...) : 0.9338085539714868\n",
      "SVC(C=3, gamma=1.5) : 0.905295315682281\n",
      "DecisionTreeClassifier(max_features=1) : 0.8625254582484725\n",
      "ExtraTreesClassifier(max_features=1, n_estimators=70) : 0.9164969450101833\n"
     ]
    }
   ],
   "source": [
    "ml_grid_balance = ClassifierGridBalance(x_train, y_train, x_test, y_test)\n",
    "\n",
    "resultML_GRIDD_balance = regr_result(ml_grid_balance)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "e945c8c6",
   "metadata": {},
   "source": [
    "##### Таблица с оптимально подобранными параметрами"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 82,
   "id": "ce7bb33d",
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Model</th>\n",
       "      <th>Score(training)</th>\n",
       "      <th>Score(test)</th>\n",
       "      <th>MAE test</th>\n",
       "      <th>MAE train</th>\n",
       "      <th>RMSE test</th>\n",
       "      <th>RMSE train</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>KNeighbors classification</td>\n",
       "      <td>0.971310</td>\n",
       "      <td>0.864562</td>\n",
       "      <td>0.135438</td>\n",
       "      <td>0.028690</td>\n",
       "      <td>0.368019</td>\n",
       "      <td>0.169380</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>RandomForest classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.922607</td>\n",
       "      <td>0.077393</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.278196</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>XGB classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.933809</td>\n",
       "      <td>0.066191</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.257277</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>SVC classification</td>\n",
       "      <td>0.982653</td>\n",
       "      <td>0.905295</td>\n",
       "      <td>0.094705</td>\n",
       "      <td>0.017347</td>\n",
       "      <td>0.307741</td>\n",
       "      <td>0.131709</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Decision Tree classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.862525</td>\n",
       "      <td>0.137475</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.370776</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>Extra Trees classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.916497</td>\n",
       "      <td>0.083503</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.288969</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                          Model  Score(training)  Score(test)  MAE test  \\\n",
       "0     KNeighbors classification         0.971310     0.864562  0.135438   \n",
       "1   RandomForest classification         1.000000     0.922607  0.077393   \n",
       "2            XGB classification         1.000000     0.933809  0.066191   \n",
       "3            SVC classification         0.982653     0.905295  0.094705   \n",
       "4  Decision Tree classification         1.000000     0.862525  0.137475   \n",
       "5    Extra Trees classification         1.000000     0.916497  0.083503   \n",
       "\n",
       "   MAE train  RMSE test  RMSE train  \n",
       "0   0.028690   0.368019    0.169380  \n",
       "1   0.000000   0.278196    0.000000  \n",
       "2   0.000000   0.257277    0.000000  \n",
       "3   0.017347   0.307741    0.131709  \n",
       "4   0.000000   0.370776    0.000000  \n",
       "5   0.000000   0.288969    0.000000  "
      ]
     },
     "execution_count": 82,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "resultML_GRIDD_balance "
   ]
  },
  {
   "cell_type": "markdown",
   "id": "977430ab",
   "metadata": {},
   "source": [
    "##### Таблица без оптимально подобранных параметров"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 83,
   "id": "0044ad9f",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Model</th>\n",
       "      <th>Score(training)</th>\n",
       "      <th>Score(test)</th>\n",
       "      <th>MAE test</th>\n",
       "      <th>MAE train</th>\n",
       "      <th>RMSE test</th>\n",
       "      <th>RMSE train</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>KNeighbors classification</td>\n",
       "      <td>0.946891</td>\n",
       "      <td>0.819756</td>\n",
       "      <td>0.180244</td>\n",
       "      <td>0.053109</td>\n",
       "      <td>0.424552</td>\n",
       "      <td>0.230454</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>RandomForest classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.909369</td>\n",
       "      <td>0.090631</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.301050</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>XGB classification</td>\n",
       "      <td>0.998132</td>\n",
       "      <td>0.943992</td>\n",
       "      <td>0.056008</td>\n",
       "      <td>0.001868</td>\n",
       "      <td>0.236660</td>\n",
       "      <td>0.043222</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>SVC classification</td>\n",
       "      <td>0.902455</td>\n",
       "      <td>0.802444</td>\n",
       "      <td>0.197556</td>\n",
       "      <td>0.097545</td>\n",
       "      <td>0.444473</td>\n",
       "      <td>0.312321</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Decision Tree classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.869654</td>\n",
       "      <td>0.130346</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.361035</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>Extra Trees classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.910387</td>\n",
       "      <td>0.089613</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.299354</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                          Model  Score(training)  Score(test)  MAE test  \\\n",
       "0     KNeighbors classification         0.946891     0.819756  0.180244   \n",
       "1   RandomForest classification         1.000000     0.909369  0.090631   \n",
       "2            XGB classification         0.998132     0.943992  0.056008   \n",
       "3            SVC classification         0.902455     0.802444  0.197556   \n",
       "4  Decision Tree classification         1.000000     0.869654  0.130346   \n",
       "5    Extra Trees classification         1.000000     0.910387  0.089613   \n",
       "\n",
       "   MAE train  RMSE test  RMSE train  \n",
       "0   0.053109   0.424552    0.230454  \n",
       "1   0.000000   0.301050    0.000000  \n",
       "2   0.001868   0.236660    0.043222  \n",
       "3   0.097545   0.444473    0.312321  \n",
       "4   0.000000   0.361035    0.000000  \n",
       "5   0.000000   0.299354    0.000000  "
      ]
     },
     "execution_count": 83,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "resultML_balance"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "e82f1499",
   "metadata": {},
   "source": [
    "Из сравнения таблиц resultML_GRIDD_balance и resultML_balance видно, что хотя подбор гиперпараметров немного улучшил предсказательную способность на тесте, однако он не помог в переобучении для RandomForest classification, Decision Tree classification, Extra Trees classification (Ранее для несбалансированных данных подбор гиперпараметров помог избавиться от переобучения для этих методов). Однако у SVC значительно уменьшилась ошибка на тесте (19.75% -> 9.47%). \n",
    "\n",
    "Предположительно, для дальнейшего улучшения работы классификаторов нужно использовать дополнительные гиперпараметры во время поиска оптимальных значений"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "50392647",
   "metadata": {},
   "source": [
    "# 8* Нейронная сеть для сбалансированнных данных"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 84,
   "id": "af41e061",
   "metadata": {
    "scrolled": true
   },
   "outputs": [],
   "source": [
    "test_err = []\n",
    "train_err = []\n",
    "train_acc = []\n",
    "test_acc = []  \n",
    "\n",
    "hidden_layer_sizes = (100,)\n",
    "alpha_arr = np.logspace(-3, 2, 21)\n",
    "\n",
    "training(x_train, x_test, y_train.values.ravel(), y_test, test_err, train_err, train_acc, test_acc, hidden_layer_sizes, alpha_arr)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f035a226",
   "metadata": {},
   "source": [
    "##### Как меняется ошибка в зависимости от гиперпараметра:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 85,
   "id": "98384eaa",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.legend.Legend at 0x22eb6b98e80>"
      ]
     },
     "execution_count": 85,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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sT06OhrHjh3Tax///vsvlEolADFL8pEjR9C8eXOjx2rrjHEuJEnC6NGj8dhjj2HEiBGmCNMuGONckGnoc24effRR/Prrr0hPT8edO3ewZ88e9OzZU45wbR7/ViyHPueiutcIJ6NEaqWys7OhUqng7++vsd3f3x+ZmZl67ePq1asYM2YMJEmCJEmYNGkSWrdubYpwbZoxzsUPP/yArVu3onXr1sVt259++ilatWpl7HBtmjHOBQD07NkTp0+fxt27dxEYGIgdO3agffv2xg7XruhzbpycnPDuu++ie/fuKCoqwowZM3jXrono+7fCvwXT0+dcVPcaYdcJk1rZ9n1JkvRu8w8PD0dqaqoJorJP1TkX//nPf1BUVGSKsOxSdc4FAN6ZZUK6zk3//v3Rv39/c4dlt3SdD/4tmE9l56K61wi7bpKrU6cOHB0dy/1qzsrKKpelkmnxXFgOngvLxXNjWXg+LIc5zoVdJ0wuLi4IDw9HUlKSxvakpCR06tRJpqjsE8+F5eC5sFw8N5aF58NymONc2HyTXG5uLv7888/i55cuXUJqaipq166Nhg0bYtq0aRgxYgQiIiIQGRmJ1atXIy0tDePHj5cxatvEc2E5eC4sF8+NZeH5sByyn4sq31dnZQ4ePCgBKLeMGjWquMzy5cul4OBgycXFRQoLC5MOHz4sX8A2jOfCcvBcWC6eG8vC82E55D4XnEuOiIiISAe77sNEREREpA8mTEREREQ6MGEiIiIi0oEJExEREZEOTJiIiIiIdGDCRERERKQDEyYiIiIiHZgwEREREenAhImIiIhIByZMRGQzLl++DIVCgdTUVL3fk5CQAG9vb5PFRES2gQkTERERkQ5MmIiIiIh0YMJERFblu+++w3/+8x94e3vD19cXffv2xV9//aW17KFDh6BQKPDNN9+gTZs2cHNzQ4cOHfDLL7+UK7t37160bNkSNWvWRK9evZCRkVH82smTJ9GjRw/UqVMHXl5e6Nq1K06fPm2yz0hElocJExFZlbt372LatGk4efIkDhw4AAcHBwwaNAhFRUUVvueVV17B0qVLcfLkSfj5+aF///4oKCgofv3evXtYunQpPv30Uxw5cgRpaWmYPn168et37tzBqFGjkJycjB9//BFNmzZFnz59cOfOHZN+ViKyHE5yB0BEVBVPPfWUxvN169bBz88P586dQ82aNbW+Z+7cuejRowcAYMOGDQgMDMSOHTswZMgQAEBBQQFWrVqFhx56CAAwadIkLFiwoPj9jz32mMb+Pv74Y/j4+ODw4cPo27ev0T4bEVku1jARkVX566+/8Mwzz6BJkybw9PRE48aNAQBpaWkVvicyMrJ4vXbt2mjevDnOnz9fvM3Dw6M4WQKAgIAAZGVlFT/PysrC+PHj0axZM3h5ecHLywu5ubmVHpOIbAtrmIjIqvTr1w9BQUFYs2YN6tevj6KiIoSGhiI/P79K+1EoFMXrzs7O5V6TJKn4+ejRo3H9+nXEx8cjODgYrq6uiIyMrPIxich6MWEiIqtx48YNnD9/Hh9//DGioqIAAEePHtX5vh9//BENGzYEANy6dQsXL15EixYt9D5ucnIyVqxYgT59+gAArly5guzsbAM+ARFZKyZMRGQ1fHx84Ovri9WrVyMgIABpaWmYNWuWzvctWLAAvr6+8Pf3x5w5c1CnTh0MHDhQ7+M+/PDD+PTTTxEREQGlUolXXnkF7u7u1fgkRGRt2IeJiKyGg4MDPv/8c6SkpCA0NBRTp07FO++8o/N9b731FqZMmYLw8HBkZGRg165dcHFx0fu4n3zyCW7duoV27dphxIgRmDx5Mvz8/KrzUYjIyiik0g31REQ25NChQ+jevTtu3brF6U+IqFpYw0RERESkAxMmIiIiIh3YJEdERESkA2uYiIiIiHRgwkRERESkAxMmIiIiIh2YMBERERHpwISJiIiISAcmTEREREQ6MGEiIiIi0oEJExEREZEO/w+QWHpRjMes+gAAAABJRU5ErkJggg==\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.semilogx(alpha_arr, train_err, 'b-o', label = 'train')\n",
    "plt.semilogx(alpha_arr, test_err, 'r-o', label = 'test')\n",
    "plt.xlim([np.min(alpha_arr), np.max(alpha_arr)])\n",
    "plt.title('Error vs. alpha')\n",
    "plt.xlabel('alpha')\n",
    "plt.ylabel('error')\n",
    "plt.legend()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "5c7dd96d",
   "metadata": {},
   "source": [
    "##### Как меняется качество модели в зависимости от гиперпараметра:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 86,
   "id": "b155f49a",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.legend.Legend at 0x22e8a131fa0>"
      ]
     },
     "execution_count": 86,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.semilogx(alpha_arr, train_acc, 'r-o', label = 'train')\n",
    "plt.semilogx(alpha_arr, test_acc, 'b-o', label = 'test')\n",
    "plt.xlim([np.min(alpha_arr), np.max(alpha_arr)])\n",
    "plt.title('Accuracy vs. alpha')\n",
    "plt.xlabel('alpha')\n",
    "plt.ylabel('Accuracy')\n",
    "plt.legend()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "fe170b78",
   "metadata": {},
   "source": [
    "##### Минимальное значение ошибки:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 87,
   "id": "4674a52f",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "ERR train =  0.0004003202562049557 \t ERR test =  0.09063136456211818\n",
      "score train =  0.999599679743795 \t score test =  0.9093686354378818\n"
     ]
    }
   ],
   "source": [
    "print('ERR train = ', np.min(train_err), '\\t', 'ERR test = ', np.min(test_err))\n",
    "print('score train = ', 1-np.min(train_err), '\\t', 'score test = ', 1-np.min(test_err))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "c21a879f",
   "metadata": {},
   "source": [
    "##### Оптимальное значение alpha:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 88,
   "id": "c98949be",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Оптимальное значение параметра:  0.0017782794100389228\n"
     ]
    }
   ],
   "source": [
    "alpha_opt = alpha_arr[test_err == np.min(test_err)]\n",
    "alpha_opt = alpha_opt[0]\n",
    "\n",
    "print(\"Оптимальное значение параметра: \", alpha_opt)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "2c438b73",
   "metadata": {},
   "source": [
    "## Классификатор при найденном оптимальном значении alpha:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 89,
   "id": "6fb14c5d",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " Ошибка на обучающей выборке:  0.008273285294902566 \n",
      " Ошибка на тестовой выборке:  0.09775967413441955\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n"
     ]
    }
   ],
   "source": [
    "mlp_model = MLPClassifier(alpha = alpha_opt, hidden_layer_sizes = (100,),\n",
    "                          solver = 'lbfgs', activation = 'logistic', random_state = 73)\n",
    "mlp_model.fit(x_train, y_train.values.ravel())\n",
    "\n",
    "y_train_pred = mlp_model.predict(x_train)\n",
    "y_test_pred = mlp_model.predict(x_test)\n",
    "\n",
    "print(\" Ошибка на обучающей выборке: \", 1 - mlp_model.score(x_train, y_train), '\\n',\n",
    "      \"Ошибка на тестовой выборке: \",1 - mlp_model.score(x_test, y_test))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "8325923e",
   "metadata": {},
   "source": [
    "## Подбор оптимального числа нейронов на первом слое при ранее найденном alpha"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 90,
   "id": "ad50f8e6",
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n"
     ]
    }
   ],
   "source": [
    "alpha_arr = np.linspace(1, 101, 50).astype(int)\n",
    "test_err = []\n",
    "train_err = []\n",
    "train_acc = []\n",
    "test_acc = []\n",
    "\n",
    "for alpha in alpha_arr:\n",
    "    mlp_model = MLPClassifier(alpha = alpha_opt, hidden_layer_sizes = (alpha,), \n",
    "                              solver = 'lbfgs', activation = 'logistic', max_iter=1000, random_state = 73)\n",
    "    mlp_model.fit(x_train, y_train.values.ravel())\n",
    "\n",
    "    y_train_pred = mlp_model.predict(x_train)\n",
    "    y_test_pred = mlp_model.predict(x_test)\n",
    "    \n",
    "    train_err.append(1 - mlp_model.score(x_train, y_train))\n",
    "    test_err.append(1 - mlp_model.score(x_test, y_test))\n",
    "    train_acc.append(accuracy_score(y_train, y_train_pred))\n",
    "    test_acc.append(accuracy_score(y_test, y_test_pred))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 91,
   "id": "df238b72",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.legend.Legend at 0x22e8a52cf40>"
      ]
     },
     "execution_count": 91,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAkgAAAHFCAYAAAAJ2AY0AAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjUuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8qNh9FAAAACXBIWXMAAA9hAAAPYQGoP6dpAABlkUlEQVR4nO3deVxU9f4/8NcwsomCGwIKopaK5pKCCyLu+1JGpdnX3TJTr6C3a5qV5i0p782lxSUrabkupVjWz1IsF8yy9IJlmlouuEBmJogLyvD5/fG5MzD7GZiZMwOv5+NxHjNz5jPnfM4cnPP283mfz0cjhBAgIiIiIgMftStARERE5GkYIBERERGZYIBEREREZIIBEhEREZEJBkhEREREJhggEREREZlggERERERkggESERERkQkGSEREREQmGCARVWJpaWnQaDRWl927d6tdRSIij1RN7QoQkeutXbsWMTExZutbtWqlQm2IiDwfAySiKqB169aIi4tz6DNCCNy6dQuBgYFm7928eRMBAQHQaDTlrtONGzdQvXr1cn++srtz5w40Gg2qVePPNJEa2MVGRAAAjUaD6dOnY9WqVWjZsiX8/f3x3nvvGbrpduzYgYkTJyI0NBTVq1dHUVERSkpKsHjxYsTExMDf3x/169fH2LFjcf78eaNt9+zZE61bt8bevXvRtWtXVK9eHRMnTrRYj2XLlkGj0eDXX381e+/pp5+Gn58fLl++DADIysrC0KFDUb9+ffj7+6NBgwYYMmSI2f6VWLBgATQaDX7++WeMGjUKISEhCAsLw8SJE5Gfn29UVgiBFStW4N5770VgYCBq166Nhx56CKdOnTIq17hxY4wfP95sXz179kTPnj0Nr3fv3g2NRoMPPvgAf//739GwYUP4+/sbvoN3330X7dq1Q0BAAOrUqYMHHngAx44dM9rm+PHjUaNGDfz6668YPHgwatSogaioKPz9739HUVGRUdmVK1eiXbt2qFGjBmrWrImYmBg888wzDn9nRJUZAySiKkCn06G4uNho0el0ZuU++eQTrFy5Es8//zy2b9+OxMREw3sTJ06Er68vPvjgA2zatAm+vr548skn8fTTT6Nfv37YunUr/vnPf+LLL79E165dDUGMXm5uLkaPHo1HH30U27Ztw9SpUy3WdfTo0fDz80NaWprZMXz44YcYNmwY6tWrh+vX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\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.plot(alpha_arr, train_err, 'b-o', label = 'train_1')\n",
    "plt.plot(alpha_arr, test_err, 'r-o', label = 'test_1')\n",
    "plt.xlim([np.min(alpha_arr), np.max(alpha_arr)])\n",
    "plt.title('Error vs. neurons')\n",
    "plt.xlabel('neurons')\n",
    "plt.ylabel('error')\n",
    "plt.legend()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 92,
   "id": "856b071b",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.legend.Legend at 0x22e8a6b1790>"
      ]
     },
     "execution_count": 92,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAkgAAAHFCAYAAAAJ2AY0AAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjUuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8qNh9FAAAACXBIWXMAAA9hAAAPYQGoP6dpAABo9UlEQVR4nO3deVwU9f8H8Ney3CooKoeCgOUZat4npmV4H18zjwrFI/ObpWSXpmX6Ky0r88Y0z/JKxbK+WpLinfdVah6FgQiSpoAnsHx+f0y7sMvuMgu7O8vyej4e89jd2c/MfHYGdt77OVVCCAEiIiIi0nFROgNEREREjoYBEhEREZEBBkhEREREBhggERERERlggERERERkgAESERERkQEGSEREREQGGCARERERGWCARERERGSAARJRGTRv3jyoVCpEREQonRUiIqfEAImoDFq+fDkA4OzZszh8+LDCuSEicj4MkIjKmGPHjuH06dPo2bMnAGDZsmUK58i0e/fuKZ0FMuL+/ftKZ4HI4TFAIipjtAHRRx99hHbt2mH9+vVGA5HU1FSMHj0aISEhcHd3R40aNTBgwABcv35dl+b27dt4/fXXUbt2bXh4eMDf3x89evTA77//DgDYvXs3VCoVdu/erbfvK1euQKVSYeXKlbp1MTExqFixIn799VdERUWhUqVKeOqppwAACQkJ6Nu3L4KDg+Hp6YlHH30UL730Em7cuFEk37///juGDBmCgIAAeHh4oFatWhg6dCgePnyIK1euwNXVFTNnziyy3d69e6FSqbBx40aj5+3vv/+Gu7s73n33XaPHVKlUmDdvHgApsHvjjTcQHh4OT09P+Pn5oUWLFli3bp3RfZujPVeffvopZs+ejfDwcFSsWBFt27bFoUOHiqQ/duwY+vTpAz8/P3h6eqJp06b45ptv9NK8//77UKlURbZduXIlVCoVrly5olsXFhaGXr16IT4+Hk2bNoWnpyemTZsGAPjtt9/Qt29fVKlSBZ6ennj88cexatUqvX1q/wbWrVuHyZMno0aNGvDx8UGXLl1w4cIFi88HUVnhqnQGiEi++/fvY926dWjZsiUiIiIwYsQIjBo1Chs3bsSwYcN06VJTU9GyZUvk5ubinXfeQePGjXHz5k389NNPuHXrFgICApCdnY0OHTrgypUrePvtt9G6dWvcuXMHe/fuRVpaGurXr29x/nJyctCnTx+89NJLmDhxIvLy8gAAf/zxB9q2bYtRo0bB19cXV65cwezZs9GhQwf8+uuvcHNzAwCcPn0aHTp0QLVq1TB9+nTUqVMHaWlp2Lp1K3JychAWFoY+ffpg8eLFeOutt6BWq3XHXrBgAWrUqIH//Oc/RvNWvXp19OrVC6tWrcK0adPg4lLw+3DFihVwd3fH888/DwCYMGECvvrqK3zwwQdo2rQp7t69i99++w03b960+JxoLVy4EPXr18ecOXMAAO+++y569OiBpKQk+Pr6AgASExPRrVs3tG7dGosXL4avry/Wr1+PQYMG4d69e4iJiSnRsU+cOIHz589jypQpCA8PR4UKFXDhwgW0a9cO/v7+mDdvHqpWrYqvv/4aMTExuH79Ot566y29fbzzzjto3749vvzyS2RlZeHtt99G7969cf78eb3rQOQ0BBGVGatXrxYAxOLFi4UQQmRnZ4uKFSuKyMhIvXQjRowQbm5u4ty5cyb3NX36dAFAJCQkmEyTmJgoAIjExES99UlJSQKAWLFihW7dsGHDBACxfPlys58hPz9f5Obmir/++ksAEN99953uvSeffFJUrlxZZGRkFJunLVu26NalpqYKV1dXMW3aNLPH3rp1qwAgduzYoVuXl5cnatSoIZ555hnduoiICNGvXz+z+5JLe64aNWok8vLydOuPHDkiAIh169bp1tWvX180bdpU5Obm6u2jV69eIigoSGg0GiGEEFOnThXGvr5XrFghAIikpCTdutDQUKFWq8WFCxf00g4ePFh4eHiI5ORkvfXdu3cX3t7e4vbt20KIgvPdo0cPvXTffPONACB++eUXC84GUdnBKjaiMmTZsmXw8vLC4MGDAQAVK1bEs88+i3379uHSpUu6dNu3b0fnzp3RoEEDk/vavn076tatiy5dulg1j88880yRdRkZGRgzZgxCQkLg6uoKNzc3hIaGAgDOnz8PQKrW2rNnDwYOHIjq1aub3H+nTp3QpEkTLFy4ULdu8eLFUKlUGD16tNm8de/eHYGBgVixYoVu3U8//YRr165hxIgRunWtWrXC9u3bMXHiROzevdsqbXZ69uypV9LSuHFjAMBff/0FALh8+TJ+//13XSlWXl6ebunRowfS0tJKXKXVuHFj1K1bV2/drl278NRTTyEkJERvfUxMDO7du4dffvlFb32fPn2K7LNw/omcDQMkojLi8uXL2Lt3L3r27AkhBG7fvo3bt29jwIABAAp6tgFSe5vg4GCz+5OTxlLe3t7w8fHRW5efn4+oqCjEx8fjrbfews6dO3HkyBFd+xtt8HHr1i1oNBpZeRo3bhx27tyJCxcuIDc3F0uXLsWAAQMQGBhodjtXV1dER0djy5YtuH37NgCp3U5QUBC6du2qSzdv3jy8/fbb+Pbbb9G5c2f4+fmhX79+ekGopapWrar32sPDA0DB59e2DXvjjTfg5uamt7z88ssAYLTNlhxBQUFF1t28edPo+ho1aujetyT/RM6GARJRGbF8+XIIIbBp0yZUqVJFt2h7s61atQoajQaA1N7m6tWrZvcnJ42npycA4OHDh3rrTd2ojTUc/u2333D69Gl88sknePXVV9GpUye0bNmyyA3Xz88ParW62DwBwHPPPYeqVati4cKF2LhxI9LT0zF27NhitwOA4cOH48GDB1i/fj1u3bqFrVu3YujQoXqlOxUqVMC0adPw+++/Iz09HXFxcTh06BB69+4t6xglUa1aNQDApEmTcPToUaPL448/DsA616Vq1apIS0srsv7atWt6+SEqrxggEZUBGo0Gq1atwiOPPILExMQiy+uvv460tDRs374dgFSVlJiYaLZKpnv37rh48SJ27dplMk1YWBgA4MyZM3rrt27dKjvv2puztsRB64svvtB77eXlhSeeeAIbN24stqTE09MTo0ePxqpVqzB79mw8/vjjaN++vaz8NGjQAK1bt8aKFSuwdu1aPHz4EMOHDzeZPiAgADExMRgyZAguXLhgs6EL6tWrhzp16uD06dNo0aKF0aVSpUoATF+X77//XvbxnnrqKezatUsXEGmtXr0a3t7eaNOmTek+EFEZx15sRGXA9u3bce3aNXz88cfo1KlTkfcjIiKwYMECLFu2DL169cL06dOxfft2dOzYEe+88w4aNWqE27dv48cff8SECRNQv359xMbGYsOGDejbty8mTpyIVq1a4f79+9izZw969eqFzp07IzAwEF26dMHMmTNRpUoVhIaGYufOnYiPj5ed9/r16+ORRx7BxIkTIYSAn58fvv/+eyQkJBRJq+3Z1rp1a0ycOBGPPvoorl+/jq1bt+KLL77QBQgA8PLLL2PWrFk4fvw4vvzyS4vO54gRI/DSSy/h2rVraNeuHerVq6f3fuvW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BkhEREREBhggERERERlggERERERkgAESERERkQEGSEREREQGGCARERERGWCARERERGSAARIRERGRAQZIRET/ysnJUToLROQgGCARkUPq1KkTxo0bh7feegt+fn4IDAzE+++/r3s/MzMTo0ePhr+/P3x8fPDkk0/i9OnTuvdjYmLQr18/vX3GxsaiU6dOesd45ZVXMGHCBFSrVg1PP/00AGDPnj1o1aoVPDw8EBQUhIkTJyIvL0923oio7GOAREQOa9WqVahQoQIOHz6MWbNmYfr06UhISIAQAj179kR6ejq2bduG48ePo1mzZnjqqafwzz//WHwMV1dXHDhwAF988QVSU1PRo0cPtGzZEqdPn0ZcXByWLVuGDz74QFbeiMg5uCqdASIiUxo3boypU6cCAOrUqYMFCxZg586dUKvV+PXXX5GRkQEPDw8AwKeffopvv/0WmzZtwujRo2Uf49FHH8WsWbN0rydPnoyQkBAsWLAAKpUK9evXx7Vr1/D222/jvffeg4uLi9m8aUuhiKhsY4BERA6rcePGeq+DgoKQkZGB48eP486dO6hatare+/fv38cff/xh0TFatGih9/r8+fNo27YtVCqVbl379u1x584dXL16FbVq1TKbNyJyDgyQiMhhubm56b1WqVTIz89Hfn4+goKCsHv37iLbVK5cGQDg4uICIYTee7m5uUXSV6hQQe+1EEIvONKu0x6/uLwRkXNggEREZU6zZs2Qnp4OV1dXhIWFGU1TvXp1/Pbbb3rrTp06VSSwMdSwYUNs3rxZL1A6ePAgKlWqhJo1a1ol/0Tk+NhIm4jKnC5duqBt27bo168ffvrpJ1y5cgUHDx7ElClTcOzYMQDAk08+iWPHjmH16tW4dOkSpk6dWiRgMubll19GSkoKXn31Vfz+++/47rvvMHXqVEyYMEHX/oiInB//24mozFGpVNi2bRs6duyIESNGoG7duhg8eDCuXLmCgIAAAEDXrl3x7rvv4q233kLLli2RnZ2NoUOHFrvvmjVrYtu2bThy5AiaNGmCMWPGYOTIkZgyZYqtPxYRORCVMKykJyIiIirnWIJEREREZIABEhEREZEBBkhEREREBhggERERERlggERERERkgAESERERkQEGSEREREQGGCARERERGWCARERERGSAARIRERGRAQZIRERERAYYIBEREREZ+H+BS9+lqnA2rwAAAABJRU5ErkJggg==\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.plot(alpha_arr, train_acc, 'r-o', label = 'train')\n",
    "plt.plot(alpha_arr, test_acc, 'b-o', label = 'test')\n",
    "plt.xlim([np.min(alpha_arr), np.max(alpha_arr)])\n",
    "plt.title('Accuracy vs. neuron')\n",
    "plt.xlabel('neuron')\n",
    "plt.ylabel('Accuracy')\n",
    "plt.legend()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "4d3114bf",
   "metadata": {},
   "source": [
    "##### Минимальное значение ошибки:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 93,
   "id": "79ad8465",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "ERR train =  0.0002668801708033408 \t ERR test =  0.08757637474541746\n",
      "score train =  0.9997331198291967 \t score test =  0.9124236252545825\n"
     ]
    }
   ],
   "source": [
    "print('ERR train = ', np.min(train_err), '\\t', 'ERR test = ', np.min(test_err))\n",
    "print('score train = ', 1-np.min(train_err), '\\t', 'score test = ', 1-np.min(test_err))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "e7cb59e4",
   "metadata": {},
   "source": [
    "##### Оптимальное значение количества нейронов на 1 слое:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 94,
   "id": "efd8c83a",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Оптимальное значение количества нейронов на первом слое:  70\n"
     ]
    }
   ],
   "source": [
    "n_opt = alpha_arr[test_err == np.min(test_err)]\n",
    "\n",
    "n_opt = n_opt[0]\n",
    "print(\"Оптимальное значение количества нейронов на первом слое: \", n_opt)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "300cf9da",
   "metadata": {},
   "source": [
    "### При найденном значении количества нейронов на первом слое, повторим обучение"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 95,
   "id": "56371ab7",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " Ошибка на обучающей выборке:  0.0022684814518281193 \n",
      " Ошибка на тестовой выборке:  0.0865580448065173\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n"
     ]
    }
   ],
   "source": [
    "mlp_model = MLPClassifier(alpha = alpha_opt, hidden_layer_sizes = (n_opt,),\n",
    "                          solver = 'lbfgs', activation = 'logistic', random_state = 73)\n",
    "mlp_model.fit(x_train, y_train.values.ravel())\n",
    "\n",
    "y_train_pred = mlp_model.predict(x_train)\n",
    "y_test_pred = mlp_model.predict(x_test)\n",
    "\n",
    "print(\" Ошибка на обучающей выборке: \", 1 - mlp_model.score(x_train, y_train), '\\n',\n",
    "      \"Ошибка на тестовой выборке: \",1 - mlp_model.score(x_test, y_test))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "7a9fcb8b",
   "metadata": {},
   "source": [
    "# Подбор оптимального числа нейронов на втором слое при ранее найденном alpha и числе нейронов на первом слое"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 98,
   "id": "57712324",
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n",
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n"
     ]
    }
   ],
   "source": [
    "alpha_arr = np.linspace(1, 101, 50).astype(int)\n",
    "test_err = []\n",
    "train_err = []\n",
    "train_acc = []\n",
    "test_acc = []\n",
    "\n",
    "\n",
    "for alpha in alpha_arr:\n",
    "    mlp_model = MLPClassifier(alpha = alpha_opt, hidden_layer_sizes = (n_opt,alpha), \n",
    "                              solver = 'lbfgs', activation = 'logistic', max_iter=1000, random_state = 73)\n",
    "    mlp_model.fit(x_train, y_train.values.ravel())\n",
    "\n",
    "    y_train_pred = mlp_model.predict(x_train)\n",
    "    y_test_pred = mlp_model.predict(x_test)\n",
    "    \n",
    "    train_err.append(1 - mlp_model.score(x_train, y_train))\n",
    "    test_err.append(1 - mlp_model.score(x_test, y_test))\n",
    "    train_acc.append(accuracy_score(y_train, y_train_pred))\n",
    "    test_acc.append(accuracy_score(y_test, y_test_pred))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "0ac411ed",
   "metadata": {},
   "source": [
    "##### Минимальное значение ошибки:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 99,
   "id": "c2ad9969",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "ERR train =  0.0 \t ERR test =  0.09164969450101834\n",
      "score train =  1.0 \t score test =  0.9083503054989817\n"
     ]
    }
   ],
   "source": [
    "print('ERR train = ', np.min(train_err), '\\t', 'ERR test = ', np.min(test_err))\n",
    "print('score train = ', 1-np.min(train_err), '\\t', 'score test = ', 1-np.min(test_err))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f2886120",
   "metadata": {},
   "source": [
    "##### Оптимальное значение количества нейронов на втором слое:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 100,
   "id": "20bac377",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Оптимальное значение количества нейронов на втором слое:  82\n"
     ]
    }
   ],
   "source": [
    "n_opt_2 = alpha_arr[test_err == np.min(test_err)]\n",
    "\n",
    "n_opt_2 = n_opt_2[0]\n",
    "print(\"Оптимальное значение количества нейронов на втором слое: \", n_opt_2)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "cb8bd33c",
   "metadata": {},
   "source": [
    "### При найденном значении количества нейронов на обоих слоях и оптимального параметра alpha повторим обучение"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 108,
   "id": "87e5d6fe",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " Ошибка на обучающей выборке:  0.03429410194822524 \n",
      " Ошибка на тестовой выборке:  0.14460285132382888\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Mi\\apps\\anaconda3\\lib\\site-packages\\sklearn\\neural_network\\_multilayer_perceptron.py:549: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "  self.n_iter_ = _check_optimize_result(\"lbfgs\", opt_res, self.max_iter)\n"
     ]
    }
   ],
   "source": [
    "mlp_model = MLPClassifier(alpha = alpha_opt, hidden_layer_sizes = (n_opt, n_opt_2, alpha),\n",
    "                          solver = 'lbfgs', activation = 'logistic', random_state = 73)\n",
    "mlp_model.fit(x_train, y_train.values.ravel())\n",
    "\n",
    "\n",
    "print(\" Ошибка на обучающей выборке: \", 1 - mlp_model.score(x_train, y_train), '\\n',\n",
    "      \"Ошибка на тестовой выборке: \",1 - mlp_model.score(x_test, y_test))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "b314a580",
   "metadata": {},
   "source": [
    "Таким образом ошибка на тестовой выборке:  14.46%, \n",
    "            ошибка на обучающей выборке 3.43%\n",
    "            \n",
    "Выведу ошибки для других классификаторов:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 109,
   "id": "2a0d6117",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Model</th>\n",
       "      <th>Score(training)</th>\n",
       "      <th>Score(test)</th>\n",
       "      <th>MAE test</th>\n",
       "      <th>MAE train</th>\n",
       "      <th>RMSE test</th>\n",
       "      <th>RMSE train</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>KNeighbors classification</td>\n",
       "      <td>0.971310</td>\n",
       "      <td>0.864562</td>\n",
       "      <td>0.135438</td>\n",
       "      <td>0.028690</td>\n",
       "      <td>0.368019</td>\n",
       "      <td>0.169380</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>RandomForest classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.922607</td>\n",
       "      <td>0.077393</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.278196</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>XGB classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.933809</td>\n",
       "      <td>0.066191</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.257277</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>SVC classification</td>\n",
       "      <td>0.982653</td>\n",
       "      <td>0.905295</td>\n",
       "      <td>0.094705</td>\n",
       "      <td>0.017347</td>\n",
       "      <td>0.307741</td>\n",
       "      <td>0.131709</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Decision Tree classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.862525</td>\n",
       "      <td>0.137475</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.370776</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>Extra Trees classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.916497</td>\n",
       "      <td>0.083503</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.288969</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                          Model  Score(training)  Score(test)  MAE test  \\\n",
       "0     KNeighbors classification         0.971310     0.864562  0.135438   \n",
       "1   RandomForest classification         1.000000     0.922607  0.077393   \n",
       "2            XGB classification         1.000000     0.933809  0.066191   \n",
       "3            SVC classification         0.982653     0.905295  0.094705   \n",
       "4  Decision Tree classification         1.000000     0.862525  0.137475   \n",
       "5    Extra Trees classification         1.000000     0.916497  0.083503   \n",
       "\n",
       "   MAE train  RMSE test  RMSE train  \n",
       "0   0.028690   0.368019    0.169380  \n",
       "1   0.000000   0.278196    0.000000  \n",
       "2   0.000000   0.257277    0.000000  \n",
       "3   0.017347   0.307741    0.131709  \n",
       "4   0.000000   0.370776    0.000000  \n",
       "5   0.000000   0.288969    0.000000  "
      ]
     },
     "execution_count": 109,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "resultML_GRIDD_balance "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 110,
   "id": "cf940ee8",
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Model</th>\n",
       "      <th>Score(training)</th>\n",
       "      <th>Score(test)</th>\n",
       "      <th>MAE test</th>\n",
       "      <th>MAE train</th>\n",
       "      <th>RMSE test</th>\n",
       "      <th>RMSE train</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>KNeighbors classification</td>\n",
       "      <td>0.946891</td>\n",
       "      <td>0.819756</td>\n",
       "      <td>0.180244</td>\n",
       "      <td>0.053109</td>\n",
       "      <td>0.424552</td>\n",
       "      <td>0.230454</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>RandomForest classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.909369</td>\n",
       "      <td>0.090631</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.301050</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>XGB classification</td>\n",
       "      <td>0.998132</td>\n",
       "      <td>0.943992</td>\n",
       "      <td>0.056008</td>\n",
       "      <td>0.001868</td>\n",
       "      <td>0.236660</td>\n",
       "      <td>0.043222</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>SVC classification</td>\n",
       "      <td>0.902455</td>\n",
       "      <td>0.802444</td>\n",
       "      <td>0.197556</td>\n",
       "      <td>0.097545</td>\n",
       "      <td>0.444473</td>\n",
       "      <td>0.312321</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Decision Tree classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.869654</td>\n",
       "      <td>0.130346</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.361035</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>Extra Trees classification</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.910387</td>\n",
       "      <td>0.089613</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.299354</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                          Model  Score(training)  Score(test)  MAE test  \\\n",
       "0     KNeighbors classification         0.946891     0.819756  0.180244   \n",
       "1   RandomForest classification         1.000000     0.909369  0.090631   \n",
       "2            XGB classification         0.998132     0.943992  0.056008   \n",
       "3            SVC classification         0.902455     0.802444  0.197556   \n",
       "4  Decision Tree classification         1.000000     0.869654  0.130346   \n",
       "5    Extra Trees classification         1.000000     0.910387  0.089613   \n",
       "\n",
       "   MAE train  RMSE test  RMSE train  \n",
       "0   0.053109   0.424552    0.230454  \n",
       "1   0.000000   0.301050    0.000000  \n",
       "2   0.001868   0.236660    0.043222  \n",
       "3   0.097545   0.444473    0.312321  \n",
       "4   0.000000   0.361035    0.000000  \n",
       "5   0.000000   0.299354    0.000000  "
      ]
     },
     "execution_count": 110,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "resultML_balance"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "a963b235",
   "metadata": {},
   "source": [
    "# Вывод:"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "610a0eff",
   "metadata": {},
   "source": [
    "       Классификация на несбалансированных данных: \n",
    "       \n",
    "При использовании дефолтных параметров наблюдается переобучение для методов Random Forest, Decision Tree, Extra Trees. При    подборке гиперпаметров получилось побороться с переобучением и уменьшить ошибку на тестах этих классификаторов. Минимальная ошибка на тестах во всех классификаторах была равна 3%, ошибка на обучающей выборке составила 4.4% для KNN и 4.5% для остальных методов.\n",
    "   \n",
    "При использовании нейронной сетки минимальная ошибка была при alpha=1.77, 1 нейроне в 1 слое и 1 нейроне во втором слое и составила 3.05% на тестовой выборке и 4.5% на обучающей выборке. Т.о. используемая нейронная сеть для классификации несбалансированных даннах выдает аналогичные результаты с другими методами.\n",
    "\n",
    "        Классификация на сбалансированных данных: \n",
    "\n",
    "Результат работы классификаторов после балансировки данных значительно ухудшился. 4 из 6 моделей до подбора параметров являются переобученными. После подбора оптимальных параметров получилось уменьшить ошибку knn с 18% до 13.8% для тестовой выборки. При этом для обучающей выборки ошибка изменилась с 5.4% до 3%. Остальные результаты можно посмотреть в таблицах resultML_balance и resultML_GRIDD_balance, которые представлены выше. Можно сделать следующий выбор по всем классификаторам: несмотря на подбор оптимальных гиперпараметров и последующим улучшением работы классификаторов, результаты после балансировки для данных методов все еще имеют значительную ошибку на тестовой выборке.\n",
    "\n",
    "При использовании нейронных ошибка минимальная ошибка была при alpha=0.00178, 70 нейроне в 1 слое и 82 нейроне во втором слое составила 3.43% на тестовой выборке и 14.46% на обучающей выборке. Т.о. используемая нейронная сеть для классификации несбалансированных даннах выдает значения хуже, чем модели из таблицы resultML_GRID_balance. RandomForest, XGB, Decision Tree, Extra Trees имеют ошибку = 0 на обучающей выборке, значит переобучаются.\n",
    "   \n",
    "Данная ситуация связана с тем, что после балансировки классификация стала происходить не только для одного класса, а для обоих"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.9.13"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
