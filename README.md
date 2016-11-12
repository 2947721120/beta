# webcomponents.org beta
<p align="center">
  <img alt="webcomponents.org" src="https://beta.webcomponents.org/assets/logo.svg" width="161">
</p>
<p align="center">
  <a href="https://travis-ci.org/webcomponents/beta"><img src="https://img.shields.io/travis/webcomponents/beta.svg?maxAge=2592000&style=flat-square"></a>
  <img src="https://img.shields.io/hexpm/l/plug.svg?maxAge=2592000&style=flat-square">
  <a href="https://gitter.im/webcomponents/community"><img src="https://img.shields.io/gitter/room/webcomponents/community.svg?maxAge=2592000&style=flat-square"></a>
</p>
---



web components.org的beta（开发中）网站。
它由多个Appengine服务组成，需要gcloud进行大多数开发.

在高层次，服务是
- 管理，一个Python服务，处理来自Bower，Github和Analysis的摄取数据的管理。
- Api，一种Python服务，提供客户端使用的REST API，以从Manage访问数据。
- 客户端，Polymer Web应用程序，它提供用户界面并消耗Api的数据。
- Analysis，一个node.js服务，使用Bower和Hydrolysis对所摄取的元素执行较慢的分析。

＃系统级依赖
需要以下依赖关系来开发，测试和/或部署beta.webcomponents.org
- 所有服务都需要gcloud SDK（https://cloud.google.com/sdk/downloads#versioned）
- node.js（和npm）（https://nodejs.org/en/download/） - 所有服务都需要
- pip（Linux：https://packaging.python.org/install_requirements_linux/，Mac：“sudo easy_install pip”或https://pip.pypa.io/en/stable/installing/） - 需要管理和Api
- bower（“npm install -g bower”） - 客户端需要
- grunt（“npm install -g grunt”） - 运行lint所需的

#  依赖
```bash
npm install
```
或者，您可以使用纱线更快的构建:
```bash
yarn
```

## 客户和分析
有关说明，请查看其子目录 `client/` and `analysis/`.

## 运行测试
```bash
python tests.py $APPENGINE_SDK
```

## 部署
要增加Github API配额，获取一个Github令牌并存储它:
```bash
cat > secrets.yaml
github_token: 'your-github-token'
```

如果您想使用reCAPTCHA，请获取令牌并存储它:
```bash
cat > secrets.yaml
recaptcha: 'your-token'
```

部署到暂存.
```bash
grunt lint #lints both client and python
appcfg.py update_dispatch dispatch.yaml
appcfg.py update manage.yaml
appcfg.py update api.yaml
```

根据他们的文档部署客户端和分析.
