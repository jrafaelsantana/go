---

copyright:
  years: 2017
lastupdated: "2017-09-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# 入門指導教學

* {: download} 恭喜，您已在 {{site.data.keyword.Bluemix}} 上部署 Hello World 範例應用程式！若要開始使用，請遵循本逐步手冊。或者，<a class="xref" href="http://bluemix.net" target="_blank" title="（下載範例程式碼）"><img class="hidden" src="../../images/btn_starter-code.svg" alt="下載應用程式碼" />下載範例程式碼</a>，並自行探索。

遵循 Go 入門指導教學，您將設定開發環境、在本端及 {{site.data.keyword.Bluemix}} 上部署應用程式，以及在應用程式中整合 {{site.data.keyword.Bluemix}} 資料庫服務。

## 開始之前
{: #prereqs}

您需要下列各項：
* [{{site.data.keyword.Bluemix_notm}} 帳戶](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git-scm.com/downloads){: new_window}
* [Go ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://golang.org/dl/){: new_window}

## 步驟 1：設定本端環境，並複製範例應用程式
{: #clone}

首先，我們將設定本端環境，方法是確保已經妥善設定所有 GO 環境變數。例如：
```
mkdir $HOME/work
export GOPATH=$HOME/work
export PATH=$PATH:$GOPATH/bin
```

切換路徑到 $GOPATH/src
```
mkdir $GOPATH/src
cd $GOPATH/src
```

現在您可以開始使用簡單 Go *hello world* 應用程式。複製儲存庫，並切換至範例應用程式所在的目錄。
```
go get github.com/IBM-Bluemix/get-started-go
```
{: pre}
```
cd github.com/IBM-Bluemix/get-started-go
```
{: pre}

瀏覽 *get-started-go* 目錄中的檔案，以熟悉內容。

## 步驟 2：在本端執行應用程式
{: #run_locally}

  {: pre}

  建置及執行應用程式。
  ```
make
  ```
  {: pre}

  ```
go run main.go
  ```
  {: pre}

  在下列網址檢視您的應用程式：http://localhost:8080

使用 *Ctrl-c*，從您啟動應用程式的相同視窗中停止應用程式。
{: tip}

## 步驟 3：準備應用程式以進行部署
{: #prepare}

若要部署至 {{site.data.keyword.Bluemix_notm}}，它有助於設定 manifest.yml 檔案。manifest.yml 包括應用程式的基本資訊（例如名稱、配置給每一個實例的記憶體數量，以及路徑）。我們已在 `get-started-go` 目錄中提供範例 manifest.yml 檔案。

開啟 manifest.yml 檔案，然後將 `name` 從 `GetStartedGo` 變更為您的應用程式名稱 <var class="keyword varname" data-hd-keyref="app_name">app_name</var>。
{: download}

  ```
 applications:
 - name: GetStartedGo
   random-route: true
   memory: 128M
   buildpack: go_buildpack
  ```
  {: codeblock}

在此 manifest.yml 檔案中，**random-route: true** 會為應用程式產生隨機路徑，以防止您的路徑與其他人發生衝突。如果您選擇這樣做，則可以將 **random-route: true** 取代為 **host: myChosenHostName**，並提供您選擇的主機名稱。[進一步瞭解...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 步驟 4：部署應用程式
{: #deploy}
您可以使用 Cloud Foundry CLI 來部署應用程式。

選擇您的 API 端點
   ```
cf api <API-endpoint>
   ```
   {: pre}

將指令中的 *API-endpoint* 取代為下列清單中的 API 端點。

|URL|地區|
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net| 美國南部|
| https://api.eu-gb.bluemix.net| 英國|
| https://api.au-syd.bluemix.net| 雪梨|
| https://api.eu-de.bluemix.net | 法蘭克福|

登入 {{site.data.keyword.Bluemix_notm}} 帳戶

  ```
cf login
```
  {: pre}

如果您無法使用 `cf login` 或 `bx login` 指令登入，因為您已有聯合使用者 ID，請使用 `cf login --sso` 或 `bx login --sso` 指令，用您的單一登入 ID 登入。若要進一步瞭解，請參閱[使用聯合 ID 登入](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id)。

從 *get-started-go* 目錄中，將應用程式推送至 {{site.data.keyword.Bluemix_notm}}
  ```
cf push
  ```
  {: pre}

這可能需要一分鐘。如果部署程序發生錯誤，則您可以使用指令 `cf logs <Your-App-Name> --recent` 進行疑難排解。

部署完成之後，您應該會看到一則訊息，指出應用程式正在執行。在 push 指令輸出中所列的 URL 檢視應用程式。您也可以發出 

   ```
cf apps
    ```
  {: pre}
  指令來檢視應用程式狀態，並且查看 URL。

## 步驟 5：新增資料庫
{: #add_database}

接下來，我們會將 NoSQL Database 新增至此應用程式並設定應用程式，因此，它可以在本端及 {{site.data.keyword.Bluemix_notm}} 上執行。

1. 在瀏覽器中，登入 {{site.data.keyword.Bluemix_notm}}。瀏覽至「儀表板」。按一下「名稱」直欄中的應用程式名稱，以選取該應用程式。
2. 依序按一下「連線」及「連接新服務」。
3. 在「資料及分析」區段中，選取 `Cloudant NoSQL DB`，然後建立服務。
4. 系統提示時，請選取「重新編譯打包」。{{site.data.keyword.Bluemix_notm}} 將重新啟動應用程式，並使用 `VCAP_SERVICES` 環境變數將資料庫認證提供給應用程式。只有在應用程式於 {{site.data.keyword.Bluemix_notm}} 上執行時，才能使用此環境變數。

環境變數可讓您分開部署設定與原始碼。例如，您可以將資料庫密碼儲存在原始碼中所參考的環境變數內，而不要將資料庫密碼寫在程式中。[進一步瞭解...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 步驟 6：使用資料庫
{: #use_database}
我們現在即將更新本端程式碼，使其指向此資料庫。我們將建立 JSON 檔案，用來儲存應用程式將使用的服務認證。只有在應用程式於本端執行時，才會使用此檔案。在 {{site.data.keyword.Bluemix_notm}} 中執行時，將會從 VCAP_SERVICES 環境變數中讀取認證。

1. 在 `get-started-go` 目錄中，建立稱為 `.env` 且具有下列內容的檔案：
  ```
  CLOUDANT_URL=
  ```
  {: pre}

2. 回到 {{site.data.keyword.Bluemix_notm}} 使用者介面，然後選取您的應用程式 ->「連線」-> Cloudant ->「檢視認證」

3. 只要將 `url` 從認證複製並貼入 `.env` 檔案的 `CLOUDANT_URL` 欄位中，並儲存變更。結果將如下：
  ```
  CLOUDANT_URL=https://123456789 ... bluemix.cloudant.com
  ```

4. 在本端執行應用程式。
  ```
go run main.go
  ```
  {: pre}

  在下列網址檢視您的應用程式：http://localhost:8080 您輸入至應用程式的任何名稱，現在都會新增至資料庫。

  本端應用程式及 {{site.data.keyword.Bluemix_notm}} 應用程式將會共用資料庫。在上述 push 指令輸出中所列的 URL 檢視 {{site.data.keyword.Bluemix_notm}} 應用程式。當您重新整理瀏覽器時，從任一應用程式新增的名稱應該會出現在這兩個應用程式中。


請記住，如果您不需要應用程式維持執行中，請停止它以避免產生任何非預期的費用。
{: tip}
