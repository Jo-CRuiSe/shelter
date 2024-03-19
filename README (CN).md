# Unpublished Posts Enhancement for Chirpy Theme

[![Gem Version](https://img.shields.io/gem/v/jekyll-theme-chirpy-customized-upe)][gem]&nbsp;
[![GitHub license](https://img.shields.io/github/license/cotes2020/chirpy-starter.svg?color=blue)][mit]

*由 [Chirpy][chirpy] 主题改编*

## 为什么需要这个变体？

我在使用Chirpy主题时发现了一些与我习惯不同的和仍缺失的功能，包括访问博客登录（当前仓库应设置为私密，或者部署到自己的服务器上）、Mathjax插件增强，更改UI样式等。同时，这也是对我的前端代码能力的一次挑战。

> 接下来的步骤与Chirpy文档类似

## 安装

### 创建一个新的URL

登录GitHub并浏览到[**unpublished-posts-enhancement**](https://github.com/Jo-CRuiSe/unpublished-posts-enhancement)页面，点击按钮<kbd>[Use this template][use-template]</kbd> > <kbd>Create a new repository</kbd>，然后为新的存储库命名，以表示您未发布的帖子页面的URL。

### 安装依赖项

在第一次运行本地服务器之前，进入您站点的根目录并运行以下命令：

```console
$ bundle
```

## Usage

在发布之前，您可能希望预览站点的内容，只需运行以下命令：

```console
$ bundle exec jekyll s
```

几秒钟后，本地服务将发布在 [http://127.0.0.1:4000](http://127.0.0.1:4000)。

## 部署

在开始部署之前，请查看 `_config.yml`文件，并确保 `url` 配置正确。记得将 `baseurl` 更改为以斜杠开头的项目名称，例如 `/project-name`。

现在，您可以选择以下方法之一来部署您的Jekyll站点。

### 使用 GitHub Actions 进行部署

准备一些事项：

- 如果您使用的是GitHub免费计划，请保持站点存储库为公开状态。
- 如果您已经将 `Gemfile.lock`提交到存储库中，并且您的本地机器不是运行Linux，请转到站点的根目录，并更新锁定文件的平台列表：

  ```console
  $ bundle lock --add-platform x86_64-linux
  ```

接下来，配置 _Pages_ 服务。

1. 浏览到您的GitHub存储库。选择选项卡 _Settings_，然后在左侧导航栏中点击 _Pages_。在 **Source** 部分（位于 _Build and deployment_ 下方），从下拉菜单中选择 [**GitHub Actions**][pages-workflow-src]。

2. 推送任何提交到GitHub以触发 _Actions_ 工作流程。在存储库的 _Actions_ 选项卡中，您应该看到 _Build and Deploy_ 工作流正在运行。一旦构建完成并成功，站点将自动部署。

此时，您可以前往GitHub指定的URL访问您的站点。

### 手动构建和部署

在自托管服务器上，您无法享受 **GitHub Actions** 的便利。因此，您应该在本地机器上构建站点，然后将站点文件上传到服务器。

进入源项目的根目录，并按以下方式构建站点：

```console
$ JEKYLL_ENV=production bundle exec jekyll b
```

除非您指定了输出路径，否则生成的站点文件将放置在项目根目录的 `_site`文件夹中。现在，您应该将这些文件上传到目标服务器。

## 配置

[此博客](https://jo-cruise.github.io/2024-02-06-HowToUseUPE)将指导您完成相关配置。

## 许可证

此作品以 [MIT][mit] 许可证发布。

[gem]: https://rubygems.org/gems/jekyll-theme-chirpy-customized-upe
[chirpy]: https://github.com/cotes2020/jekyll-theme-chirpy/
[use-template]: https://github.com/Jo-CRuiSe/unpublished-posts-enhancement/generate
[CD]: https://en.wikipedia.org/wiki/Continuous_deployment
[mit]: https://github.com/Jo-CRuiSe/jekyll-theme-chirpy-customized-upe/blob/master/LICENSE
