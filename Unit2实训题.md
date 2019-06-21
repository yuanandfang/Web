### 编写一个程序

可以让用户在窗体网页上输入名称、密码，若名称caterpillar且密码为123456，

则显示一个HTML页面相应并有“登录成功”字样，则显示“登录失败”字样，

否则显示“登录失败”字样，并由一个超链接连回窗体网页。

注意：不可在地址栏上出现用户输入的名称、密码。
UserDao.java
```
package nuc.dao;

import java.sql.ResultSet;
import java.sql.SQLException;

import nuc.entity.UserEntity;
import nuc.util.DB;

public class UserDao {
	public UserEntity getUserByName(String userName){
		String sql="select * from users where userName='"+userName+"'";
		DB db = new DB();
		ResultSet rs = null;
		rs = db.getRs(db.getSm(db.getConn()),sql);
		UserEntity ue = null;
		try {
			if(rs.next()){
				ue = new UserEntity();
				ue.setId(rs.getInt("Id"));
				ue.setUserName(rs.getString("userName"));
				ue.setPassWord(rs.getString("passWord"));
			}
		}catch(SQLException e){
			e.printStackTrace();	
		}
		return ue;
	}
}

```


form.jsp

```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<form method="post" action="./index.do">
		用户名:<input  name="userName" type="text">
		<br>
		密   码:<input name="userPassword" type="password" >
		<input type="submit" value="提交">
	</form>
</body>
</html>
```
