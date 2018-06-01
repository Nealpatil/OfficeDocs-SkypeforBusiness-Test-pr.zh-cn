﻿---
title: Lync Server 2013 中的 DNS 负载平衡
TOCTitle: Lync Server 2013 中的 DNS 负载平衡
ms:assetid: 7ed0ed20-33ad-4253-926d-21d392590ae7
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg398634(v=OCS.15)
ms:contentKeyID: 49313389
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 DNS 负载平衡

 

_**上一次修改主题：** 2016-12-08_

Lync Server 可实现 DNS 负载平衡，这是一种可以大幅降低用于网络负载平衡的管理开销的软件解决方案。DNS 负载平衡可平衡 Lync Server 独有的网络流量，例如 SIP 流量和媒体流量。

如果部署 DNS 负载平衡，则组织用于硬件负载平衡器的管理开销将降至最低。此外，还可以免除解决 SIP 流量负载平衡器配置错误相关问题的复杂过程。您还可以阻止服务器连接以使服务器脱机。同时，DNS 负载平衡还可确保硬件负载平衡器问题不会影响 SIP 流量的元素，例如基本呼叫路由。

与为所有类型的流量使用硬件负载平衡器相比，使用 DNS 负载平衡还可以降低您购买硬件负载平衡器的成本。您应该使用已通过与 Lync Server 的互操作性资格测试的负载平衡器。有关负载平衡器互操作性测试的详细信息，请参阅“Lync Server 2010 负载平衡器合作伙伴”，网址为 <http://go.microsoft.com/fwlink/?linkid=202452>。

前端池、边缘服务器池、控制器池和独立的中介服务器池都支持 DNS 负载平衡。

## 前端池和控制器池中的 DNS 负载平衡

您可以使用 DNS 负载平衡来平衡前端池和控制器池中的 SIP 流量。部署 DNS 负载平衡后，仍需要对这些池使用硬件负载平衡器，但仅用于客户端到服务器的 HTTPS 流量。硬件负载平衡器用于通过端口 443 和 80 从客户端传入的 HTTPS 流量。

尽管这些池中仍需要硬件负载平衡器，但这些负载平衡器的安装和管理主要用于硬件负载平衡器管理员熟悉的 HTTPS 流量。

## 支持旧客户端和服务器并对其进行 DNS 负载平衡

DNS 负载平衡仅支持运行 Lync Server 2013 或 Lync Server 2010 的服务器以及 Lync 2013 和 Lync 2010 客户端的自动故障转移。早期版本的客户端和 Office Communications Server 仍可以连接到运行 DNS 负载平衡的池，但是如果不能与 DNS 负载平衡将其指引到的第一台服务器建立连接，将无法故障转移到池中的其他服务器。

此外，如果您使用的是 Exchange UM，则必须至少使用 Exchange 2010 SP1 版本才能支持 Lync Server DNS 负载平衡。如果使用较早版本的 Exchange，则在以下 Exchange UM 方案中无法为您的用户提供故障转移功能：

  - 在其电话上播放“企业语音”语音邮件

  - 转接来自 Exchange UM 自动助理的呼叫

其他所有 Exchange UM 方案将正常工作。

## 在前端池和控制器池中部署 DNS 负载平衡

在前端池和控制器池中部署 DNS 负载平衡时，需要使用 FQDN 和 DNS 记录执行一些额外步骤。

  - 使用 DNS 负载平衡的池必须具有两个 FQDN：一个是 DNS 负载平衡使用的常规池 FQDN（例如 pool01.contoso.com），它解析为该池中服务器的物理 IP；另一个是池的 Web 服务的 FQDN（例如 web01.contoso.com），它解析为该池的虚拟 IP 地址。
    
    在拓扑生成器中，如果要为池部署 DNS 负载平衡，以便为池的 Web 服务创建此额外 FQDN，则必须选中“覆盖内部 Web 服务池 FQDN”复选框，并在“指定该池的 Web 服务 URL”页中键入 FQDN。

  - 要支持 DNS 负载平衡使用的 FQDN，必须设置 DNS，以便将池 FQDN（例如 pool01.contoso.com）解析为该池中所有服务器的 IP 地址（例如，192.168.1.1、192.168.1.2 等）。您应该仅包含当前部署的服务器的 IP 地址。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ656815.warning(OCS.15).gif" title="warning" alt="warning" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果有多个前端池或前端服务器，则外部 Web 服务 FQDN 必须是唯一的。例如，如果将前端服务器的外部 Web 服务 FQDN 定义为 <strong>pool01.contoso.com</strong>，则不能将 <strong>pool01.contoso.com</strong> 用于另一个前端池或前端服务器。如果您还部署控制器，则为任何控制器或控制器池定义的外部 Web 服务 FQDN 必须与任何其他控制器或控制器池以及任何前端池或前端服务器的不同。如果决定使用自定义的 FQDN 覆盖内部 Web 服务，则每个 FQDN 都必须不同于任何其他前端池、控制器或控制器池。</td>
    </tr>
    </tbody>
    </table>


