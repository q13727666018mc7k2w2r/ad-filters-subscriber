<div align="center">
<h1>AD Filter Subscriber</h1>
  <p>无编程基础新手探索用，copy 修改Bibaiji大佬的规则
    
    广告过滤规则订阅器，整合不同来源的规则，帮助你快速构建属于自己的规则集~
  </p>
<!-- Badges -->
<p>
  <a href="https://github.com/fordes123/ad-filters-subscriber">
    <img src="https://img.shields.io/github/last-commit/fordes123/ad-filters-subscriber?style=flat-square" alt="last update" />
  </a>
  <a href="https://github.com/fordes123/ad-filters-subscriber">
    <img src="https://img.shields.io/github/forks/fordes123/ad-filters-subscriber?style=flat-square" alt="forks" />
  </a>
  <a href="https://github.com/fordes123/ad-filters-subscriber">
    <img src="https://img.shields.io/github/stars/fordes123/ad-filters-subscriber?style=flat-square" alt="stars" />
  </a>
  <a href="https://github.com/fordes123/ad-filters-subscriber/issues/">
    <img src="https://img.shields.io/github/issues/fordes123/ad-filters-subscriber?style=flat-square" alt="open issues" />
  </a>
  <a href="https://github.com/fordes123/ad-filters-subscriber">
    <img src="https://img.shields.io/github/license/fordes123/ad-filters-subscriber?style=flat-square" alt="license" />
  </a>
</p>

<h4>
    <a href="#a">项目说明</a>
  <span> · </span>
    <a href="#b">快速开始</a>
  <span> · </span>
    <a href="#c">规则订阅</a>
  <span> · </span>
    <a href="#d">问题反馈</a>
  </h4>
</div>

<br/>
<h2 id="a">📔 项目说明</h2>

本项目旨在整合不同来源的广告过滤规则，通过 `Github Action` 定时执行，拉取远程规则，去重和分类输出。
根据过滤规则的特性，本项目将规则分为 `DOMAIN`、`REGEX`、`MODIFY`、`HOSTS` 四种类型，它们之间互不包含， 你可在配置文件中自由的对四种类型进行组合：

- `DOMAIN`：基于域名的过滤规则，适用于几乎所有广告过滤工具
- `REGEX`：基于正则表达式的**域名过滤**规则，适用于主流广告过滤工具
- `MODIFY`：基于正则和其他修饰符的过滤规则，可以拦截页面上的特定元素，但不适用于DNS过滤
- `HOSTS`：基于 `HOSTS` 的过滤规则，适用于支持 `HOSTS` 的所有设备

<br/>
<h2 id="b">🛠️ 快速开始</h2>

### 示例配置

```yaml
application:
  rule:
    #远程规则订阅，仅支持http、https
    remote:
      - 'https://example.com/list.txt'
    #本地规则，请将文件移动到项目路径rule目录中
    local:
      - 'mylist.txt'
  output:
    file_header: |  #输出文件头, 占位符${name}将被替换为文件名，如all.txt,  ${date} 将被替换为当前日期
      [ADFS Adblock List]
      ! Title: ${name}
      ! Last Modified: ${date}
      ! Homepage: https://github.com/fordes123/ad-filters-subscriber/
    path: rule   #规则文件输出路径，相对路径默认从 项目目录开始
    文件:
      all.txt: #输出文件名
        - DOMAIN
        - REGEX
        - MODIFY
        - HOSTS
```

---
本程序基于 `Java17` 编写，使用 `Maven` 进行构建，你可以参照示例配置，编辑 `src/main/resources/application.yml`
，并通过以下任意一种方式快速开始：

#### **本地调试**

```bash
git clone https://github.com/fordes123/ad-filters-subscriber.git
cd ad-filters-subscriber
mvn clean
mvn spring-boot:run
```

#### **Github Action**

- fork 本项目
- 自定义规则订阅 (可选)
    - 参照示例配置，修改配置文件: `src/main/resources/application.yml`，注意本地规则文件应放入项目根目录 `rule` 文件夹
- 打开 `Github Action` 页面，选中左侧 `Update Filters` 授权 `Workflow` 定时执行(⚠ 重要步骤)
- 点击 `Run workflow` 或等待自动执行。执行完成后相应规则生成在配置中指定的目录下

#### **代码空间**

- 登录 `Github`，点击本仓库右上角 `代码` 按钮，选择并创建新的 `代码空间`
- 等待 `代码空间` 启动，即可直接对本项目进行调试

<br/>
<h2 id="c">🎯 规则订阅</h2>

**⚠ 本仓库不再提供规则订阅，我们更推荐 fork 本项目自行构建规则集.**

下面是使用了本项目进行构建的规则仓库，可在其中寻找合适的规则订阅:
<details>
<summary>点击查看</summary>
<ul>
    <li><a href="https://github.com/xndeye/adblock_list/">xndeye/adblock_list</a></li>
    <p>欢迎提交 issues 或 pr 留下你的仓库地址~</p>
</ul>
</details>

<br/>
<h2 id="d">💬 问题反馈</h2>

- 👉 [issues](https://github.com/fordes123/ad-filters-subscriber/issues)
