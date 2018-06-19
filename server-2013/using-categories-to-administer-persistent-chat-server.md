﻿---
title: 使用類別以管理常設聊天室伺服器
TOCTitle: 使用類別以管理常設聊天室伺服器
ms:assetid: dfcb3ad1-da90-467e-b08c-f4e68673b7b5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398988(v=OCS.15)
ms:contentKeyID: 49292565
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用類別以管理常設聊天室伺服器

 

_**上次修改主題的時間：** 2013-10-01_

常設聊天室伺服器 部署可以同時裝載許多 常設聊天室 聊天室。聊天室在伺服器上會組織成一組類別。每個聊天室各屬於一項類別，而且會繼承該類別中的一些設定。這樣的組織會建立一個有用的結構，可用於根據其商業用途來識別交談，並促進委派管理功能和簡化管理。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然執行 常設聊天室 ( Lync 用戶端) 的電腦中，提供使用者許多聊天室的管理功能，但 常設聊天室 管理員 (身為 <strong>cspersistentchatadministrator</strong> 角色) 必須使用 Lync Server 控制台或 Windows PowerShell Cmdlet 來建立或管理類別。</td>
</tr>
</tbody>
</table>


常設聊天室 管理員可使用 Lync Server 控制台或 Windows PowerShell Cmdlet 建立和管理類別，以及設計組織中的使用者存取聊天室的方式。

能夠管理一或多個聊天室的 常設聊天室 聊天室管理員，可以使用 Lync 用戶端啟動聊天室管理 Web 應用程式，建立和管理聊天室 (或者使用者可建立自訂的解決方案以及要叫用的工作流程)。 常設聊天室 管理員也可以使用 Lync Server 控制台或 Windows PowerShell Cmdlet 來建立和管理聊天室。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>常設聊天室聊天室的名稱不可與常設聊天室類別相同。</td>
</tr>
</tbody>
</table>


聊天室理員可以變更所有聊天室內容，變更聊天室類別除外。不可限制其無法進行下列動作：

  - 停用聊天室

  - 變更聊天室名稱

  - 變更聊天室說明

  - 變更聊天室類型 (視聽形式或是一般形式)

  - 變更聊天室隱私權 (比較開放式、封閉式及祕密)

  - 新增或移除成員

  - 新增或移除聊天室管理員

  - 新增或移除增益集

  - 變更設定，例如邀請 (根據該類別所允許的設定)

## 委派管理

正確地使用類別，能讓建立和管理 常設聊天室 聊天室更加容易。 常設聊天室 管理員可以為每個類別定義 **AllowedMembers** 與 **Creators**，以及定義會套用至以該類別建立之所有聊天室的預設聊天室設定與行為。 常設聊天室 管理員可透過使用 Lync Server 控制台或 Windows PowerShell Cmdlet 來建立和管理類別。

允許以該類別建立聊天室的個人與群組，只有識別為該類別 Creators 的使用者、組織單位 (OU) 及使用者群組。建立類別之後，可以從類別的 **AllowedMembers** 清單中選擇使用者、OU 及使用者群組，做為管理和參與聊天室的聊天室管理員與成員。

以類別建立的聊天室會依循該類別強制執行的原則和設定 (例如，誰具有聊天室的成員資格、誰可以管理聊天室、是否允許上傳檔案、是否要傳送邀請等)。