## 边缘服务器池中的 DNS 负载平衡

您可以在边缘服务器池中部署 DNS 负载平衡。如果要进行部署，则必须了解以下注意事项。

在边缘服务器中使用 DNS 负载平衡会导致以下方案中丧失故障转移功能：

  - 与运行 Lync Server 2010 之前的 Office Communications Server 版本的组织建立联盟。

  - 除了与基于 XMPP 的提供商和服务器（例如 Google Talk）进行即时消息交换外，也与使用公共即时消息 (IM) 服务 AOL 和 Yahoo\! 的用户进行即时消息交换。
    
    <table>
    <colgroup>
    <col style="width: 100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398794.important(OCS.15).gif" title="important" alt="important" />重要提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><ul>
    <li><p>Google Talk 目前是唯一受支持的 XMPP 合作伙伴。</p></li>
    <li><p>自 2012 年 9 月 1 日起，新订或续订合同不能再购买 Microsoft Lync 公共 IM 连接用户订阅许可证 (“PIC USL”)。拥有有效许可证的客户可继续与 Yahoo! Messenger 联盟直至服务关闭。AOL 和 Yahoo! 的生命周期结束日期已宣布，为 2014 年 6 月。有关详细信息，请参阅 <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公共即时消息连接支持</a>。</p></li>
    </ul></td>
    </tr>
    </tbody>
    </table>


只要池中的所有边缘服务器都在运行，这些方案就会正常工作；但是如果某台边缘服务器不可用，则发送到该服务器的对这些方案的所有请求都将失败，而不会路由到其他边缘服务器。

如果您使用的是 Exchange UM，则必须至少使用 Exchange 2013 才能在边缘上支持 Lync Server DNS 负载平衡。如果使用较早版本的 Exchange，则在以下 Exchange UM 方案中无法为您的远程用户提供故障转移功能：

  - 在其电话上播放“企业语音”语音邮件

  - 转接来自 Exchange UM 自动助理的呼叫

其他所有 Exchange UM 方案将正常工作。

内部边缘接口和外部边缘接口必须使用同一类型的负载平衡。您不能对一个边缘接口使用 DNS 负载平衡，而对另一个边缘接口使用硬件负载平衡。

## 在边缘服务器池中部署 DNS 负载平衡

要在边缘服务器池的外部接口上部署 DNS 负载平衡，需要具有以下 DNS 条目：

  - 对于访问边缘服务，池中的每台服务器都需要有一个条目。每个条目必须将访问边缘服务的 FQDN（例如 sip.contoso.com）解析为该池中某台边缘服务器上访问边缘服务的 IP 地址。

  - 对于 Web 会议边缘服务，池中的每台服务器都需要有一个条目。每个条目必须将 Web 会议边缘服务的 FQDN（例如 webconf.contoso.com）解析为该池中某台边缘服务器上 Web 会议边缘服务的 IP 地址。

  - 对于音频/视频边缘服务，池中的每台服务器都需要有一个条目。每个条目必须将音频/视频边缘服务的 FQDN（例如 av.contoso.com）解析为该池中某台边缘服务器上音频/视频边缘服务的 IP 地址。

要在边缘服务器池的内部接口上部署 DNS 负载平衡，必须添加一条将此边缘服务器池的内部 FQDN 解析为该池中每台服务器的 IP 地址的 DNS A 记录。

## 在中介服务器池中使用 DNS 负载平衡

可以在独立的中介服务器池上使用 DNS 负载平衡。所有 SIP 和媒体流量都通过 DNS 负载平衡进行平衡。

要在中介服务器池中部署 DNS 负载平衡，必须设置 DNS，以便将池 FQDN（例如 mediationpool1.contoso.com）解析为该池中所有服务器的 IP 地址（例如，192.168.1.1、192.168.1.2 等）。

## 使用 DNS 负载平衡阻止到服务器的流量

如果使用 DNS 负载平衡并且需要阻止至特定计算机的流量，则仅仅删除池 FQDN 中的 IP 地址条目是不够的。您还必须删除计算机的 DNS 条目。

请注意，对于服务器到服务器的流量，Lync Server 2013 将使用可识别拓扑的负载平衡。服务器读取中央管理存储中已发布的拓扑以在拓扑中获取服务器的 FQDN，并且在各服务器之间自动分发流量。若要阻止服务器接收服务器到服务器的流量，则必须从拓扑中删除服务器。
