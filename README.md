> 中文翻译：曾毅 (https://github.com/studyzy/)

## 可验证凭证（Verifiable Credentials）数据模型与表示

凭证是我们日常生活的一部分；驾照用于证明我们有能力驾驶机动车辆，大学学位可用于证明我们的教育水平，政府颁发的护照使我们能够在国家之间旅行。本规范提供了一种在 Web 上表达此类凭证的机制，该机制具有密码学安全性、隐私保护性和机器可验证性。

我们鼓励符合[贡献指南](CONTRIBUTING.md)的贡献。虽然我们更倾向于在 GitHub 仓库中创建议题和拉取请求，但讨论也会在 [public-vc-wg](http://lists.w3.org/Archives/Public/public-vc-wg/) 邮件列表中进行。

## Verifiable Credentials Working Group
* 工作组页面：[https://www.w3.org/2017/vc/WG/](https://www.w3.org/2017/vc/WG/)
* 章程：[https://www.w3.org/2022/06/verifiable-credentials-wg-charter.html](https://www.w3.org/2022/06/verifiable-credentials-wg-charter.html)
* 主席
  * Brent Zundel - @brentzundel

### 可验证凭证 GitHub 仓库
* [用例](https://github.com/w3c/vc-use-cases)
* [数据模型](https://github.com/w3c/vc-data-model)
* [实现指南](https://github.com/w3c/vc-imp-guide/)
* [数据模型测试用例](https://github.com/w3c/vc-test-suite)

### 讨论论坛
* [W3C Credentials Community Group 邮件列表（孵化）](https://lists.w3.org/Archives/Public/public-credentials/)
* [W3C Verifiable Credentials WG 邮件列表（标准化）](https://lists.w3.org/Archives/Public/public-vc-wg/)

## 可验证凭证数据模型拉取请求流程概述
1. 任何人都可以在该仓库上提交拉取请求。请注意，要合并拉取请求，提交者必须同意 [W3C 专利政策](https://www.w3.org/Consortium/Patent-Policy/)。
2. 一旦在 `v2.0` 分支上打开拉取请求，主席和编辑将判断变更是实质性的还是编辑性的。
   <dl>
     <dt>编辑性变更</dt>
     <dd>标记 "editorial" 标签</dd>
     <dt>实质性变更</dt>
     <dd>标记 "substantive" 标签。</dd>
   </dl>
3. W3C CCG 会在拉取请求提出和讨论时自动收到通知。
4. 如果有充分的审查和共识（由主席和编辑确定），拉取请求通常在 7 天内合并。

### 2022-2024 路线图

VCWG 在最新的 [VCWG 章程](https://www.w3.org/2022/06/verifiable-credentials-wg-charter.html)中列出了一组[交付物](https://www.w3.org/2022/06/verifiable-credentials-wg-charter.html#deliverables)和[时间线](https://www.w3.org/2022/06/verifiable-credentials-wg-charter.html#timeline)。

### 调试 Github Pages 构建错误

有时 Github Pages 会构建失败并显示不明确的错误信息，例如 "Page build error." 或 "Symlink does not exist within your site's repository"。您需要在本地运行 github-pages 来调试此类错误。要运行使用 Ruby 和 Jekyll 的 github-pages，您需要[设置可用的 Ruby 和 Bundle 环境](https://help.dreamhost.com/hc/en-us/articles/115001070131-Using-Bundler-to-install-Ruby-gems)。

安装 Ruby 和 Bundle 之后，您需要执行以下操作：

```
gem install jekyll github-pages
```

然后在顶层目录创建一个 `Gemfile` 文件，内容如下：

```
source 'https://rubygems.org'
gem 'github-pages'
```

然后运行以下命令：

```
bundle exec jekyll serve --watch --force_polling
```

运行上述命令后，您应该能够看到详细的页面构建错误信息。

### 本地开发

本规范使用 [`respec`](https://respec.org/) 构建。

要进行本地开发，首先安装 `respec`；然后，您可以在项目根目录下使用以下命令在本地构建规范：

```sh
respec --localhost index.html out.html --verbose -e
```

接下来在 Web 浏览器中打开 `out.html` 并查看文档。
