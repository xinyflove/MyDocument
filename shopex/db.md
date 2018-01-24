# 数据库操作 #

具体操作在`Doctrine\DBAL\Connection`类Connection中

## 1. 获取数据库操作对象

`$db = app::get('base')->database();`或者`$db = app::get('当前app名称')->database();`

## 1.1 根据sql语句操作

### 1.1.1 查询操作

#### 1.1.1.1 获取单条数据,返回关联数组格式

$sql = "SELECT *  FROM table_full_name WHERE id = 1";   
$res = $db->fetchAssoc($sql);

#### 1.1.1.2 获取单条数据,返回集合数组格式

$sql = "SELECT *  FROM table_full_name WHERE id = 1";   
$res = $db->fetchArray($sql);

#### 1.1.1.3.获取单条数据,返回结果的第一行的单个列的值,用于返回计数结果

$sql = "SELECT COUNT(\*) FROM table_full_name WHERE id = 1";   
$res = $db->fetchColumn($sql);

#### 1.1.1.4.获取多条数据

$sql = "SELECT *  FROM table_full_name";   
$res = $db->fetchAll($sql);

### 1.1.2 添加、更新、删除

//执行一条SQL语句并返回受影响的行数。  
$row = $db->exec($sql); 

//使用给定的参数执行SQL插入/更新/删除查询，并返回受影响的行数。  
//该方法支持PDO绑定类型和DBAL映射类型。  
$row = $db->executeUpdate($sql); 

## 2.查询构建器

就是调用了`Doctrine\DBAL\Query`中的QueryBuilder类

$conn = db::connection();  
$qb = $conn->createQueryBuilder();

### 2.1 安全：安全防范SQL注入

调用方法传参，例如:

```
$res = $qb->select('*')
            ->from('sysstore_store')
            ->where('store_id = :store_id')
            ->setParameters(['store_id'=>'1'])
            ->execute()->fetch();
```

### 2.2 构建查询

\Doctrine\DBAL\Query\QueryBuilder 支持创建 SELECT，INSERT，UPDATE，和DELETE 查询，使用哪种类型的查询取决于您正在使用的方法。

#### 2.2.1 SELECT 查询 ：在你调用select()方法时开始

```
$qb->select('id', 'name')
    ->from('users');
    ->execute()
    ->fetch();//或fetchAll();多条
```

#### 2.2.2 INSERT, UPDATE 和 DELETE查询：

你可以通过表名 insert（$tableName）、update($tableName）和delete($tableName)：

```
$res = $qb->insert('sysstore_store')
            ->setValue('store_name', "'aa'")
            ->setValue('store_desc', "'bb'")
            ->execute();

$res = $qb->update('sysstore_store')
            ->set('store_name', "'mozzie'")
            ->set('store_desc', "'caffrey'")
            ->where('store_id = :store_id')
            ->setParameters(['store_id'=>'4'])
            ->execute();


$res = $qb->delete('sysstore_store')
            ->where('store_id = :store_id')
            ->setParameters(['store_id'=>'8'])
            ->execute();
```
