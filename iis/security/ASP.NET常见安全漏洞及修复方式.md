## Microsoft IIS 版本信息泄露

查看网页返回的 Header 信息，默认会包含 IIS，ASP.NET 版本信息：

![alt text](image.png)

### 隐藏 Server 标头


编辑 web.config 文件，在 system.webServer 节点中配置 requestFiltering 来移除Server标头：：

```diff
<security>
+  <requestFiltering removeServerHeader ="true" />
</security>
```

### 隐藏 X-ASPNET-Version 标头

编辑 web.config 文件，在 system.web 节点， 添加以下配置代码：

```diff
<system.web>
+  <httpRuntime enableVersionHeader="false" />
</system.web>
```

### 隐藏 X-Powered-By 标头

编辑 web.config 文件，在 system.webServer.customeHeaders 节点， 添加以下代码：

```diff
<system.webServer>
  <httpProtocol>
    <customHeaders>
+	    <remove name="X-Powered-By" />
    </customHeaders>
  </httpProtocol>
 </system.webServer>
```

修改完响应 Header 如下所示：

![alt text](image-1.png)

## 其他

### 增加 IP 地址黑名单

首先打开“服务器管理器”中，进入“管理”，点击“添加角色和功能”，在“服务器角色”的 Web服务器/Web服务器/安全性 中找到 “IP和域限制”，勾选并安装。

![alt text](image-2.png)

安装成功后，在 IIS 中点击对应的网站，右侧面板中找到 “IP和域限制”，

![alt text](image-3.png)

双击进入，右键添加拒绝条目即可。

![alt text](image-4.png)