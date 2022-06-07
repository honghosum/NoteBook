# Pandas

## 一、创建DataFrame

### 1、空DataFrame

    df = pandas.DataFrame()

### 2、参数创建

    df = pandas.DataFrame(data = [['Sisyphus', 'male', 'D'],
                          ['Athena', 'female', 'B'],
                          ['Zeus', 'male', 'A'],
                          ['Hera', 'female', 'C'],
                          ['Lucifer', 'male', 'B']],
                          columns = ['name', 'gender', 'rank'],
                          index = [0, 1, 2, 3, 4])

### 3、字典

    dic = {'name': ['Sisyphus', 'Athena', 'Zeus', 'Hera', 'Lucifer'],
           'gender': ['male', 'female', 'male', 'female', 'male'],
           'rank': ['D', 'B', 'A', 'C', 'B']}

    df = pandas.DataFrame(dic)

### 4、读取Excel / csv

    df = pd.read_excel('test.xlsx', sheet_name = 'test_sheet')

    df = pd.read_excel('test.xlsb', sheet_name = 'test_sheet', engine = 'pyxlsb')

    df = pd.read_csv('test.csv')

## 二、查询

### 1、统计

    df.head(n) # 返回前n行，DataFrame类型
    
    df.tail(n) # 返回后n行，DataFrame类型
    
    df.sample(n) # 随机返回n行样本，DataFrame类型

    df.ndim # 返回DataFrame的列数

    df.size # 返回DataFrame的值个数

    df.shape # 返回DataFrame的行列数，Tuple类型

    df.dtypes # 返回DataFrame的数据类型

    df.axes # 返回DataFrame的行列标签信息

    df['col'].sum()

    df['col'].mean()

    df['col'].count()

    df['col'].max()

    df['col'].min()

    df['col'].describe() # 返回DataFrame的基本统计数据，标准差、中位数等

### 2、筛选

#### (1)、常规

    df['name'] # 返回Series

    df.name # 返回Series

    df['name'].to_list() # 返回list

#### (2)、loc

##### I、常规选择

    df.loc[0] # 指定索引值index = 0的行，返回Series

    df.loc[[0, 2]] # 指定索引值index = 0和index = 2的行，返回DataFrame

    df.loc[0: 3] # 指定索引值index从0到2的行，返回DataFrame

    df.loc[df['name'] == 'Sisyphus'] # 指定name为Sisyphus的所有行所有列，返回DataFrame

    df.loc[df['name'] == 'Sisyphus', 'gender'] # 指定name为Sisyphus的所有行的gender列，返回Series

    df.loc[df['name'] == 'Sisyphus', ['gender', 'rank'] # 指定name为Sisyphus的所有行的gender和rank列，返回DataFrame

##### II、且 / 或

    df.loc[(df['gender'] == 'male') & (df['rank'] == 'B')] # 多条件筛选，且

    df.loc[(df['rank'] == 'A') | (df['rank'] == 'B')] # 多条件筛选，或

##### III、包含 / 不包含

    df.loc[df['name'].str.contains('s')] # .str.contains，指定name中包含字符's'的所有行所有列

    df.loc[~ df['name'].str.contains('s')] # .str.contains，指定name中不包含字符's'的所有行所有列

    df.loc[df['name'].isin(list)] # .isin，指定name在list内的所有行所有列

##### IV、以xx开头

    df.loc[df['name'].str.startswith('s') # .str.startswith，指定name中以's'开头的所有行所有列

##### V、去重

    df['name'].unique() # 返回numpy.ndarray

    df['name'].unique().tolist() # 返回list

#### (2)、iloc

##### I、索引行

    df.iloc[0] # 指定索引值index = 0的行，返回Series

    df.iloc[[0, 2]] # 指定索引值index = 0和index = 2的行，返回DataFrame

    df.iloc[0: 2] # 指定索引值index从0到2的行，返回DataFrame

    df.iloc[[True, False, True]] # 指定对应为True的索引值，返回DataFrame

    df.iloc[lambda x: x.index % 2 == 0] # 指定能被2整除的索引值，返回DataFrame

##### II、索引单元格

    df.iloc[0, 1] # 指定0行1列的单元格，返回该单元格对应类型的对应值

    df.iloc[[0, 2], [1, 3]] # 指定0行2行和1列3列交叉的单元格，返回DataFrame

    df.iloc[1:3, 0:3] # 指定1行至2行和0列至2列交叉的单元格，返回DataFrame

    df.iloc[:, [True, False, True, False]] # 指定对应为True的列的所有行，返回DataFrame

    df.iloc[:, lambda df: [0, 2]] # 指定0列2列的所有行，返回DataFrame
