---

copyright:
  years: 2016, 2018
lastupdated: "2018-02-14"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 開始使用 {{site.data.keyword.openwhisk_short}}

{{site.data.keyword.openwhisk}} 是分散式、事件驅動計算服務，也稱為「無伺服器運算」或「函數即服務 (FaaaS)」。{{site.data.keyword.openwhisk_short}} 會執行應用程式邏輯，以回應來自 Web 或透過 HTTP 的行動應用程式的事件或直接呼叫。事件可以從 {{site.data.keyword.Bluemix}} 服務（例如 Cloudant）和外部來源提供。開發人員可以著重在撰寫應用程式邏輯，以及建立依需求執行的「動作」。
這個新參照範例的主要好處是您不用明確地供應伺服器。因此，不用擔心自動擴充、高可用性、更新、維護，以及為了伺服器在執行中但未處理要求的時間，負擔數小時的處理器時間成本。
有 HTTP 呼叫、資料庫狀態變更，或觸發執行程式碼的其他類型事件時，便會執行您的程式碼。不論 VM 是否執行有用的工作，都會依執行時間的毫秒（四捨五入至最接近的 100 毫秒）來向您收費，而非依每小時的 VM 使用率。
{: shortdesc}

這個程式設計模型最適合微服務、行動式、IoT 及許多其他應用程式。您預設會有既有的自動擴充及負載平衡，而不需要手動配置叢集、負載平衡器、http 外掛程式等。如果您剛好是在 {{site.data.keyword.openwhisk}} 上執行，則也會有零管理的好處，意思是 IBM 會維護所有的硬體、網路及軟體。您只需要提供您要執行的程式碼，並將它交給 {{site.data.keyword.openwhisk}}。剩下的就是「魔法」。[Martin Fowler 部落格](https://martinfowler.com/articles/serverless.html)充分地介紹了無伺服器程式設計模型。

您也可以取得 [Apache OpenWhisk 原始碼](https://github.com/openwhisk/openwhisk)，並自行執行系統。

如需 {{site.data.keyword.openwhisk_short}} 運作方式的詳細資料，請參閱[關於 {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html)。

您可以使用「瀏覽器」或 CLI 來開發 {{site.data.keyword.openwhisk_short}} 應用程式。這兩者具有類似的功能可用來開發應用程式；CLI 可讓您進一步控制部署及作業。

## 在瀏覽器中開發
{: #openwhisk_start_editor}

請在[瀏覽器](https://console.{DomainName}/openwhisk/actions)中試用 {{site.data.keyword.openwhisk_short}} 來建立「動作」、使用「觸發程式」自動執行「動作」，以及探索公用套件。
如需「{{site.data.keyword.openwhisk_short}} 使用者介面」的快速導覽，請造訪[進一步瞭解](https://console.{DomainName}/openwhisk/learn)頁面。

## 使用 CLI 開發
{: #openwhisk_start_configure_cli}

您可以使用 {{site.data.keyword.openwhisk_short}} 指令行介面 (CLI) 來設定名稱空間及授權金鑰。移至[配置 CLI](https://console.{DomainName}/openwhisk/cli)，並遵循指示進行安裝。

## 概觀
{: #openwhisk_start_overview}
- [OpenWhisk 運作方式](./openwhisk_about.html)
- [無伺服器應用程式的常見使用案例](./openwhisk_use_cases.html)
- [設定及使用 OpenWhisk CLI](./openwhisk_cli.html)
- [從 iOS 應用程式使用 OpenWhisk](./openwhisk_mobile_sdk.html)
- [文章、範例及指導教學](https://github.com/openwhisk/openwhisk-external-resources)
- [Apache OpenWhisk FAQ](http://openwhisk.org/faq)
- [定價](https://console.ng.bluemix.net/openwhisk/learn/pricing)

## 程式設計模型
{: #openwhisk_start_programming}
- [系統詳細資料](./openwhisk_reference.html)
- [OpenWhisk 所提供服務的型錄](./openwhisk_catalog.html)
- [動作](./openwhisk_actions.html)
- [觸發程式及規則](./openwhisk_triggers_rules.html)
- [資訊來源](./openwhisk_feeds.html)
- [套件](./openwhisk_packages.html)
- [註釋](./openwhisk_annotations.html)
- [Web 動作](./openwhisk_webactions.html)
- [API 閘道](./openwhisk_apigateway.html)
- [實體名稱](./openwhisk_reference.html#openwhisk_entities)
- [動作語意](./openwhisk_reference.html#openwhisk_semantics)
- [限制](./openwhisk_reference.html#openwhisk_syslimits)

## {{site.data.keyword.openwhisk_short}} Hello World 範例
{: #openwhisk_start_hello_world}
若要開始使用 {{site.data.keyword.openwhisk_short}}，請嘗試下列 JavaScript 程式碼範例。

```javascript
/**
 * Hello world as an OpenWhisk action.
 */
function main(params) {
    var name = params.name || 'World';
    return {payload:  'Hello, ' + name + '!'};
}
```
{: codeblock}

若要使用此範例，請遵循下列步驟：

1. 將程式碼儲存至檔案。例如，*hello.js*。

2. 從 {{site.data.keyword.openwhisk_short}} CLI 指令行中，輸入下列指令來建立「動作」：
    ```
wsk action create hello hello.js
    ```
    {: pre}

3. 然後，輸入下列指令來呼叫「動作」。
    ```
wsk action invoke hello --blocking --result
    ```
    {: pre}  

    這個指令會輸出：
    ```json
    {
        "payload": "Hello, World!"
    }
    ```
    
    ```
wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    這個指令會輸出：
    ```json
    {
        "payload": "Hello, Fred!"
    }
    ```

您也可以使用 {{site.data.keyword.openwhisk_short}} 中的事件驅動功能，來呼叫此「動作」以回應事件。請遵循[警示服務範例](./openwhisk_packages.html#openwhisk_package_trigger)，將事件來源配置成每次產生定期事件時都呼叫「`hello` 動作」。

[OpenWhisk 指導教學及範例的完整清單可在這裡找到](https://github.com/openwhisk/openwhisk-external-resources#sample-applications)。除了範例之外，此儲存庫也包含文章、簡報、播客、視訊及其他 {{site.data.keyword.openwhisk_short}} 相關資源的鏈結。

## API 參考資料
{: #openwhisk_start_api notoc}
* [REST API 文件](./openwhisk_reference.html#openwhisk_ref_restapi)
* [REST API](https://console.{DomainName}/apidocs/98)

## 相關鏈結
{: #general notoc}
* [探索：{{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/)
* [IBM developerWorks 上的 {{site.data.keyword.openwhisk_short}}](https://developer.ibm.com/openwhisk/)
* [Apache {{site.data.keyword.openwhisk_short}} 專案網站](http://openwhisk.org)
