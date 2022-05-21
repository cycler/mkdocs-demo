# 服务安装指南

关于API接口的说明，请查看官方文档： [ API 官方文档](https://docs.xxxxxxxx.com/api/index.html).


## 准备工作：

* AWS EC2 服务器 1台
* AWS RDS 数据库服务器 1台 （可选）
* AWS KMS
* Docker运行环境

## 安装过程
* 下载安装脚本
* 配置参数：workspace ID、
* 选择是否用docker版本的MySQL数据库，或者用独立的AWS RDS服务器（需要自行完成数据库创建和初始化）


## 启动服务 

* 激活API账号，需要配合管理员账号 完成

  1. 查看激活二维码文件

  2. 用户打开 App， 查看新用户激活任务，扫码步骤1获得的二维码，授权通过，完成激活。

* 检查服务是否正常启动

  服务已集成健康检查接口，可以在服务器上通过以下命令查看状态。

  

## 配置回调服务URL

![思维导图插入](./pic.png)

授权回调接口

客户需要提供用于交易授权回调接口，用来进行交易内容的校验和授权，每次交易都会回调此接口进行授权，通过之后才会进行 MPC 签名。

<table>
  <tbody>
  <tr>
    <th bgcolor="LightSalmon">接口请求说明</th>
    <th bgcolor="MintCream">接口响应说明</th>
  </tr>
  <tr>
    <td><font color="Grey">POST类型的请求，body内容为：
   `{
      String content;
      String key;
      String sig;
      String timestamp;
    }
</font></td>
<td><font color="Grey">返回值：
    `{
     String code;
     String content;
     String timestamp;
     String key;
    String sig;
    }
</font></td>
</tr>
</tbody>
</table>


请求参数解密方式请参考API文档。用户须对交易内容做校验，确认没问题则返回通过，有问题则返回拒绝。

TRANSACTION类型：

	{
	"type":"TRANSACTION",
	"customerContent":{
	    "businessKey":"e4cceb740e2f407bb520549a676c2893",
	    "triggerTime":1638532981615,
	    "triggerUserName":"我是一个饼",
	    "sourceAddress":"0xe67ee022b442e8483eb6fce0a870c1ca425e4f0f",
	    "sourceAccountKey":"account6e63dacbf80243118e425ce5363b31a3",
	    "sourceAccountName":"源账号名",
	    "destinationAccountKey":"011f6bdb5fe44eaeb3cedd86dfa5f732",
	    "destinationAccountName":"目标账号名",
	    "destinationAddress":"0x234diweoro234dsdssdsdsdsssds",
	    "note":"我是一个备注",
	    "customerRefId":"xxxxxxxxxxxx",
	}
	}
