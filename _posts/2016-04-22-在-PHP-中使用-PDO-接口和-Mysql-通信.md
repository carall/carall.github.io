---
layout: post
---
#  [PDO](http://www.php.net/manual/en/book.pdo.php) in [PHP](http://php.net/manual/en/index.php)

***

PHP和Mysql的合作很完美，在php中和mysql通信的接口有两套：PDO和mysqli，前者可以在其他数据库软件环境下使用，故介绍。

## 1. 建立连接

`$dbh=new PDO('mysql:host=localhost;dbname=test',$user,$pass);  ` **建立并返回一个 [PDO](http://php.net/manual/en/class.pdo.php) 实例!**

* 错误控制:  

`$dbh->setAttribute(PDO::ATTR_ERRMODE,PDO::ERRMODE_EXCEPTION);`  
`try{} catch(PDOException $e){die();}`

* 关闭连接:

`$dbh=null`

* Persistent connections

***
## 2.  SQL 查询语句

#### 2.1  exec()  

`$dbh->exec($sql)` 用于不会返回结果的查询语句

#### 2.2 query()  

当query有数据要返回时，如select，要使用：

`$dbh->query($sql)`  **会返回一个 [PDOStatement](http://php.net/PDOStatement) 实例(result set)**

#### 2.3 prepare()

当有变量要传入query语句时，要用prepare：

* `$stmt=$sbh->prepare("select :name,:Id from table_name");` 准备好sql语句，当然是含有变量的。

* `$stmt->bindParam(':name',$name);` 把变量赋值 
* `$result=$stmt->execute();` execute之后返回PDOStatement实例

***

## 3. 从 PDOStatement 实例中获取数据

#### 3.1 [fetch()](http://php.net/manual/en/pdostatement.fetch.php)  

#### 3.2 fetchAll()

#### 3.3 setFetchMode()  

#### 3.4 bindColumn()  

* `$result->bindColumn(1,$name)`  

****

## 4. Transaction
