# 数据库操作 #

## 获取数据库操作对象

`$db = app::get('base')->database();`或者`$db = app::get('当前app名称')->database();`

## 根据sql语句操作

### 查询操作

#### 1.获取单条数据,返回关联数组格式

$sql = "SELECT *  FROM table_full_name WHERE id = 1";   
$res = $db->fetchAssoc($sql);

#### 2.获取单条数据,返回集合数组格式

$sql = "SELECT *  FROM table_full_name WHERE id = 1";   
$res = $db->fetchArray($sql);

#### 3.获取多条数据

$sql = "SELECT *  FROM table_full_name";   
$res = $db->fetchAll($sql);

### 添加、更新、删除

//执行一条SQL语句并返回受影响的行数。  
$row = $db->exec($sql); 

//使用给定的参数执行SQL插入/更新/删除查询，并返回受影响的行数。  
//该方法支持PDO绑定类型和DBAL映射类型。  
$row = $db->executeUpdate($sql); 

