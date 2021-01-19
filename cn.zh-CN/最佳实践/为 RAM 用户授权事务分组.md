# 为 RAM 用户授权事务分组

GTS 支持 RAM 用户，您可以使用 RAM 用户的账号使用 GTS，但需要先使用云账号（主账号）为 RAM 用户进行事务分组的授权。

云账号和 RAM 用户对于事务分组的权限说明如下：

-   只有主账号可以创建并拥有事务分组。
-   主账号可以将创建的事务分组授权给 RAM 用户。授权粒度为全部授权。
-   授权后，RAM 用户才可以在应用的 TxcTransactionScaner 中配置其帐号的 Access Key ID 和 Access Key Secret 来使用 GTS。
-   授权后，RAM 用户才可以在控制台查看相应事务分组的监控信息。

## 步骤一：新建授权策略

1.  登录 [RAM 控制台](https://ram.console.aliyun.com)。

2.  在左侧导航栏单击**权限策略管理**。

3.  在**权限策略管理**页面单击**创建权限策略**。

4.  在**新建自定义权限策略**页面输入**策略名称**、在**配置模式**下方单击**脚本配置**，然后在**策略内容**的模板中设置具体策略内容，然后单击**确定**。

    目前 GTS 提供两种授权策略：授权单个事务分组和授权全部事务分组。授权的示例请参见[授权策略示例](#section_twz_q73_ezr)。

    ![新建自定义授权策略](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1739944851/p93530.png)

5.  返回**权限策略管理**页面，在权限策略列表中查看新建的策略是否已存在。


## 步骤二：为 RAM 用户授权

1.  登录 [RAM 控制台](https://ram.console.aliyun.com)。

2.  在左侧导航栏选择**授权管理** \> **授权**。

3.  在**授权**页面单击**新增授权**。

4.  在**添加权限**页面输入**被授权主体**（RAM 用户），在**选择权限**下方选择**自定义策略**，在权限策略列表中选择之前新建的权限策略，单击**确定**。

    ![添加权限](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1739944851/p93533.png)

5.  返回**授权**页面，查看是否已经存在给 RAM 用户（被授权主体）授权对应的权限策略的记录。

    ![授权](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1739944851/p93534.png)


## 结果验证

完成为 RAM 用户授权事务分组后，使用 RAM 用户的账号登录 [GTS 控制台](https://txc.console.aliyun.com)，在左侧导航栏单击**事务总览**，在**事务总览**页面检查是否能查看并操作已授权的事务分组。

## 授权策略示例

-   示例 1：针对单个事务分组授权

    ```
    {
        "Statement": [
            {
                "Action": "*",
                "Effect": "Allow",
                "Resource": "acs:txc:*:xxxxx:vgroup/test1.xxxxx.QD"
            }
        ],
        "Version": "1"
    }            
    ```

    -   `Action` 和 `Effect` 字段无需填写。只需要填写 `Resource` 字段内容。
    -   `xxxxx` 为主帐号 ID。
    -   `test1.xxxxx.QD` 为事务分组的全名，可以在 GTS 控制台获取。
    这样一个授权策略授予某 RAM 用户后，该用户即可使用事务分组`test1.xxxxx.QD`。

-   示例 2：授权全部事务分组

    ```
    {
      "Statement": [
        {
          "Action": "*",
          "Effect": "Allow",
          "Resource": "acs:txc:*:xxxxx:vgroup/*"
        }
      ],
      "Version": "1"
    }               
    ```

    -   `Action` 和 `Effect` 字段无需填写。只需要填写 `Resource` 字段内容。
    -   `xxxxx` 为主帐号 ID。
    -   `vgroup/` 后面的 `*` 表示所有事务分组。
    这样一个授权策略授予某 RAM 用户后，RAM 用户即可使用主帐号的全部事务分组。


