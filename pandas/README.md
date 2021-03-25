# pandas頻出

```
import numpy as np  
import pandas as pd  
import matplotlib.pyplot as plt 

# グラフ　下のインポートで日本語は文字化けしない
import japanize_matplotlib
```

## 表示のオプション

```
pd.options.display.max_columns = 100
pd.options.display.max_rows = 10
```

## csv読み込み

```
# 見出しなし、文字列として読み込む例
df = pd.read_csv("hokkaido.csv", header=None, dtype="object")

# ヘッダーがないので読み込み時にname=でつける
df = pd.read_csv("hokkaido.csv", names=("postcode", "pref", "city", "address"), dtype="object")

# 読み込みと同時にdatetime型変換
df = pd.read_csv("./csv1_1.csv", parse_dates=["date"])
```

## csv保存

```
df.to_csv("iris.csv", index=False)
```

## ピクル読み込み

```
df = pd.read_pickle("05疑似個人情報.pkl")
```

## ピクル保存

```
pd.to_pickle(df, "05疑似個人情報.pkl")
```

## datetime型への変換処理

```
df["年月日"] = pd.to_datetime(df["年月日"], format="%Y年%m月%d日")
```

## 基本統計量

```
df.describe()
```

## 相関係数

```
df.corr()
```

## 欠損値個数

```
df.isnull().sum()
```

## 欠損値処理

```
# subsetで指定した列に欠損値がある行を削除する
df.dropna(subset=['age'])

# 列削除
df.drop(["Unnamed", "col2"], axis=1)

# 列ごとに穴埋めする値を変える
df.fillna({'A':-10, 'B': 0, 'C': 999})
df['Age'].fillna(df['Age'].median())
df['Embarked'].fillna(df['Embarked'].mode()[0]) # 最頻値

```

## シリーズのユニークなものを出力　numpy.ndarray

```
df['state'].unique()
```

## シリーズのユニークな要素の個数

```
df['state'].nunique()
```

## 出現回数をカウント要素の頻度

```
df['state'].value_counts()
df['state'].value_counts(normalize=True)

df.loc[df["Country"] == "India", "SocialMedia"].value_counts()
df.loc[df["Country"] == "India"]["SocialMedia"].value_counts()

df[df["pred"] == 1]["actual"].value_counts()
```

## カラム名変更

```
df = df.rename(columns={0:"postcode", 1:"state", 2:"city", 3:"address"})
```

## カラムの順番を変える

```
 	A 	B 	C 	D
0 	1 	10 	100 	111
1 	2 	20 	200 	222
2 	3 	30 	300 	333

df = df[["B","C","D","A"]]

 	B 	C 	D 	A
0 	10 	100 	111 	1
1 	20 	200 	222 	2
2 	30 	300 	333 	3
```

## 型確認 dtypes

```
df.dtypes
```

## インデックスのみ確認

```
df.index
```

## カラムのみ確認

```
df.columns
```

## 型変換 astype

```
df.astype({'col_one':'float', 'col_two':'float'})

df.astype({'col1': 'int32'}).dtypes
ser.astype('category')
```

## インデックスを振り直す

```
df.reset_index(inplace=True, drop=True)
```

## カテゴリカル型 factorize

```
codes, uniques = pd.factorize(df['fruit'])

>>> codes
array([0, 0, 1], dtype=int64)

>>> uniques
Index(['a', 'c'], dtype='object'))

# 型変換
df['fruit'] = df['fruit'].astype('category')
```






