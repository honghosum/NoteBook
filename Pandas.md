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
