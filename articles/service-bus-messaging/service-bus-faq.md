---
title: 服務匯流排常見問題集 | Microsoft Docs
description: 回答一些有關 Azure 服務匯流排的常見問題。
services: service-bus
documentationcenter: na
author: sethmanheim
manager: timlt
editor: ''

ms.service: service-bus
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/04/2016
ms.author: sethm;juconway

---
# <a name="service-bus-faq"></a>服務匯流排常見問題集
本文提供 Microsoft Azure 服務匯流排的一些常見問題解答。 您也可以造訪 [Azure 支援常見問題集](http://go.microsoft.com/fwlink/?LinkID=185083) ，以取得一般的 Azure 價格和支援資訊。 本文包含下列主題：

* [關於 Azure 服務匯流排訊息的一般問題](#general-questions-about-azure-service-bus-messaging)
* [服務匯流排最佳做法](#service-bus-best-practices)
* [服務匯流排價格](#service-bus-pricing)
* [服務匯流排配額](#service-bus-quotas)
* [訂用帳戶和命名空間管理](#subscription-and-namespace-management)
* [疑難排解](#service-bus-troubleshooting)

## <a name="general-questions-about-azure-service-bus-messaging"></a>關於 Azure 服務匯流排訊息的一般問題
### <a name="what-is-azure-service-bus-messaging?"></a>什麼是 Azure 服務匯流排訊息？
[Azure 服務匯流排訊息](service-bus-messaging-overview.md)是非同步的訊息雲端平台，可讓您在彼此分離的系統之間傳送資料。 Microsoft 以服務的形式提供此功能，這表示您不需要裝載任何自有硬體就能使用。

### <a name="what-is-a-service-bus-namespace?"></a>什麼是服務匯流排命名空間？
[命名空間](../service-bus/service-bus-create-namespace-portal.md)提供範圍容器，可在應用程式內定址服務匯流排資源。 必須建立命名空間才能使用服務匯流排，而且這也是開始使用的第一個步驟。

### <a name="what-is-an-azure-service-bus-queue?"></a>什麼是 Azure 服務匯流排佇列？
[服務匯流排佇列](service-bus-queues-topics-subscriptions.md)是訊息儲存所在的實體。 如果您有多個應用程式，或多個需要彼此通訊的分散式應用程式部分，佇列會特別有用。 佇列和配送中心的類似之處在於，兩者都會接收多個產品 (訊息)，再從該處送出。

### <a name="what-are-azure-service-bus-topics-and-subscriptions?"></a>什麼是 Azure 服務匯流排主題和訂用帳戶？
主題可視覺化為佇列，而且在使用多個訂用帳戶時，主題會變成更豐富的訊息模型；基本上是一對多的通訊工具。 此發佈/訂閱模型 (或「pub/sub」) 可讓應用程式將訊息傳送至具有多個訂用帳戶的主題，以便讓多個應用程式接收該訊息。

### <a name="what-is-the-azure-service-bus-relay-service?"></a>什麼是 Azure 服務匯流排轉送服務？
[轉送服務](../service-bus-relay/service-bus-relay-overview.md)能夠在幕後裝載 WCF 服務，以及從任何地方存取 WCF 服務。 換句話說，此服務可讓混合式應用程式在 Azure 資料中心和內部部署企業環境中執行。

### <a name="what-is-a-partitioned-entity?"></a>什麼是分割的實體？
傳統的佇列或主題由單一訊息代理程式處理並儲存在一個訊息存放區中。 [分割的佇列或主題](service-bus-partitioning.md)會由多個訊息代理程式處理，並儲存在多個訊息存放區。 這表示分割佇列或主題的整體輸送量不會再受到單一訊息代理程式或訊息存放區的效能所限制。 此外，即使訊息存放區暫時中斷也不會讓分割的佇列或主題無法使用。

請注意，使用分割實體時無法確保順序。 若分割無法使用，您仍可從其他分割傳送及接收訊息。

## <a name="service-bus-best-practices"></a>服務匯流排最佳做法
### <a name="what-are-some-azure-service-bus-best-practices?"></a>Azure 服務匯流排的最佳做法有哪些？
* [使用服務匯流排代理傳訊的效能改進最佳作法][使用服務匯流排代理傳訊的效能改進最佳作法] – 這篇文章說明如何在交換代理訊息時將效能最佳化。
* [將應用程式與服務匯流排中斷和災難隔絕的最佳做法][將應用程式與服務匯流排中斷和災難隔絕的最佳做法] – 這篇文章討論如何盡可能避免轉送端點、佇列和主題以及主動和被動複寫因資料中心中斷而受影響。

### <a name="what-should-i-know-before-creating-messaging-entities?"></a>建立訊息實體前的須知事項為何？
佇列和主題的下列屬性是不可變的。 在佈建實體時請將這一點納入考量，因為若要修改屬性，就必須建立新的替代實體。

* 大小
* 分割
* 工作階段
* 重複偵測
* 快速實體

## <a name="service-bus-pricing"></a>服務匯流排價格
本節提供服務匯流排價格結構的一些常見問題解答。 您也可以造訪 [Azure 支援常見問題集](http://go.microsoft.com/fwlink/?LinkID=185083) ，以取得一般 Microsoft Azure 價格資訊。 如需服務匯流排價格的完整資訊，請參閱 [服務匯流排價格詳細資料](https://azure.microsoft.com/pricing/details/service-bus/)。

### <a name="how-do-you-charge-for-service-bus?"></a>服務匯流排的收費方式為何？
如需服務匯流排價格的完整資訊，請參閱[服務匯流排價格詳細資料][價格概觀]。 除了註明的價格，您還需支付您的應用程式佈建所在資料中心外部的輸出相關資料傳輸費用。

### <a name="what-usage-of-service-bus-is-subject-to-data-transfer?-what-is-not?"></a>何種服務匯流排用法需支付資料傳輸費用？ 何種不需？
指定的 Azure 區域內的任何資料傳輸都是免費提供。 區域外部的資料傳輸需支付輸出費用，其費率為每 GB 0.15 美元 (從北美洲和歐洲地區) 和每 GB 0.20 美元 (從亞太地區)。 任何輸入資料傳輸都是免費提供。

### <a name="how-is-the-relay-hours-meter-calculated?"></a>如何計算轉送時數計量？
轉送時數的計費方式為在指定的計費期間內，每個服務匯流排轉送為「開放」狀態的累計時間量。 當已啟用轉送的 WCF 服務或「轉送接聽程式」第一次連接到指定的服務匯流排位址 (服務命名空間 URL) 時，轉送就會隱含具現化並於該位址開放。 只有在最後一個接聽程式中斷連接其位址時，才會關閉轉送。 因此，為了方便計費，從第一個轉送接聽程式連接轉送的服務匯流排位址，到最後一個轉送接聽程式中斷連接的這段時間，該轉送會被視為「開放」。 換句話說，每當一或多個轉送接聽程式連接到轉送的服務匯流排位址時，該轉送就會被視為「開放」。

### <a name="what-if-i-have-more-than-one-listener-connected-to-a-given-relay?"></a>如果我有一個以上的接聽程式連接到指定的轉送，該怎麼辦？
在某些情況下，服務匯流排中的單一轉送可能有多個已連接的接聽程式。 這可能會發生於使用 netTCPRelay 或 HttpRelay WCF 繫結的負載平衡服務，或使用 netEventRelay WCF 繫結的廣播事件接聽程式。 至少有一個轉送接聽程式連接到服務匯流排中的轉送時，即會被視為「開放式」轉送。 將其他接聽程式加入至開放式轉送並不會變更該轉送的狀態，以便計費。 連接到轉送的轉送傳送者 (叫用或傳送訊息至轉送的用戶端) 數目也不會影響轉送時數的計算。

### <a name="how-is-the-messages-meter-calculated-for-relays?"></a>如何針對轉送計算訊息計量？
一般而言，對代理實體 (佇列、主題和訂用帳戶) 使用上述相同方法的轉送會計算計費訊息。 但是，請注意以下幾個差異：

將訊息傳送至服務匯流排轉送會被視為「完全直達」傳送至接收訊息的轉送接聽程式，而不是傳送至服務匯流排轉送並接著傳遞至轉送接聽程式。 因此，對於轉送接聽程式的要求-回覆模式服務叫用 (最多 64 KB) 將會產生兩則計費訊息︰一則是要求的計費訊息，一則是回應的計費訊息 (假設回應也是 \< = 64 KB)。 這與使用佇列在用戶端與服務之間居中協調不同。 在後面的情況中，相同的要求-回覆模式需要將要求傳送至佇列，接著清除佇列/從佇列傳遞至服務，然後接著將回應傳送至另一個佇列，以及清除佇列/從該佇列傳遞至用戶端。 始終使用相同的 (\< = 64 KB) 大小假設，居中協調的佇列模式會因此產生四則計費訊息，這是使用轉送實作相同模式所需計費數目的兩倍。 當然，使用佇列來達成此模式有許多優點，例如，持久性和負載調節。 這些優點可合理解釋額外的費用。

使用 netTCPRelay WCF 繫結開啟的轉送不會將訊息視為個別的訊息，而會視為通過系統的資料流。 換句話說，只有傳送者和接聽程式能夠看見使用此繫結傳送/接收之個別訊息的框架。 因此，對於使用 netTCPRelay 繫結的轉送，所有資料都會被視為資料流，以便計算計費訊息。 在此情況下，服務匯流排會計算每隔 5 分鐘透過每個個別轉送傳送或接收的資料總量並將該總量除以 64 KB，以便判斷該期間內有問題之轉送的計費訊息數目。

### <a name="does-service-bus-charge-for-storage?"></a>服務匯流排是否會收取儲存體費用？
不會，服務匯流排不會收取儲存體費用。 不過，有配額會限制每個佇列/主題可保存的資料數量上限。 請參閱下一個常見問題。

## <a name="service-bus-quotas"></a>服務匯流排配額
如需服務匯流排的限制和配額清單，請參閱[配額概觀][配額概觀]。

### <a name="does-service-bus-have-any-usage-quotas?"></a>服務匯流排是否有任何使用量配額？
根據預設，對於所有雲端服務，Microsoft 會設定針對所有客戶的訂用帳戶計算的彙總每月使用量配額。 因為我們了解您的需求可能超過這些限制，請隨時連絡客戶服務部門，讓我們能夠了解您的需求並適當地調整這些限制。 服務匯流排的彙總使用量配額如下：

* 50 億則訊息
* 2 百萬個轉送小時

雖然我們有權停用在指定的月份內超出其使用量配額的客戶帳戶，但我們將提供電子郵件通知並且在採取任何動作之前多次嘗試連絡客戶。 超出這些配額的客戶仍需負責支付超出配額的費用。

如同 Azure 上的其他服務，服務匯流排會強制執行一組特定的配額，以確保公平的資源使用量。 以下是此服務會強制執行的使用量配額：

#### <a name="queue/topic-size"></a>佇列/主題大小
您會在建立佇列或主題時指定佇列或主題大小上限。 此配額的值可以是 1、2、3、4 或 5 GB。 如果達到大小上限，其他內送訊息將會遭到拒絕，而且呼叫端程式碼將會收到例外狀況。

#### <a name="naming-restrictions"></a>命名限制
服務匯流排命名空間的名稱長度只能介於 6 到 50 個字元之間。 對於每個佇列、主題或訂用帳戶，字元數限制為 1 到 50 個字元之間。

#### <a name="number-of-concurrent-connections"></a>並行連線數目
佇列/主題/訂用帳戶 -佇列/主題/訂用帳戶上並行 TCP 連線數目的限制為 100。 如果達到這個配額，其他連接的後續要求將會遭到拒絕，而且呼叫端程式碼將會收到例外狀況。 對於每個訊息工廠而言，如果該訊息工廠所建立的任何用戶端有作用中的作業擱置，或在少於 60 秒之前完成作業，則服務匯流排會維持一個 TCP 連線。 REST 作業不會計入並行 TCP 連線內。

#### <a name="number-of-concurrent-listeners-on-a-relay"></a>轉送上的並行接聽程式數目
轉送上並行的 **netTcpRelay** 和 **netHttpRelay** 接聽程式數目限制為 25 (1 適用於 **NetOneway** 轉送)。

#### <a name="number-of-concurrent-relay-listeners-per-namespace"></a>每個命名空間的並行轉送接聽程式數目
服務匯流排會強制執行每個服務命名空間 2000 個並行轉送接聽程式的限制。 如果達到這個配額，開啟其他轉送接聽程式的後續要求將會遭到拒絕，而且呼叫端程式碼將會收到例外狀況。

#### <a name="number-of-topics/queues-per-service-namespace"></a>每個服務命名空間的主題/佇列數目
服務命名空間上的主題/佇列 (持久型儲存體支援的實體) 數目上限為 10,000。 如果達到此配額，後續要求在服務命名空間上建立新主題/佇列將會遭到拒絕。 在此情況下，視建立嘗試是透過入口網站或在用戶端程式碼中完成而定，Azure 傳統入口網站將會顯示一則錯誤訊息，或呼叫端程式碼將會收到例外狀況。

### <a name="message-size-quotas"></a>訊息大小配額
#### <a name="queue/topic/subscription"></a>佇列/主題/訂用帳戶
**訊息大小** – 每則訊息的大小總計限制為 256KB，包含訊息標頭。

**訊息標頭大小** – 每個訊息標頭的限制為 64 KB。

**NetOneway 和 NetEvent 轉送** - 每則訊息的大小總計限制為 64KB，包含訊息標頭。

**Http 和 NetTcp 轉送** – 服務匯流排不會強制執行這些訊息大小的上限。

超出這些大小配額的訊息將會遭到拒絕，而且呼叫端程式碼將會收到例外狀況。

**每個主題的訂用帳戶數目** – 每個主題的訂用帳戶數目上限為 2,000。 如果達到此配額，將會拒絕建立主題的其他訂用帳戶的後續要求。 在此情況下，視建立嘗試是透過入口網站或在用戶端程式碼中完成而定，Azure 傳統入口網站將會顯示一則錯誤訊息，或呼叫端程式碼將會收到例外狀況。

**每個主題的 SQL 篩選器數目** – 每個主題的 SQL 篩選器數目上限為 2,000。 如果達到這個配額，則在主題上建立其他篩選器的後續要求都會遭到拒絕，而且呼叫端程式碼將會收到例外狀況。

**每個主題的相互關聯篩選器數目** – 每個主題的相互關聯篩選器數目上限為 100,000。 如果達到這個配額，則在主題上建立其他篩選器的後續要求都會遭到拒絕，而且呼叫端程式碼將會收到例外狀況。

## <a name="subscription-and-namespace-management"></a>訂用帳戶和命名空間管理
### <a name="how-do-i-migrate-a-namespace-to-another-azure-subscription?"></a>如何將命名空間移轉到另一個 Azure 訂用帳戶？
您可以使用 PowerShell 命令 (可在[這裡][這裡]的文章中找到) 將命名空間從某個 Azure 訂用帳戶移到另一個 Azure 訂用帳戶。 若要執行此作業，命名空間必須已是作用中。 此外，執行命令的使用者也必須是來源和目標訂用帳戶的系統管理員。

## <a name="service-bus-troubleshooting"></a>服務匯流排疑難排解
[例外狀況概觀][例外狀況概觀]

### <a name="what-are-some-of-the-exceptions-generated-by-azure-service-bus-messaging-apis-and-their-suggested-actions?"></a>Azure 服務匯流排訊息 API 所產生的例外狀況有哪些，其建議的動作為何？
訊息 API 可能產生的例外狀況分成下列幾個類別︰

* 使用者編碼錯誤
* 設定/組態錯誤
* 暫時性例外狀況
* 其他例外狀況

[服務匯流排傳訊例外狀況][例外狀況概觀]一文會說明部分例外狀況和建議的動作。

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature?"></a>什麼是共用存取簽章，何種語言可支援產生簽章？
共用存取簽章是以 SHA-256 安全雜湊或 URI 為基礎的驗證機制。 如需如何在 Node、PHP、Java 和 C\# 中產生自有簽章的相關資訊，請參閱[共用存取簽章][共用存取簽章]一文。

## <a name="next-steps"></a>後續步驟
若要深入了解服務匯流排訊息，請參閱下列主題。

* [Azure 服務匯流排進階傳訊簡介 (部落格文章)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Azure 服務匯流排進階傳訊簡介 (Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [服務匯流排訊息概觀](service-bus-messaging-overview.md)
* [Azure 服務匯流排架構概觀](../service-bus/service-bus-fundamentals-hybrid-solutions.md)
* [開始使用服務匯流排佇列](service-bus-dotnet-get-started-with-queues.md)

[使用服務匯流排代理傳訊的效能改進最佳作法]: service-bus-performance-improvements.md
[將應用程式與服務匯流排中斷和災難隔絕的最佳做法]: service-bus-outages-disasters.md
[價格概觀]: https://azure.microsoft.com/pricing/details/service-bus/
[配額概觀]: service-bus-quotas.md
[這裡]: service-bus-powershell-how-to-provision.md#migrate-a-namespace-to-another-azure-subscription
[例外狀況概觀]: service-bus-messaging-exceptions.md
[共用存取簽章]: service-bus-sas-overview.md



<!--HONumber=Oct16_HO2-->


