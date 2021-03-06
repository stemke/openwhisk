---

copyright:
  years: 2016, 2018
lastupdated: "2018-01-09"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 函數即服務比較
{: #openwhisk_faas_compared}

無伺服器架構並非所有計算問題的萬能措施，但確實可以解決一些問題。當無伺服器設計可以是好選擇時，有[許多使用案例](./openwhisk_use_cases.html)。比較下列架構：
{: shortdesc}

1. **函數即服務 (FaaS)** - 受管理 OpenWhisk。IBM 是唯一提供受管理 [OpenWhisk on{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/openwhisk) 的供應商。

2. 含「OpenWhisk 自行開發 (RYO)」的**基礎架構即服務 (IaaS)**。一般使用者可以從 Apache Incubation Project 下載 OpenWhisk ，並在 [{{site.data.keyword.Bluemix_notm}}IaaS](https://console.ng.bluemix.net/catalog/?category=devices) 或其他 [IaaS 雲端](https://en.wikipedia.org/wiki/Cloud_computing#Infrastructure_as_a_service_.28IaaS.29)中安裝並執行它。

3. **平台即服務 (PaaS)** - 受管理應用程式執行時期。建議範例是 {{site.data.keyword.Bluemix_notm}} CloudFoundry 實作所管理的 [Liberty for Java](https://console.ng.bluemix.net/catalog/starters/liberty-for-java) 執行時期。

4. **容器即服務 (CaaS)** - 受管理容器環境。最佳範例是 IBM 的 [Containers on{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/catalog/?category=containerImages)。

5. 含 Java EE 執行時期的**基礎架構即服務 (IaaS)**。最好的範例是來自 IBM 的 [WebSphere Application Server VM on{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/catalog/services/websphere-application-server)。

以下是在這些不同執行時期上開發及操作應用程式的**一般使用者視景**中，所提供每一個架構的優缺點摘要：


| 主題| (1) OpenWhisk FaaS| (2) OpenWhisk RYO| (3) PaaS| (4) CaaS| (5) IaaS+Java EE|
| --- | --- | --- | --- | --- | --- |
|	應用程式單位	|	單一函數（通常是 JavaScript、Swift 或 Docker 容器中的小型程式碼區塊）- 可以小於 1 KB，但可以更大。通常不超過幾 KB。|	與直欄 (1) 相同|	視所使用的執行時期而定。EAR 或 WAR 檔案，或是其他語言特定的應用程式軟體組，通常會相當大型，如果軟體組中有許多服務則為 KB 或甚至 MB，但也可以小到只有單一服務。|	Docker 容器是部署單位。|	具有含 EAR 或 WAR 檔案及其他相依關係的應用程式伺服器的 VM - 大小通常是 GB。|
|	資源覆蓋區	|	一般使用者不會購買或在意記憶體、CPU 或其他資源。雖然「動作」確實會有一些覆蓋區，但是使用者不需要擔心|	高。一般使用者必須先佈建 IaaS 環境，然後只在其上安裝及配置 OpenWhisk。|	小。一般使用者會購買記憶體及 CPU 來執行應用程式，但未執行的應用程式則不會進行任何動作|	中小型|	高。執行應用程式時，一般使用者必須購買磁碟儲存空間、記憶體、CPU 以及可能的其他元件。停止時，只會發生儲存空間成本|
|	安裝及設定|	不需要|	困難 - 全部由一般使用者完成|	不需要|	中 - 硬體、網路、OS、CaaSs 供應商所提供的容器管理工具、映像檔、連線功能及實例，由一般使用者進行|	困難 - 硬體、網路、OS、供應商所提供的起始 Java EE 安裝、其他配置、形成叢集、調整，由一般使用者進行|
|	佈建時間	|	毫秒	|	請參閱直欄 (4) 及 (5)|	分鐘	|	分鐘	|	小時	|
|	持續管理	|	無	|	困難	|	無	|	中	|	困難	|
|	彈性調整	|	一律都會根據負載立即且固有地調整每一個「動作」。不需要事先佈建 VM 或其他資源|	未提供 - 一般使用者必須提供 IaaS 上的運算容量，以及管理 VM 的調整。調整 VM 之後，OpenWhisk 會自動調整「動作」，但必須已事先佈建資源|	自動，但慢速調整。在增加負載期間，使用者可能要等待數分鐘，等到調整大小「動作」完成。自動調整需要仔細進行調整|	自動，但慢速調整。在增加負載期間，使用者可能要等待數分鐘，等到調整大小「動作」完成。自動調整需要仔細進行調整|	未提供	|
|	容量規劃	|	不需要。FaaS 會視需要自動提供最多的容量|	需要事先佈建足夠的容量，或編寫它的 Script|	需要進行一些容量規劃，但會提供一些自動增加容量|	需要進行一些容量規劃，但會提供一些自動增加容量|	需要靜態佈建足夠的容量來處理尖峰工作負載|
|	持續性連線及狀態|	限制 - 無法保持持續性連線，但容器快取除外。一般而言，狀態必須保留在外部資源中|	與直欄 (1) 相同|	受支援 - 可以保留開放式 Socket 或連線較長的時間、可以在呼叫之間將狀態儲存在記憶體中|	受支援 - 可以保留開放式 Socket 或連線較長的時間、可以在呼叫之間將狀態儲存在記憶體中|	受支援 - 可以保留開放式 Socket 或連線較長的時間、可以在呼叫之間將狀態儲存在記憶體中|
|	維護	|	無 - 整個堆疊由 IBM 管理。|	重要 - 視目標環境而定，使用者必須佈建硬體、網路、OS、儲存空間、DB、安裝及維護 OpenWhisk 等等。|	無 - 整個堆疊由供應商管理。|	重要 - 使用者必須建立及維護自訂映像檔、部署及管理容器、容器之間的連線等等。|	重要 - 使用者必須個別配置 VM、管理及調整 Java EE 伺服器。|
|	高可用性 (HA) 及災難回復 (DR)|	固有/無額外成本|	自行開發 (RYO)|	有額外成本|	可以自動重新啟動失敗的容器|	有額外成本，半自動。可以自動失效接手 VM|
|	安全	|	由供應商提供	|	自行開發 (RYO)|	混合使用 RYO 與由供應商提供的|	混合使用 RYO 與由供應商提供的|	自行開發 (RYO)|
|	開發人員速度	|	最高	|	最高	|	最高	|	普通|	慢速	|
|	資源使用率（仍然需要付費的閒置資源）|	資源絕不會閒置，因為只有在要求時才會進行呼叫。工作負載不存在時，不會發生成本或資源配置。|	因為此選項使用 IaaS 或 CaaS，所以會套用直欄 (4) 及 (5) 中的類似考量|	部分資源可以閒置，而自動調整有助於刪除閒置資源。許多執行中實例必須一直存在，且可能會使用於小於 50% 的容量。已停止的實例沒有任何成本|	與直欄 (3) 類似|	部分資源可以閒置，但不支援自動調整。某些執行中實例必須一直存在，且可能使用的容量少於 50% 的容量。已停止的實例會造成儲存體的成本|
|	期滿 |	提早期滿	|	提早期滿	|	提早期滿	|	中度期滿	|	非常成熟|
|	資源限制	|	[有些限制](./openwhisk_reference.html#openwhisk_syslimits)	|	取決於配置的資源|	否	|	否	|	否	|
|	罕用服務的延遲|	罕見要求一開始會經歷數秒回應時間，但後續要求會在毫秒範圍內完成。|	視情況而定	|	低|	低|	低 - 假設系統具有足夠的資源|
|	甜蜜點類型的應用程式|	事件處理、IoT、行動後端系統、微服務。絕對不適用於龐大應用程式。請參閱[使用案例](./openwhisk_use_cases.html)	|	與直欄 (1) 相同，但在使用者想要在非 IBM Cloud 或內部部署上執行時。|	需要長期間開啟連線的全年無休工作負載、有狀態服務的 Web 應用程式。可以用來執行微服務或龐大的應用程式|	適用於微服務應用程式。|	從內部部署移轉至雲端的傳統企業應用程式。適用於整合型應用程式|
|	費用精度及計費|	[每個區塊 100 毫秒](https://console.ng.bluemix.net/openwhisk/learn/pricing)	|	視實作而定，如果使用 IaaS 或 CaaS，則適用類似的考量，請參閱直欄 (4) 及 (5)|	對於資源組（CPU + 記憶體 + 部分磁碟空間），通常是每小時收費（極少的情況下是每分鐘）|	與直欄 (3) 類似|	與直欄 (3) 類似|
|	總擁有成本 (TCO)|	對於其優點，應用程式的執行成本量級可能會低於替代方案。因為資源會自動調整大小，所以不會發生過度佈建。|	對於雲端部署，這可能會比 OpenWhisk FaaS 更為昂貴，但對於內部部署，部署可能會比傳統架構還要便宜|	相對低 - 使用者不需要佈建或管理資源，可以著重於應用程式開發。相較於無伺服器，某層級的過度佈建|	中 - 使用者需要佈建及管理容器和應用程式，但相較於無伺服器及 PaaS，會看到某層級的過度佈建|	相對高 - 考量到從舊式應用程式移轉至雲端原生模型可能過於昂貴，這可為應用程式的可行且經濟實惠的選擇。|
