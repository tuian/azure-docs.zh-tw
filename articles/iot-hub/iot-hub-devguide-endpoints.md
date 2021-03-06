---
title: "開發人員指南 - IoT 中樞端點 | Microsoft Docs"
description: "Azure IoT 中樞開發人員指南 - IoT 中樞端點的相關參考資訊"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 57ba52ae-19c6-43e4-bc6c-d8a5c2476e95
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: dobett
translationtype: Human Translation
ms.sourcegitcommit: c18a1b16cb561edabd69f17ecebedf686732ac34
ms.openlocfilehash: f2da46ba3fdf9386ad78ade4d2364a4a8990cd6d


---
# <a name="reference---iot-hub-endpoints"></a>參考 - IoT 中樞端點
## <a name="list-of-iot-hub-endpoints"></a>IoT 中樞端點清單
Azure IoT 中樞是一項多租用戶服務，可將其功能公開給各種動作項目。 下圖顯示 IoT 中樞公開的各種端點。

![IoT 中樞端點][img-endpoints]

以下是端點的說明︰

* **資源提供者**。 IoT 中樞資源提供者會公開 [Azure Resource Manager][lnk-arm] 介面，可讓 Azure 訂用帳戶擁有者建立和刪除 IoT 中樞，以及更新 IoT 中樞屬性。 IoT 中樞屬性用來管理[中樞層級的安全性原則][lnk-accesscontrol] (相對於裝置層級的存取控制) 和雲端到裝置與裝置到雲端傳訊的功能選項。 IoT 中樞資源提供者也可讓您[匯出裝置身分識別][lnk-importexport]。
* **裝置身分識別管理**。 每個 IoT 中樞都會公開一組用來管理裝置身分識別的 HTTP REST 端點 (建立、擷取、更新和刪除)。 [裝置身分識別][lnk-device-identities]用於裝置驗證和存取控制。
* **裝置對應項管理**。 每個 IoT 中樞會公開一組服務面向的 HTTP REST 端點，以查詢和更新[裝置對應項][lnk-twins] (更新標籤和屬性)。
* **作業管理**。 每個 IoT 中樞會公開一組服務面向的 HTTP REST 端點，以查詢和管理[作業][lnk-jobs]。
* **裝置端點**。 針對身分識別登錄中所佈建的各個裝置，IoT 中樞會公開裝置可用來傳送並接收訊息的一組端點：
  
  * 傳送裝置到雲端的訊息。 使用這個端點[傳送裝置到雲端的訊息][lnk-d2c]。
  * 接收雲端到裝置的訊息。 使用此端點來接收目標[雲端到裝置訊息][lnk-c2d]的裝置。
  * *起始檔案上傳*。 裝置會使用這個端點從 IoT 中樞接收 Azure 儲存體 SAS URI，以[上傳檔案][lnk-upload]。
  * *擷取和更新裝置對應項的屬性*。 裝置使用此端點來存取其[裝置對應項][lnk-twins]的屬性。
  * *接收直接方法要求*。 裝置使用此端點來接聽[直接方法][lnk-methods]的要求。
    
    公開這些端點時，是使用 [MQTT v3.1.1][lnk-mqtt]、HTTP 1.1 及 [AMQP 1.0][lnk-amqp] 通訊協定來公開。 請注意，AMQP 也可透過連接埠 443 上的 [WebSockets][lnk-websockets] 來取得。
    
    裝置對應項端點和方法端點只能在使用 [MQTT v3.1.1][lnk-mqtt] 時取得。
* **服務端點**。 各個 IoT 中樞會公開您的應用程式後端可用來與您的裝置通訊的一組端點。 這些端點目前只會使用 [AMQP][lnk-amqp] 通訊協定來公開，但透過 HTTP 1.1 公開的方法叫用端點除外。
  
  * *接收裝置到雲端的訊息*。 此端點與 [Azure 事件中樞][lnk-event-hubs]相容。 後端服務可用它來讀取由您的裝置所傳送的所有[裝置到雲端訊息][lnk-d2c]。
  * *傳送雲端到裝置的訊息及接收傳遞通知*。 這些端點可讓您的應用程式後端傳送可靠的[雲端到裝置訊息][lnk-c2d]，以及接收相對應的傳遞或到期通知。
  * *接收檔案通知*。 此訊息的端點可讓您接收您的裝置已成功上傳檔案的通知。 
  * *直接方法叫用*。 此端點可讓後端服務在裝置上叫用[直接方法][lnk-methods]。

[Azure IoT SDK][lnk-sdks] 一文說明您可用來存取這些端點的各種方式。

最後請務必注意，所有的 IoT 中樞端點都使用 [TLS][lnk-tls] 通訊協定，且絕不會在未加密/不安全的通道上公開任何端點。

## <a name="field-gateways"></a>現場閘道器
在 IoT 解決方案中， *現場閘道*位於裝置和 IoT 中樞端點之間。 它通常位於接近您的裝置的位置。 您的裝置會使用裝置所支援的通訊協定，直接與現場閘道器通訊。 現場閘道會使用 IoT 中樞所支援的通訊協定來連線到 IoT 中樞端點。 現場閘道可以是高度特殊化硬體或低功率電腦，其執行完成閘道所想要之端對端案例的軟體。

您可以使用 [Azure IoT 閘道 SDK][lnk-gateway-sdk] 來實作現場閘道。 此 SDK 提供特定功能，例如可以對從多個裝置到相同 IoT 中樞連接的通訊進行多工處理。

## <a name="next-steps"></a>後續步驟
此 IoT 中樞開發人員指南中的其他參考主題包括︰

* [裝置對應項和作業的 IoT 中樞查詢語言][lnk-devguide-query]
* [配額和節流][lnk-devguide-quotas]
* [IoT 中樞的 MQTT 支援][lnk-devguide-mqtt]

[lnk-gateway-sdk]: https://github.com/Azure/azure-iot-gateway-sdk

[img-endpoints]: ./media/iot-hub-devguide-endpoints/endpoints.png
[lnk-amqp]: https://www.amqp.org/
[lnk-mqtt]: http://mqtt.org/
[lnk-websockets]: https://tools.ietf.org/html/rfc6455
[lnk-arm]: ../azure-resource-manager/resource-group-overview.md
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/

[lnk-tls]: https://tools.ietf.org/html/rfc5246


[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-accesscontrol]: iot-hub-devguide-security.md#access-control-and-permissions
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-device-identities]: iot-hub-devguide-identity-registry.md
[lnk-upload]: iot-hub-devguide-file-upload.md
[lnk-c2d]: iot-hub-devguide-messaging.md#cloud-to-device-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md

[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md



<!--HONumber=Nov16_HO5-->


