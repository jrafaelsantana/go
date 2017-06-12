---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Go
{: #go_runtime}

{{site.data.keyword.Bluemix}} の Go ランタイムには go_buildpack が採用されています。
go_buildpack は、Go アプリケーションのための完全なランタイム環境を提供します。
{: shortdesc}

go_buildpack は、アプリケーションに *.go という名前のファイルが含まれている場合に使用されます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、Go スターター・アプリケーションが用意されています。Go スターター・アプリケーションは、アプリケーションで使用可能なテンプレートを提供する、シンプルな Go アプリケーションです。スターター・アプリケーションを試し、Bluemix 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](/docs/cfapps/starter_app_usage.html)を参照してください。

## ランタイム・バージョン
{: #runtime_versions}

アプリケーションのルートにある Godeps/Godeps.json ファイルで GoVersion プロパティーを設定することにより、アプリケーションで使用する Go のバージョンを指定できます。例えば、次のように指定します。

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.6.1",
	"Deps": []
}
```
{: codeblock}
詳しくは、[『godep』](https://github.com/tools/godep){: new_window}を参照してください。

### 使用可能なバージョン:
{: #available_versions}

現在 {{site.data.keyword.Bluemix}} にインストールされている [Go ビルドパック](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.7.5){: new_window}では、以下のバージョンの Go が使用できます。

* 1.4.2
* 1.4.3
* 1.5.3
* 1.5.4
* 1.6
* 1.6.1

アプリケーションが、リストされていないバージョンの Go を必要とする場合は、外部の [Go ビルドパック](https://github.com/cloudfoundry/go-buildpack.git){: new_window}を使用してアプリケーションをデプロイできます。

# 関連リンク
{: #rellinks notoc}
## 一般
{: #general notoc}

* [The Go Programming Language](http://golang.org/){: new_window}
* [Cloud Foundry buildpack for the Go Language](https://github.com/cloudfoundry/go-buildpack){: new_window}
