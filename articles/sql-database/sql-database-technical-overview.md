---
title: "什麼是 SQL Database？ SQL Database 簡介 | Microsoft Docs"
description: 'Get an introduction to SQL Database: technical details and capabilities of Microsoft''s relational database management system (RDBMS) in the cloud.'
keywords: "sql 簡介,sql 簡介,什麼是 sql database"
services: sql-database
documentationcenter: 
author: shontnew
manager: jhubbard
editor: cgronlun
ms.assetid: c561f600-a292-4e3b-b1d4-8ab89b81db48
ms.service: sql-database
ms.custom: overview
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 11/08/2016
ms.author: shkurhek
translationtype: Human Translation
ms.sourcegitcommit: 1c603d37735bbbfdfaaf4a191e2ad1ce6ff5b2b7
ms.openlocfilehash: 67f3e923680a9a2f399c0839d2ec11ef4615da00


---
# <a name="what-is-sql-database-introduction-to-sql-database"></a>什麼是 SQL Database？ SQL Database 簡介
SQL Database 是以領先市場的 Microsoft SQL Server 引擎為基礎，位於雲端並擁有許多關鍵任務功能的關聯式資料庫服務。 SQL Database 提供可預測的效能、無停機時間的延展性、商務持續性和資料保護等功能，且全都幾乎免管理。 如此一來，您便可以專注於快速開發應用程式及加快上市時間，而不是耗費在管理虛擬機器與基礎結構上。 由於 SQL Database 是以 [SQL Server](https://msdn.microsoft.com/library/bb545450.aspx) 引擎為基礎，因此可支援現有 SQL Server 工具、程式庫和 API，讓您可以更輕鬆地移動和延伸至雲端。

本文介紹與效能、延展性和管理能力相關的 SQL Database 核心概念和功能，並提供連結讓您進一步了解詳細資料。 如果您已經準備開始，可以立即[建立您的第一個 SQL Database](sql-database-get-started.md)，或者[建立彈性資料庫集區](sql-database-elastic-pool-create-portal.md)。 如果您想要進行更深入的探討，請觀賞這段 30 分鐘的影片。

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON326/player]
> 
> 

## <a name="adjust-performance-and-scale-without-downtime"></a>無須停機即可調整效能和規模
基本、標準和高階服務層皆提供 SQL Database。 每個服務層提供[不同層級的效能和功能](sql-database-service-tiers.md)，以支援輕量到重量級的資料庫工作負載。 您可以在小型資料庫中建置第一個應用程式，一個月只需少許花費。接著可依據應用程式在全世界受歡迎的程度，隨時以手動或程式設計方式[變更服務層](sql-database-scale-up.md)，且應用程式或客戶皆無須停機。

對於許多企業和應用程式而言，只要能夠建立資料庫，並依需求調高或調低單一資料庫的效能即可，尤其是當使用模式相當容易預測時更是如此。 但如果您有無法預測的使用模式，則管理成本和商務模式就會變得相當困難。

[彈性集區](sql-database-elastic-pool.md) 可解決此問題。 概念很簡單。 您可以將效能配置給集區，並針對集區的整體效能 (而非單一資料庫的效能) 付款。 您不需要調高或調低資料庫的效能。 集區中的資料庫 (即彈性資料庫 ) 可依據需求自動擴大或縮減規模。 彈性資料庫會取用集區的資源，但不會超過其限制，因此您的成本可在資料庫使用情形無法預測的狀況下維持可預測性。 此外，您還可以 [將資料庫移入/移出集區](sql-database-elastic-pool-manage-portal.md)，並將您的應用程式從數個資料庫擴充至數千個，而且全都在您可掌控的預算之內。 若要深入了解使用彈性集區的 SaaS 應用程式的設計模式，請參閱 [採用 Azure SQL Database 的多租用戶 SaaS 應用程式的設計模式](sql-database-design-patterns-multi-tenancy-saas-applications.md)。

