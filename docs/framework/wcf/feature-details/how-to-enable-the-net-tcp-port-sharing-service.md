---
title: 如何：启用 Net.TCP 端口共享服务
ms.date: 03/30/2017
helpviewer_keywords:
- port sharing [WCF]
- activation services [WCF]
ms.assetid: c9175af4-c27c-4765-bf45-b8f7528a7282
ms.openlocfilehash: 4b5a18e11d9fc15f23b5353883a63d838face58a
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33490755"
---
# <a name="how-to-enable-the-nettcp-port-sharing-service"></a>如何：启用 Net.TCP 端口共享服务
Windows Communication Foundation (WCF) 使用名为 Net.TCP 端口共享服务的 Windows 服务以方便在多个进程之间共享 TCP 端口。 此服务已安装作为一部分 WCF，但该服务未启用默认情况下，作为安全措施，并且因此必须手动启用在首次使用之前。 本主题描述如何使用 Microsoft 管理控制台 (MMC) 管理单元配置 Net TCP 端口共享服务。  
  
 启用 Net.TCP 端口共享服务并手动启动后，请参阅[如何： 配置 WCF 服务以使用端口共享](../../../../docs/framework/wcf/feature-details/how-to-configure-a-wcf-service-to-use-port-sharing.md)有关如何配置你的服务以使用此服务的信息。  
  
 有关使用 net.tcp:// 端口共享的示例，请参阅[Net.TCP 端口共享示例](../../../../docs/framework/wcf/samples/net-tcp-port-sharing-sample.md)。  
  
### <a name="to-enable-the-nettcp-port-sharing-service-using-mmc"></a>使用 MMC 启用 Net.TCP 端口共享服务  
  
1.  从开始菜单中，打开服务管理控制台通过打开命令提示符窗口并键入`services.msc`或通过打开运行并键入`services.msc`在打开的框中。  
  
2.  在**名称**services，对列表的列右键单击**Net.Tcp Port Sharing Service**，然后选择**属性**从菜单。  
  
3.  若要启用该服务的手动启动在**属性**窗口中选择**常规**选项卡上，然后在**启动类型**框中选择手动，并依次**应用**。  
  
4.  若要启动服务，服务状态区域中，单击**启动**按钮。 现在，服务状态区域应显示为“已启动”。  
  
5.  若要返回到服务的列表，请单击**确定**，并退出 MMC 控制台。  
  
## <a name="example"></a>示例  
  
## <a name="see-also"></a>请参阅  
 [Net.TCP 端口共享](../../../../docs/framework/wcf/feature-details/net-tcp-port-sharing.md)  
 [配置 Net.TCP 端口共享服务](../../../../docs/framework/wcf/feature-details/configuring-the-net-tcp-port-sharing-service.md)
