﻿---
title: Lync Server 2013：設定類別
TOCTitle: 設定類別
ms:assetid: 4547f514-f0c0-404d-890f-092ddeeac852
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204859(v=OCS.15)
ms:contentKeyID: 49290770
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定類別

 

_**上次修改主題的時間：** 2012-10-06_

在 Lync Server 2013 控制台中，您可以使用 **\[ 常設聊天室\]** 頁面的 **\[類別\]** 區段來設定類別。 常設聊天室聊天室類別是組織聊天室的邏輯結構。類別會定義一組預設的存取控制清單 (ACLs)，用於控制可建立或加入聊天室的使用者及使用者群組。您可以利用類別在組織內不同的子部門之間強制執行道德管束。

聊天室類別可包含聊天室，但不可包含其他類別。每個類別分別說明其內容與中繼資料，例如*Name*與*Description*。此外，您可以設定類別中的內容以控制所屬聊天室的行為，例如聊天室是否允許*Invitations*或*File Uploads*，或包含*Chat History*。

## 設定聊天室的類別

1.  使用指派給 CsPersistentChatAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任一部電腦。

2.  從 **\[開始\]** 功能表中，選取 Lync Server 控制台或開啟瀏覽器視窗，然後輸入 Admin URL。如需各種 Lync Server 控制台啟動方法的詳細資訊，請參閱＜ [開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)＞。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您也可以使用 Windows PowerShell Cmdlet。如需詳細資訊，請參閱部署移轉文件 <a href="configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md">使用 Windows PowerShell Cmdlet 設定常設聊天室伺服器</a>＞。</td>
    </tr>
    </tbody>
    </table>


3.  在左導覽列中，按一下 **\[ 常設聊天室\]** ，然後按一下 **\[類別\]** 。
    
    如有多個 Persistent Chat Server 集區部署，則從下拉式清單中選取適當的集區。

4.  在 **\[類別\]** 頁面上，按一下 **\[新增\]** 或 **\[編輯\]** 。

5.  在 **\[選取服務\]** 中，選取對應至需要建立類別的 Persistent Chat Server 集區的服務。此服務是 常設聊天室 (用戶端) 用來找出類別所屬集區的 常設聊天室伺服器 集區。類別只能屬於一個 Persistent Chat Server 集區，不得移到另一個集區，或與另一個集區共用。

6.  在 **\[新類別\]** 中，執行下列作業：
    
    1.  在 **\[名稱\]** 中，指定新聊天室類別的名稱。
    
    2.  在 **\[描述\]** 中，提供聊天室類別的詳細描述 (例如，Contoso 的聊天室類別)。
    
    3.  如果要控制是否可以為屬於此類別的聊天室啟用邀請，請選取或清除 **\[啟用邀請\]** 核取方塊。如果選取，此類別中的聊天室即可開啟或關閉邀請；如果清除，則不允許此類別中的聊天室有邀請。如果聊天室開啟邀請，當新成員加入聊天室時，該成員會在其 常設聊天室用戶端收到新聊天室的通知。
    
    4.  如果要控制屬於此類別的聊天室中的檔案上傳，請選取或清除 **\[啟用檔案上傳\]** 核取方塊。如果選取，此類別的聊天室就可以啟用或停用檔案上傳；如果清除，則不允許此類別的聊天室有檔案上傳。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>這個設定在伺服器上是強制執行的，因為自訂應用程式或是使用 Office Communications Server 2007 R2群組聊天伺服器或 Lync Server 2010 群組聊天的舊版 群組聊天用戶端可以在聊天室中張貼檔案。由於 Lync 2013 用戶端沒有檔案上傳/下載功能，因此如果是單純的 Lync 2013 部署或 Lync 2013 用戶端，就不可能在 常設聊天室伺服器 聊天室中張貼檔案。</td>
        </tr>
        </tbody>
        </table>
    
    5.  如果要控制交談記錄，請選取或清除 **\[啟用交談記錄\]** 核取方塊。如果選取，聊天內容會持續存在；如果清除，聊天訊息就不會存在。如果啟用規範，將會依規範儲存聊天內容，但是使用者無法存取較早的訊息。這個選項可用於指派給不需要保存交談記錄的即時、臨時共同作業的聊天室。

7.  在 **\[編輯類別\]** 中，執行下列作業：
    
      - 在 **\[成員資格\]** 的 **\[允許的成員\]** 區段中，新增或移除獲得允許成為屬於此類別聊天室成員的使用者及其他 Active Directory 網域服務 主體 (使用者、通訊群組、組織單位等等)。類別所允許的主體可以搜尋該類別中的聊天室 (除非該聊天室為隱藏，則只有其成員可以在目錄中搜尋它)。
    
      - 在 **\[成員資格\]** 的 **\[拒絕的成員\]** 區段中，新增或移除與被聊天室拒絕的成員有關聯的使用者及其他 Active Directory 主體。
    
      - 在 **\[成員資格\]** 的 **\[建立者\]** 區段中，新增或移除與類別建立者有關聯的使用者及其他 Active Directory 主體。建立者是有權建立聊天室及指派聊天室管理員和成員的使用者。

8.  按一下 \[認可\] 。
