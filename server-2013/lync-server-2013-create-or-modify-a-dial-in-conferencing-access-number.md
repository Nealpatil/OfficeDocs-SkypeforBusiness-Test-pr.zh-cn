﻿---
title: Lync Server 2013：创建或修改电话拨入式会议访问号码
TOCTitle: 创建或修改电话拨入式会议访问号码
ms:assetid: 06f55c28-57f8-4d4e-8313-9740846796d9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg398126(v=OCS.15)
ms:contentKeyID: 49311890
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中创建或修改电话拨入式会议访问号码

 

_**上一次修改主题：** 2012-09-17_

如果要创建或修改电话拨入式会议访问号码，请执行以下步骤。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398794.important(OCS.15).gif" title="important" alt="important" />重要提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>创建新的拨入访问号码前，必须在与新拨入访问号码关联的拨号计划中设置电话拨入式会议区域。多个拨号计划可使用同一区域。</td>
</tr>
</tbody>
</table>


## 创建或修改拨入访问号码

1.  使用分配给 CsUserAdministrator 或 CsAdministrator 角色的用户帐户，登录到内部部署中的任何计算机。

2.  打开浏览器窗口，然后输入管理 URL 以打开 Lync Server 控制面板。有关可以用于启动 Lync Server 控制面板的不同方法的详细信息，请参阅[打开 Lync Server 管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左侧导航栏中，单击“会议”，然后单击“拨入访问号码”。

4.  在“拨入访问号码”页上，执行下列操作之一：
    
      - 单击“新建”打开“新建拨入访问号码”。
    
      - 单击列表中的一个拨入访问号码，再单击“编辑”，然后单击“显示详细信息”。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>使用搜索字段搜索拨入访问号码列表中某一列的内容时，可能得不到预期结果。此时，可以按照列的关注度对列表进行排序，以识别要查看或更改的拨入访问号码。</td>
        </tr>
        </tbody>
        </table>


5.  在“显示号码”中，键入相应的电话号码，以便公用电话交换网 (PSTN) 电话用户可拨打此号码加入会议。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>该号码会显示在会议邀请和电话拨入式会议设置网页中。</td>
    </tr>
    </tbody>
    </table>


6.  在“显示名称”中，键入拨入访问号码的说明。此名称与 Lync 搜索结果中的拨入访问号码相关联。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>用户呼叫访问号码时，此名称会显示在客户端上。</td>
    </tr>
    </tbody>
    </table>


7.  在“线路 URI”中，使用 TEL URI 格式键入拨入访问号码的 E.164 号码，请在此号码前添加 + 符号，不要添加空格。例如：tel:+14255550200。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>同一线路 URI 不能由其他电话拨入式会议访问号码重复使用。</td>
    </tr>
    </tbody>
    </table>


8.  在“SIP URI”中，执行下列操作：
    
      - 在文本框中，为此电话拨入式会议访问号码键入唯一的 SIP URI。此 SIP URI 将显示在各种不同的位置，包括但不限于呼叫通知消息和早期版本的 Communicator 客户端。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>同一 SIP URI 不能由其他电话拨入式会议访问号码重复使用。创建访问号码之后，将不能修改 SIP URI。更改 SIP URI 的唯一方法是删除并重新创建访问号码。</td>
        </tr>
        </tbody>
        </table>
    
      - 在下拉列表框中，单击支持此拨入访问号码的 会议助理应用程序的域。

9.  在“池”中，单击运行支持此拨入访问号码的会议助理实例的池。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>创建访问号码后，如果需要更改池，必须使用 <strong>Move-CsApplicationEndpoint</strong> cmdlet 或删除并重新创建访问号码。</td>
    </tr>
    </tbody>
    </table>


10. 在“主要语言”中，单击针对此拨入访问号码播放提示时使用的语言。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>主要语言是会议助理应答呼叫时使用的语言。支持的语言显示在电话拨入式会议设置网页上的每个访问电话号码旁边。</td>
    </tr>
    </tbody>
    </table>


11. （可选）在“辅助语言（最多 4 个）”中，单击“添加”，选择一个或多个要为此拨入访问号码的呼叫者提供支持的其他语言，然后单击“确定”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>最多可以为每个拨入访问号码选择四种辅助语言。用户通过电话拨入加入会议时，在输入会议 ID 之前可以选择一种辅助语言。</td>
    </tr>
    </tbody>
    </table>


12. 要为拨入访问号码添加区域，请在“关联区域”下单击“添加”，再单击一个或多个与此拨入访问号码的拨号计划关联的区域，然后单击“确定”。

13. 要从拨入访问号码中删除某个区域，请在“关联区域”下，单击要删除的区域，然后单击“删除”。

14. 单击“提交”。

