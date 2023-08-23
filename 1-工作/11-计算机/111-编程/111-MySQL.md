# MySQL


## 用户管理
user表
* MySQL自带，存储用户信息
* 重要字段
	1. host：允许登录的位置（本机localhost，ip地址）
	2. user：用户名
	3. authentication_string：密码（通过mysql的passwora()函数加密后）

用户管理语句
* 创建用户：`create user '用户名'@'允许登录位置' identified by '密码';`
* 删除用户：`drop user '用户名'@'允许登录位置';`
* 登录：`mysql -h localhost -u 用户名 -p`，然后输入密码
	- 直接在一条指令里写密码：`-p密码`，注意没有空格
* 修改密码`alter user '用户名'@'允许登录位置' identified by '密码';`

## 权限管理
一些权限举例：
* all \[privileges\]：除grant_option外的所有简单权限
* alter：alter table
* create：创建表
* create user：创建和删除用户
* delete：允许使用delete
* 等等等……

用户授权及权限回收
* `grant 权限列表 on 库.对象名 to '用户名' @'登陆位置' [identified by '密码'];`
	- 可选项的作用：如果用户存在，修改密码；如果不存在，创建用户
* `revoke 权限列表 on 库.对象名 from '用户名' @'登陆位置';`

## 日期函数
`NOW()`：返回当前日期和时间，例如2017-07-25 21:51:54

`DATE()`：将日期和时间截取日期部分，用法例如`DATE(NOW())`

`DATE_ADD() / DATE_SUB()`：将日期值加上/减去几天/周/月/年，用法例如`DATE_ADD('2018-01-01', INTERVAL 1 MONTH)`

## ODBC
mysql安装包自带Connector/ODBC

连接方法：
有两台机器A和B，数据库在B上，A要通过ODBC访问B；
在A的mysql上创建用户，**权限为all**
在B上配置Connector/ODBC DSN，参数与A新建的用户对应

### ODBC 数据源管理器
Microsoft的Windows系统自带
直接搜索ODBC，在“用户DSN”里添加，选择相应数据源

### 使用C++连接
需要的库：odbc32.dll或odbc32.lib
* 我的电脑上，路径为：`C:\Windows\System32\odbc32.dll`

需要包含的头文件：sql.h，sqlext.h

### 数据类型
ODBC使用两组数据类型：
1. SQL数据类型：类型标识符例如SQL_CHAR
2. C数据类型：类型标识符例如SQL_C_CHAR

SQL数据源中使用了C数据类型，而C数据类型在应用程序的C代码中使用

### 准备硬编码的SQL语句
```c++
#define DESC_LEN 51
SQLCHAR *Statement = "INSERT INTO Parts (PartID, Description,  Price) "
         "VALUES (?, ?, ?)";
SQLUINTEGER   PartID;
SQLCHAR       Desc[DESC_LEN];
SQLREAL       Price;
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;

// Prepare the INSERT statement.
SQLPrepare(hstmt, Statement, SQL_NTS);

// Bind the parameters.
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,
                  &PartID, 0, &PartIDInd);
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,
                  Desc, sizeof(Desc), &DescLenOrInd);
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,
                  &Price, 0, &PriceInd);

// Loop to continually get new values and insert them.
while (GetNewValues(&PartID, Desc, &Price))
   SQLExecute(hstmt);
```
直接执行语句：`SQLExecDirect(hstmt, Statement, SQL_NTS);`，Statement自行构造（例如用sprintf_s）

### 提取结果
```c++
SQLCHAR       SalesPerson[11];
SQLUINTEGER   CustID;
SQLINTEGER    SalesPersonLenOrInd, CustIDInd;
SQLRETURN     rc;
SQLHSTMT      hstmt;

// Bind SalesPerson to the SalesPerson column and CustID to the
// CustID column.
SQLBindCol(hstmt, 1, SQL_C_CHAR, SalesPerson, sizeof(SalesPerson),
            &SalesPersonLenOrInd);
SQLBindCol(hstmt, 2, SQL_C_ULONG, &CustID, 0, &CustIDInd);

// Execute a statement to get the sales person/customer of all orders.
SQLExecDirect(hstmt, "SELECT SalesPerson, CustID FROM Orders ORDER BY SalesPerson",
               SQL_NTS);

// Fetch and print the data. Print "NULL" if the data is NULL. Code to
// check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {
   if (SalesPersonLenOrInd == SQL_NULL_DATA)
            printf("NULL                     ");
   else
            printf("%10s   ", SalesPerson);
   if (CustIDInd == SQL_NULL_DATA)
         printf("NULL\n");
   else
            printf("%d\n", CustID);
}

// Close the cursor.
SQLCloseCursor(hstmt);
```

游标：
* 在ODBC中，当执行创建结果集的语句时，将隐式打开游标。当游标打开时，它将定位在结果集的第一行之前。在嵌入的SQL和ODBC中，应用程序使用完游标后必须将其关闭。
* 默认：只进游标（只能向前滚动，要想返回只能重新打开）

SQLFetch
* 注意：NULL值返回的是SQL_NULL_DATA

### 诊断
#### 返回代码
ODBC的每个函数都返回一个代码（返回代码），指示函数的整体成功或失败

返回代码包括：
* SQL_SUCCESS
* SQL_SUCCESS_WITH_INFO
* SQL_ERROR
* SQL_INVALID_HANDLE
* SQL_NO_DATA
* SQL_NEED_DATA
* SQL_STILL_EXECUTING

#### 诊断记录
包含：使用特定句柄的最后一个函数的诊断信息

两种诊断记录
* 标头记录：记录0，函数执行的一般信息，始终会返回（除非函数返回SQL_INVALID_HANDLE）
* 状态记录：记录1及以上，特定错误或警告的信息，当返回SQL_ERROR、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_NEED_DATA或SQL_STILL_EXECUTING时创建

#### SQLGetDiagRec 或 SQLGetDiagField
```c++
SQLCHAR       SqlState[6], SQLStmt[100], Msg[SQL_MAX_MESSAGE_LENGTH];
SQLINTEGER    NativeError;
SQLSMALLINT   i, MsgLen;
SQLRETURN     rc1, rc2;
SQLHSTMT      hstmt;

// Prompt the user for an SQL statement.
GetSQLStmt(SQLStmt);

// Execute the SQL statement and return any errors or warnings.
rc1 = SQLExecDirect(hstmt, SQLStmt, SQL_NTS);
if ((rc1 == SQL_SUCCESS_WITH_INFO) || (rc1 == SQL_ERROR)) {
   SQLLEN numRecs = 0;
   SQLGetDiagField(SQL_HANDLE_STMT, hstmt, 0, SQL_DIAG_NUMBER, &numRecs, 0, 0);
   // Get the status records.
   i = 1;
   while (i <= numRecs && (rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,
            Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {
      DisplayError(SqlState,NativeError,Msg,MsgLen);
      i++;
   }
}

if ((rc1 == SQL_SUCCESS) || (rc1 == SQL_SUCCESS_WITH_INFO)) {
   // Process statement results, if any.
}
```
