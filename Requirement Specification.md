# 需求规约

## 项目介绍

- 背景
随着软件工程的发展和技术进步，运维技术显得越发必要和不可替代。所有硬件设备都有寿命问题，而信息系统包含大量不同种类、不同功能、不同性能的设备，对信息系统而言，几乎在项目建设完成后即需进入项目运维期，而对某些建设周期需要很多年的信息系统来说，在项目建设后期，便要对前期建设的项目进行运维。系统软件、工具软件、系统软件自身可能存在缺陷，也需要主动监控、修正和完善。目前，zabbix提供的监控方案丰富而全面，然而监控项繁多，模版内含监控项原型存在很多我们不需要时刻了解的信息。
- 项目目标
在我们前期对zabbix、prometheus以及influxdb、grafana的调研之后，尝试利用zabbix提供的API进行二次开发，主要目的在于选取我们关心的、反应系统基础性能的监控项信息(如cpu负载和磁盘使用率等)，获取它们的数据并存储在influxdb中，通过grafana反应展示出他们的变化趋势，以便我们及时监控分析我们关心的数据，对系统健康性做出判断。此外，提供web界面的配置、查询以及下载数据等。
- 目标用户
运维人员，需要利用一定的监控方案掌握主机或系统基础性能或状态的运维团队。
- 项目边界
该项目目前实现以下几个方面
    1. 实现从已部署的zabbix抓取指定监控项信息
    2. 实现监控项数据的持久化存储
    3. 提供web界面供用户指定zabbix和influxdb的一些配置
    4. 监控项数据的查询与csv文件格式的展示
    5. 监控项数据的下载

## 项目需求分析

KAOS模型图如下

![KAOSD](https://raw.githubusercontent.com/VVphe/ZabbixWatcherDoc/master/images/KAOSD.png)

## 用例分析

用例图如下
![Use Case](https://raw.githubusercontent.com/VVphe/ZabbixWatcherDoc/master/images/usecase.png)

---

### Use Case: 登录zabbix

#### 描述

用户利用该用例连接到自己配置的zabbix

#### 参与者

用户

#### 前置条件

配置zabbix url

#### 后置条件

无

#### 基本事件流

![loginzabbix](https://raw.githubusercontent.com/VVphe/ZabbixWatcherDoc/master/images/loginzabbix.png)


---

### Use Case: 登录influxdb

#### 描述

用户利用该用例连接到influxdb

#### 参与者

用户

#### 前置条件

配置influxdb url

#### 后置条件

无

#### 基本事件流

![loginzabbix](https://raw.githubusercontent.com/VVphe/ZabbixWatcherDoc/master/images/logininflux.png)


---

### Use Case: 添加主机

#### 描述

用户利用该用例添加需要监控的主机

#### 参与者

用户

#### 前置条件

zabbix前端已部署该主机

#### 后置条件

主机添加成功，则开始调用zabbix api获取一些基础监控项数据

#### 基本事件流

![loginzabbix](https://raw.githubusercontent.com/VVphe/ZabbixWatcherDoc/master/images/confighost.png)


---

### Use Case: 添加数据库

#### 描述

用户利用该用例添加目标数据库

#### 参与者

用户

#### 前置条件

无

#### 后置条件

数据库添加成功，则将获取到的zabbix items数据存入到该数据库

#### 基本事件流

![loginzabbix](https://raw.githubusercontent.com/VVphe/ZabbixWatcherDoc/master/images/configdb.png)


---

### Use Case: 查询监控项数据

#### 描述

用户利用该用例在前端界面查询想要了解的监控项数据

#### 参与者

用户

#### 前置条件

已配置好正确的zabbix和influxdb

#### 后置条件

如果监控项存在，页面跳转，以csv文件的格式在前端展示数据

#### 基本事件流

![loginzabbix](https://raw.githubusercontent.com/VVphe/ZabbixWatcherDoc/master/images/searchitem.png)


---

### Use Case: 下载数据

#### 描述

用户利用该用例下载需要的监控项数据到本地

#### 参与者

用户

#### 前置条件

已正确配置好正确的zabbix和influxdb

#### 后置条件

无

#### 基本事件流

![loginzabbix](https://raw.githubusercontent.com/VVphe/ZabbixWatcherDoc/master/images/download.png)


---