因此，不論您要使用單一或彈性資料庫，都將不再受到限制。 您可以混合使用單一資料庫與彈性資料庫集區，並快速且輕易地變更單一資料庫和集區的服務層來適應您的情況。 此外，透過 Azure 功能強大而無遠弗屆的特性，您可以使用 SQL Database 混合和搭配其他 Azure 服務，滿足您獨特應用程式的設計需求、有效運用成本和資源，並且產生新的商機。

但是，您要如何比較資料庫和資料庫集區的相對效能？ 當您調高和調低效能時，要如何知道該在何處停止？ 答案就是內建的效能監視和警示工具，加上以適用於單一資料庫的資料庫交易單位 (DTU)，以及適用於彈性資料庫和資料庫集區的彈性 DTU (eDTU) 為根據的效能分級，讓您能夠根據目前或專案的效能需求快速評估相應增加或減少的影響。 如需詳細資訊，請參閱 [SQL Database 選項和效能：了解每個服務層中可用的項目](sql-database-service-tiers.md) 。

## <a name="keep-your-app-and-business-running"></a>讓您的應用程式和業務持續運作
Azure 領先業界的 99.99% 可用性服務等級協定 [(SLA)](http://azure.microsoft.com/support/legal/sla/)(由 Microsoft 管理之資料中心的全球網路提供支援)，可協助讓您的應用程式 24 小時全年無休地運作。 使用每個 SQL Database，您可以利用內建的安全性、容錯功能，以及可能需要另外設計、購買、建置和管理的資料保護功能。 即便如此，根據您的業務需求，您可能需要額外的保護層級，以確保在發生嚴重損壞、錯誤或其他干擾時，應用程式和業務可以快速復原。 使用 SQL Database 時，每個服務層都會提供一組完整的業務持續性功能和選項，讓您能夠用來啟動和執行，並持續維持該狀態。 您可以使用時間點還原將資料庫回復成先前的狀態，最久可至 35 天前。 此外，如果裝載資料庫的資料中心發生中斷情形，您可以從最新備份的異地備援複本還原資料庫，或者容錯移轉至其他區域中的資料庫複本。 您也可以使用複本進行升級，或將其重新放置到不同區域。

![SQL Database 異地複寫](./media/sql-database-technical-overview/azure_sqldb_map.png)

如需可用於不同服務層之其他商務持續性功能的詳細資料，請參閱 [商務持續性](sql-database-business-continuity.md) 。

## <a name="secure-your-data"></a>保護您的資料
SQL Server 的資料安全性向來是一項可靠的傳統，而 SQL Database 支援與其相同的多項功能，可限制存取權、保護資料，以及協助您監視活動。 如需可在 SQL Database 中使用之安全性選項的快速概要，請參閱 [保護您的 SQL Database](sql-database-security.md) 。 如需更完整的安全性功能檢視，請參閱 [SQL Server Database Engine 和 SQL Database 的資訊安全中心](https://msdn.microsoft.com/library/bb510589) 。 如需 Azure 平台安全性的相關資訊，也請造訪 [Azure 信任中心](https://azure.microsoft.com/support/trust-center/security/) 。

## <a name="next-steps"></a>後續步驟
您現已閱讀 SQL Database 簡介並回答了「什麼是 SQL Database？」問題，您就可以：

* 如需單一資料庫及彈性資料庫的成本和計算機，請參閱 [價格頁面](https://azure.microsoft.com/pricing/details/sql-database/) 。
* 深入了解 [彈性集區](sql-database-elastic-pool.md)。
* 從 [建立您的第一個資料庫](sql-database-get-started.md)開始。
* [使用 SSMS 連接及查詢](sql-database-connect-query-ssms.md)
* 以 C#、Java、Node.js、PHP、Python 或 Ruby 建置您的第一個應用程式： [SQL Database 和 SQL Server 的連接庫](sql-database-libraries.md)



<!--HONumber=Nov16_HO5-->


