---
title: "在 Azure App Service 中建立交易夥伴協議 | Microsoft Docs"
description: "建立交易夥伴協議"
services: logic-apps
documentationcenter: .net,nodejs,java
author: rajram
manager: erikre
editor: 
ms.assetid: 319e46fa-fd81-4730-a742-768bf1676972
ms.service: logic-apps
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/23/2016
ms.author: rajram
translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: e41ac0e91bd66fbc7df08b4397e78377021fcbca


---
# <a name="creating-a-trading-partner-agreement"></a>建立交易夥伴協議
[!INCLUDE [app-service-logic-version-message](../../includes/app-service-logic-version-message.md)]

交易夥伴是指涉及 B2B (企業對企業) 通訊的實體。 當兩個夥伴建立關係時，這稱為協議 。 定義的協議會以這兩個夥伴想要達成的通訊為基礎，且是特定的通訊協定或傳輸。 Azure App Service 支援的各種 B2B 通訊協定和傳輸包括：

* AS2 (Applicability Statement 2)
* EDIFACT (聯合國/行政、商業、傳輸的電子資料交換 (UN/EDIFACT))
* X12 (ASC X12)

### <a name="biztalk-api-apps-that-support-b2b-scenarios"></a>支援 B2B 案例的 BizTalk API 應用程式
下列 API 應用程式會啟用這些使用 Azure 入口網站中豐富且直覺化體驗的功能：

## <a name="biztalk-trading-partner-management-tpm"></a>BizTalk 交易夥伴管理 (TPM)
* 建立和管理夥伴、設定檔與身分識別
* 儲存和管理 EDI 結構描述
* 儲存和管理憑證 (用於 AS2 通訊協定)
* 建立和管理 AS2 協議
* 建立和管理 EDIFACT 協議 (包含傳送端上的批次處理)
* 建立和管理 X12 協議 (包含傳送端上的批次處理)

![][1]

## <a name="as2-connector"></a>AS2 連接器
* 執行如相關 TPM API 應用程式執行個體中所定義的 AS2 協議
* 瀏覽 AS2 處理/追蹤資訊以進行疑難排解

## <a name="biztalk-edifact"></a>BizTalk EDIFACT
* 執行如相關 TPM API 應用程式執行個體中所定義的 EDIFACT 協議
* 瀏覽 EDIFACT 處理/追蹤資訊以進行疑難排解
* 提供如相關 TPM API 應用程式執行個體中 EDIFACT 協議所定義的批次狀態管理 (「開始」和「停止」)

## <a name="biztalk-x12"></a>BizTalk X12
* 執行如相關 TPM API 應用程式執行個體中所定義的 X12 協議 
* 瀏覽 X12 處理/追蹤資訊以進行疑難排解
* 提供如相關 TPM API 應用程式執行個體中 X12 協議所定義的批次狀態管理 (「開始」和「停止」)

如前所述，AS2、x12 和 EDIFACT API 應用程式都需要 TPM API 應用程式，才能如預期般運作。

## <a name="getting-started"></a>開始使用
建立交易夥伴協議：

1. 建立 **BizTalk 交易夥伴管理** 連接器的執行個體。 這需要一個空白的 SQL Database 才能運作。 開始之前，請確定具有並可供使用的空白資料庫。
2. 視協議的需要上傳結構描述和憑證。 您可透過瀏覽已建立的 TPM 執行個體，並逐步執行 [結構描述] 和/或 [憑證] 部分，來完成上述動作
3. 瀏覽至已建立的 TPM 執行個體，並逐步執行 [夥伴]  部分
4. 視需要建立夥伴。 並適當地編輯設定檔，以及新增必要的身分識別
5. 現在使用 [協議]  部分來建立協議。 當您建立協議時，必須選取將會使用的通訊協定。 其餘的設定選項取決於您選取的通訊協定。

![][2]

![][3]

<!--Image references-->
[1]: ./media/app-service-logic-create-a-trading-partner-agreement/TPMResourceView.png
[2]: ./media/app-service-logic-create-a-trading-partner-agreement/ProtocolSelection.png
[3]: ./media/app-service-logic-create-a-trading-partner-agreement/X12AgreementCreation.png




<!--HONumber=Nov16_HO2-->


