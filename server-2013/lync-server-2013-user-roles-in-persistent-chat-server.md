﻿---
title: 持久聊天服务器中的用户角色
TOCTitle: 持久聊天服务器中的用户角色
ms:assetid: 343a0563-9ca5-4ad0-b4f3-a72f1d7f1a81
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ676774(v=OCS.15)
ms:contentKeyID: 49888372
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 持久聊天服务器中的用户角色

 

_**上一次修改主题：** 2015-03-19_

持久聊天服务器提供允许/拒绝的成员的概念，适用于持久聊天类别且控制可以访问特定类别的聊天室的用户。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398794.important(OCS.15).gif" title="important" alt="important" />重要提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>类别中的允许/拒绝的成员与<strong>成员</strong>角色（适用于持久聊天聊天室）不同。<br />
搜索显示进行搜索的用户位于其允许/拒绝的成员列表中的所有打开和关闭的聊天室。不会显示加密聊天室，除非进行搜索的用户是加密聊天室的成员。用户只能搜索自己已经是其成员的聊天室，或者他们可以请求成员身份的聊天室。</td>
</tr>
</tbody>
</table>


允许/拒绝的成员概念的主要原理是信息隔离墙。例如，银行和财务机构通常设立了阻止贸易商和分析师在实施策略和约定时共享通信的信息隔离区域。若要满足此要求，管理员可以创建相应类别，以便一个类别允许创建聊天室并允许贸易商使用该聊天室，而另一个类别允许创建聊天室并允许分析师使用该聊天室。在系统中设计此约束可禁止在父类别阻止某用户时将该用户添加为聊天室的成员。

以下是持久聊天服务器的四个用户角色：

  - **创建者：** 有权创建聊天室的用户。这些用户位于特定类别的“创建者”列表中：他们可以在该类别中创建聊天室，还可以根据该类别分配成员身份，以及指派管理员管理聊天室。创建聊天室的用户将自动添加为聊天室的管理员。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>成为创建者仅仅为其提供创建聊天室的权限。通过自动升级为管理员，创建者才能够在已创建的聊天服务中进一步细化成员身份、管理员等等。</td>
    </tr>
    </tbody>
    </table>
    
    此角色使您能够控制在您的组织中创建聊天室的用户，尤其是当您要集中管理聊天室创建活动以强制实施策略和约定并且随后将聊天室管理权委派给组织中的其他用户时。

  - **管理员：** 管理聊天室属性的用户。聊天室管理员可以修改成员列表（添加和移除成员），以及修改聊天室管理员列表（添加和移除管理员）。聊天室管理员可以将自己添加到成员或演示者列表（对于大会堂聊天室）中以便他们可以加入聊天室。聊天室管理员还可以禁用聊天室（管理员可查询已禁用聊天室且可以将其永久删除）。除聊天室的类别外，管理员可以更改聊天室的所有属性。只有持久聊天管理员可以在创建聊天室之后更改类别。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398794.important(OCS.15).gif" title="important" alt="important" />重要提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果该管理员还是其他类别的创建者，则他/她可以更改该类别以使自己有权创建聊天室。</td>
    </tr>
    </tbody>
    </table>


  - **成员：** 作为聊天室成员的用户。这些用户可以查看目录中的聊天室（即使聊天室是保密的），以及订阅聊天室（包括未读消息、自我筛选器和关键字筛选器等元数据选项）并加入聊天室（可以发布内容，除非该聊天室是只有演示者才能发布、获取内容和进行搜索的大会堂聊天室）。不是聊天室成员的用户若位于该类别的“允许的成员”列表中，则可搜索聊天室，但需要请求访问权才能加入这些聊天室来访问内容。（系统中未内置请求访问权或审批功能；这些操作需通过电子邮件、电话或其他联系方式在外部完成。）

  - **演示者：** 可以在大会堂聊天室发布消息的用户。

以下角色是持久聊天服务器的管理员角色：

  - **持久聊天管理员 (CsPersistentChatAdministrator)：** 这是一个管理持久聊天服务器的新的基于角色的访问控制 (RBAC) 角色。指定为 CsPersistentChatAdministrator 的用户或安全组能够通过远程（即，在持久聊天服务器以外的计算机中）使用 Windows PowerShell cmdlet 来管理持久聊天服务器。持久聊天服务器检查确认持久聊天管理员是否为持久聊天服务器前端服务器上本地组“RTC Local administrator”的成员。
    
    CsPersistentChatAdministrator 角色可以管理聊天室（修改包括成员身份、管理员、类别在内的所有属性，将聊天室标记为禁用），以及创建和管理用于定义可创建和访问聊天室的用户的聊天室类别。管理员还可以将聊天室标记为禁用并清理不再处于活动状态的聊天室。管理员不会受到“创建者”或“允许的成员”限制的影响。管理员可以创建任何类型的聊天室以及将自己添加为任何聊天室的成员。管理员还可以修改和管理持久聊天配置（池属性、全局设置以及合规性配置）并且还可以规划和实施从旧群聊服务器部署到 Lync Server 2013持久聊天服务器的迁移。

  - **Lync 管理员：** 负责部署的 Lync Server 2013 的整个企业管理员。

  - **操作管理员：** 负责管理日常操作的用户。

  - **第三方开发人员和合作伙伴：** 第三方开发人员可扩展系统，特别是针对组会话、合规性支持和工具、Web/移动客户端和自动程序开发框架提供信息隔离墙解决方案。

