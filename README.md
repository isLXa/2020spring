# 后端  

### 数据库操作  

#### 连接  

 - 连接  

   ```python
   con=pymysql.connect(db['host'],db['user'],db['passwd'],db['database'],charset='utf8')
   ```

   连接数据库，```dp```是从```config.py```引入的块，其实就是一个字典

   ```python
   # 得到一个可以执行SQL语句的光标对象
   cursor = conn.cursor()  # 执行完毕返回的结果集默认以元组显示
   # 得到一个可以执行SQL语句并且将结果作为字典返回的游标
   ```

   创建光标

- 关闭

  ```python
  # 关闭游标
  cur.close()
  # 关闭数据库
  conn.close()
  ```

#### 增  

 - 第一种:

   ```python
   #本次任务代码
   cursor.execute("INSERT INTO users (username, sex, grade, location, academy, phone, first, second, adjust, time, introduce)"
                      "VALUES (%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)",
                      (username, sex, grade, location, academy, phone, first, second, adjust, time, introduce))
   #增，mysql模板代码
   cursor.execute("insert into 插入数据库对应表名 (参数1，参数2....) value(%s,%s...)"，%变量名称1，%2)
   #上述代码不建议，因为防止不了SQL注入
   cursor.execute("insert into 插入数据库对应表名 (参数1，参数2....) value(%s,%s...)"，(变量1，变量2))
   #使用元组可避免上述结果
   con.commit()#注意是con，而不是curcos，执行这语句后，数据才能插入数据库
   ```

   

 - 第二种：

   ```python
   sql="""
   insert into 插入数据库对应表名 (参数1，参数2....) value(%s,%s...)"，%变量名称1，%2
   """#使用代码块格式
   cursor.execut(sql)
   con.commit()#作用与上面一致，但注意虽然有时候sql语句不需要"""。。。。"""但有时会出现错误，目前原因不知
   ```

- 第三种：

  ```python
  #一次性插入许多行，val是一个元组列表
  mycursor.executemany(sql, val)
  ```

  

#### 删

​	**与上面相似，也可以分为两种**

​	模板代码：

```python
cursor.execute("delete from students where name='王钢蛋'")
```



#### 改

​	模板代码：

```python
cursor.execute("update 表名 set name = 'xxx where name = 'xxx'";)
#where是添加修饰条件，当条件符合时，才能影响数据库
```



#### 查

​	模板代码：  

```python
cursor.execute( 'select * from users where phone = %s', (tel,))#返回一个元组，像数组一样的东西，可通过循环语句对它进行遍历取值
cursor.rowcount = cursor.execute(sql)#本质是获得sql语句影响数据库表的行数
result = cursor.fetchone()#本质是获得sql影响数据库表行数的第一行，返回元组格式，故result是一个元组
#显然也有获得全部影响行数的
result = cursor.fetchall()
result = fetchmany(4)#获得指定数目的数据
```

### 代码规范

#### 文件分布

- 注意代码的封装与保护，配置信息可专门存储在一个 <code style="color:red">config</code> 文件，密码要进行加密，千万不能再集合到一个文件中
- 有关数据库的操作，用```database.py```来封装，不同的操作集合成函数，通过参数传递值
- 实例化flask，封装入```app.py``` 文件

#### 命名规范

- 一个项目内只能保留一种命名方式，便于理解，常常采用驼峰式命名
- 该注释注释，记好修改的地方，避免出现bug找不到
- 代码不规范，debug火葬场，不能像竞赛一样为了代码的简洁而删去空行，要学会保留

### debug

#### 查找bug

- 通过对于可能出现bug的前后位置，设置```print()```定位bug
- 仔细查看错误信息，不懂百度，懂的靠经验，再不行仔细对比修改的地方

#### 记录bug

- 出现bug是无法避免的，为了避免再次出现bug和出现bug不会改，应对bug进行一定程度的记录

# bug记录

<code style="color:red;fontsize:100px">**遇到就加**</code>

