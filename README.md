# S2-052（CVE-2017-9805）
struts2 052远程代码执行漏洞POC利用（影响版本：Struts 2.1.2 - Struts 2.3.33, Struts 2.5 - Struts 2.5.12）<br/>
官方介绍：https://cwiki.apache.org/confluence/display/WW/S2-052<br/>
此POC是在struts-2.5.12版本测试验证的。<br/>
1、搭建测试环境<br/>
下载struts2.5.12版本：http://archive.apache.org/dist/struts/2.5.12/
下载apache-tomcat 这里用的是8.5.20版，这是绿色非安装板，配置即可使用，具体配置网上很多资料可参考这里不介绍。
将struts2-rest-showcase.war放到webapps目录下。conf目录下server.xml默认配置如下：
<Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">

        <!-- SingleSignOn valve, share authentication between web applications
             Documentation at: /docs/config/valve.html -->
        <!--
        <Valve className="org.apache.catalina.authenticator.SingleSignOn" />
        -->

        <!-- Access log processes all example.
             Documentation at: /docs/config/valve.html
             Note: The pattern used is equivalent to using pattern="common" -->
        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log" suffix=".txt"
               pattern="%h %l %u %t &quot;%r&quot; %s %b" />
</Host>
然后访问http://127.0.0.1:8080/struts2-rest-showcase/orders.xhtml <br/>
如果上述都顺利的话可以看到Orders可编辑界面，下面是POC测试过程。<br/>
点击编辑，进入到修改界面，点击"提交"抓包，然后修改Content-Type为application/xml格式，post数据替换为poc中data提交即可弹计算器了。<br/>
Notes:<br/>
Windows下关键字为：<br/>
<command>											<string>calc</string>										</command><br/>
Mac下关键字为：<br/>
<command>
<string>/Applications/Calculator.app/Contents/MacOS/Calculator</string>
</command><br/>
![calc](https://raw.githubusercontent.com/cyjaysun/S2-052/master/img/calc.jpg)
