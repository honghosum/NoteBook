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

### 3、字典 / 列表

    dic = {'name': ['Sisyphus', 'Athena', 'Zeus', 'Hera', 'Lucifer'],
           'gender': ['male', 'female', 'male', 'female', 'male'],
           'rank': ['D', 'B', 'A', 'C', 'B']}

    li = [['Sisyphus', 'Athena', 'Zeus', 'Hera', 'Lucifer'],
          ['male', 'female', 'male', 'female', 'male'],
          ['D', 'B', 'A', 'C', 'B']]
          
    df = pandas.DataFrame(dic)
    
    df = pandas.DataFrame(li)
    
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

df.loc[<索引表达式>, <列表达式>]

##### I、常规筛选

    df.loc[0] # 指定索引值index = 0的行
    
    df.loc[[0, 2]] # 指定索引值index = 0和index = 2的行
    
    df.loc[0: 2] # 指定索引值index从0到2的行

    df.loc[df['name'] == 'Sisyphus'] # 指定name为Sisyphus的所有行所有列
    
    df.loc[df['name'] == 'Sisyphus', 'gender'] # 指定name为Sisyphus的所有行的gender列
    
    df.loc[df['name'] == 'Sisyphus', ['gender', 'rank'] # 指定name为Sisyphus的所有行的gender和rank列

##### II、且 / 或

    df.loc[(df['gender'] == 'male') & (df['rank'] == 'B')] # 多条件筛选，且

    df.loc[(df['rank'] == 'A') | (df['rank'] == 'B')] # 多条件筛选，或

##### III、包含 / 不包含

    df.loc[df['name'].str.contains('s')] # .str.contains，指定name中包含字符's'的所有行所有列

    df.loc[~ df['name'].str.contains('s')] # .str.contains，指定name中不包含字符's'的所有行所有列

##### IV、以xx开头

