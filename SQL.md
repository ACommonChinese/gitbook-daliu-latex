# 存储过程


忘记MySQL密码:
参考: [https://www.jianshu.com/p/8b8a2d0a2051](https://www.jianshu.com/p/8b8a2d0a2051)

1. `sudo vim /etc/my.cnf`  在mysqld下添加: `skip-grant-tables`并保存
2. 点击电脑端系统偏好设置中的MySQL图标并输入电脑密码开启MySQL
3. `mysql -u root -p` 不需要密码直接按回车
4. 使用sql语句修改密码:
```sql
# 示例:
mysql> update mysql.user set authentication_string=password('110') where user='root';
```
5. 重新编辑 `/etc/my.cnf`删除刚加入的`skip-grant-tables`, 重启MySQL

参考链接: [https://www.jianshu.com/p/d7dead4be9b8](https://www.jianshu.com/p/d7dead4be9b8)

含义：一组预先编译好的SQL语句的集合，理解成批处理语句
1、提高代码的重用性
2、简化操作
3、`减少了编译次数并且减少了和数据库服务器的连接次数，提高了效率

### 创建

```sql
create procedure 存储过程名(参数列表)
begin # 如果存储过程体仅仅只有一句话, begin和end可以省略
	存储过程体
end
```

**参数列表**
参数列表包含三部分
1. 参数模式
2. 参数名
3. 参数类型

参数模式:
in：该参数可以作为输入，也就是该参数需要调用方传入值
out：该参数可以作为输出，也就是该参数可以作为返回值
inout：该参数既可以作为输入又可以作为输出，也就是该参数既需要传入值，又可以返回值

**存储过程体**
存储过程体是一组合法的SQL语句), 每条sql语句都要加分号作做语句结束标记.
存储过程的结尾可以使用`delimiter`重新设置, 语法:

```sql
delimiter $ # 以$作为结束标记
```

### 调用

`call 存储过程名(实参列表);`

### 创建和使用示例

