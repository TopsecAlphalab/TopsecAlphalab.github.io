# qdPM9.1 Installer Cross-Site-Scripting

## 一、	背景介绍
qdPM是一个免费的基于Web的项目管理工具，适用于从事多个项目的小团队。可自由配置，从而轻松管理项目，任务和人员。 1.1 漏洞描述
qdPM安装页面由于参数过滤不严格，导致反射型xss。
### 1.2 受影响的系统版本
qdPM 9.1
## 二、环境搭建
1.通过官网http://qdpm.net/download-qdpm-free-project-management下载网站源码
2.将源码解压到web目录下并访问，如下：
 
## 三、漏洞分析
网站安装过程中的数据库配置文件为qdPM\install\modules\database_config.php，如下图所示，可以看到当db_error为真时，会将db_error的值输出到页面，在此过程中，没有进行任何过滤，这导致了发射型xss：
 
## 四、漏洞利用
1.访问网站：
 
2.点击database config按钮并输入错误的数据库信息：
 
3.提交之后，我们可以看到db_error信息输出在页面上：
 
4.构造payload url：http://127.0.0.1/qdPM/install/index.php?step=database_config&db_error=<img src=x onerror=alert(1) /> 并对其访问
5.可以看到，xss成功执行：
 

