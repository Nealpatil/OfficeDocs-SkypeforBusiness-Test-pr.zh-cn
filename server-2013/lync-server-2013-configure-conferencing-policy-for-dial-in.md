﻿---
title: Lync Server 2013：配置电话拨入式会议策略
TOCTitle: 配置电话拨入式会议策略
ms:assetid: 9bf926d6-0248-4352-98c3-9c5a333debbc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg398810(v=OCS.15)
ms:contentKeyID: 49313732
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中配置电话拨入式会议策略

 

_**上一次修改主题：** 2014-03-21_

会议策略是一种用户帐户设置，用于指定参与者的会议体验。您可以创建具有站点作用域或用户作用域的会议策略。会议策略设置包含会议安排和参与会议的多个方面。一些会议策略设置支持参与者参加电话拨入式会议。当您配置电话拨入式会议时，应该确认已针对组织正确设置了这些字段，并根据需要进行修改。

请验证会议策略中的下列字段：

  - **允许参与者邀请匿名用户** 此设置允许会议组织者邀请匿名（即未经身份验证）参与者参加会议。此设置对于电话拨入式会议是可选的。默认情况下，在默认全局会议策略中，此设置处于选中状态。

  - **启用 PSTN 电话拨入式会议** 此设置允许用户通过从 PSTN 拨入来加入会议的音频部分。此设置对于电话拨入式会议是必需的。默认情况下，在默认全局会议策略中，此设置处于选中状态。

  - **允许匿名参与者拨出** 此设置允许已加入会议的匿名用户拨出电话号码来加入会议的音频部分。此设置对于电话拨入式会议是可选的。默认情况下，在默认全局会议策略中，此设置处于未选中状态。

  - **允许未启用 企业语音的参与者拨出**    此设置允许未启用 企业语音的会议参与者和组织者拨出电话号码来加入会议的音频部分。将基于组织分配的语音策略授权电话拨出式呼叫。默认情况下，在默认全局会议策略中，此设置处于未选中状态。将禁用此设置默认值。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要启用此功能，未启用 企业语音 的会议组织者应分配有适当的语音策略，以授权来自该用户组织的会议的任何拨出。可通过 Lync Server 命令行管理程序 向未启用企业语音的用户分配语音策略。如果用户没有显式分配的语音策略，则全局语音策略将用于授权拨出请求。如果没有网站语音策略，则将使用全局语音策略。 </td>
    </tr>
    </tbody>
    </table>


本节中的过程解释如何修改会议策略。有关如何配置定义默认会议策略中的参与者体验的所有设置的详细信息，请参阅 [在 Lync Server 2013 中创建或修改会议配置设置的集合](lync-server-2013-create-or-modify-a-collection-of-meeting-configuration-settings.md)。有关如何为特定用户或用户组创建会议策略的详细信息，请参阅 [在 Lync Server 2013 中创建或修改会议策略](lync-server-2013-create-or-modify-a-conferencing-policy.md)。有关所有可用会议策略设置的列表，请参阅 [在 Lync Server 2013 中会议策略设置参考](lync-server-2013-conferencing-policy-settings-reference.md)。

## 修改拨入的会议策略

1.  以 RTCUniversalServerAdmins 组成员或者 **Cs-ServerAdministrator** 或 **CsAdministrator** 角色成员的身份登录计算机。

2.  打开浏览器窗口，然后输入管理 URL 以打开 Lync Server 控制面板。有关可以用于启动 Lync Server 控制面板的不同方法的详细信息，请参阅[打开 Lync Server 管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左侧导航栏中，单击“会议”。

4.  在“会议策略”选项卡上，双击会议策略名称打开“编辑会议策略”对话框。

5.  确认电话拨入式会议的字段适合您的组织，并根据需要修改设置。

6.  单击“提交”。

