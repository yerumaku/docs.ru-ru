---
title: "Интерфейсы API для поддержки размещения в собственном браузере WPF"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: AutoGeneratedOrientationPage
helpviewer_keywords:
- browser hosting support [WPF]
- WPF browser hosting support APIs [WPF]
ms.assetid: 82c133a8-d760-45fb-a2b9-3a997537f1d4
caps.latest.revision: "33"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 87b7b8491fe07f5ab1f93ba332e50333a366f109
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="native-wpf-browser-hosting-support-apis"></a>Интерфейсы API для поддержки размещения в собственном браузере WPF
Размещение [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)] приложений в веб-браузеров можно добиться с помощью сервера активных документов (также известного как DocObject), зарегистрированного вне узла WPF. [!INCLUDE[TLA2#tla_ie](../../../../includes/tla2sharptla-ie-md.md)]напрямую можно активировать и интегрировать в активном документе. Для размещения приложений XBAP и свободных XAML-документов в браузерах Mozilla [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)] предоставляет подключаемый модуль NPAPI, который обеспечивает аналогичную среду размещения для [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)] сервера активных документов как [!INCLUDE[TLA2#tla_ie](../../../../includes/tla2sharptla-ie-md.md)] does. Тем не менее самым простым практическим способом размещения приложений XBAP и XAML документов в других браузерах и автономных приложениях является использование элемента управления веб-браузера Internet Explorer. Элемент управления веб-браузер предоставляет сложные среда размещения сервера активных документов, а также включает собственную узла настроить и расширить эту среду и напрямую взаимодействовать с текущим объектом активного документа.  
  
 [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)] Сервера активных документов реализует несколько общих интерфейсов размещения, включая [IOleObject](http://go.microsoft.com/fwlink/?LinkId=162049), [IOleDocument](http://go.microsoft.com/fwlink/?LinkId=162050), [IOleInPlaceActiveObject](http://go.microsoft.com/fwlink/?LinkId=162051), [IPersistMoniker](http://go.microsoft.com/fwlink/?LinkId=162045), [IOleCommandTarget](http://go.microsoft.com/fwlink/?LinkId=162047). При размещении в элементе управления веб-браузер этих интерфейсов может быть запросов из объекта, возвращаемого [IWebBrowser2::Document](http://go.microsoft.com/fwlink/?LinkId=162048) свойство.  
  
## <a name="iolecommandtarget"></a>IOleCommandTarget  
 Реализация сервера активных документов WPF [IOleCommandTarget](http://go.microsoft.com/fwlink/?LinkId=162047) поддерживает множество связанных с навигацией и обозревателем команд стандартные группы команд OLE (при значении null GUID группы команд). Кроме того он распознает пользовательской команды группа с именем CGID_PresentationHost. В настоящее время имеется только одна команда, определенная в этой группе.  
  
```  
DEFINE_GUID(CGID_PresentationHost, 0xd0288c55, 0xd6, 0x4f5e, 0xa8, 0x51, 0x79, 0xde, 0xc5, 0x1b, 0x10, 0xec);  
enum PresentationHostCommands {   
   PHCMDID_TABINTO = 1   
};  
```  
  
 PHCMDID_TABINTO предписывает PresentationHost, чтобы перенести фокус на первый или последний элемент может иметь фокус в его содержимом, в зависимости от состояния клавиши Shift.  
  
## <a name="in-this-section"></a>В этом разделе  
 [IEnumRAWINPUTDEVICE](../../../../docs/framework/wpf/app-development/ienumrawinputdevice.md)  
 [IWpfHostSupport](../../../../docs/framework/wpf/app-development/iwpfhostsupport.md)
