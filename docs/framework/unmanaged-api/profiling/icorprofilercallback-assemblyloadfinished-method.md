---
title: "Метод ICorProfilerCallback::AssemblyLoadFinished"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerCallback.AssemblyLoadFinished
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerCallback::AssemblyLoadFinished
helpviewer_keywords:
- ICorProfilerCallback::AssemblyLoadFinished method [.NET Framework profiling]
- AssemblyLoadFinished method [.NET Framework profiling]
ms.assetid: 86d98f39-52e6-4c61-a625-9760f695ff12
topic_type: apiref
caps.latest.revision: "13"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 9de280a1b92bc921ecb400c80522f21cf65f861a
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="icorprofilercallbackassemblyloadfinished-method"></a>Метод ICorProfilerCallback::AssemblyLoadFinished
Уведомляет профилировщик об окончании загрузки сборки.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT AssemblyLoadFinished(  
    [in] AssemblyID assemblyId,  
    [in] HRESULT    hrStatus);  
```  
  
#### <a name="parameters"></a>Параметры  
 `assemblyId`  
 [in] Идентифицирует сборку, которая была загружена.  
  
 `hrStatus`  
 [in] Значение HRESULT, указывающее, является ли сборка Загрузка завершена успешно.  
  
## <a name="remarks"></a>Примечания  
 Значение `assemblyId` является недопустимым для информационного запроса до `AssemblyLoadFinished` вызывается метод.  
  
 Некоторые части загрузки сборки может быть продолжено после `AssemblyLoadFinished` обратного вызова. Значение HRESULT в `hrStatus` указывает на сбой. Тем не менее значение HRESULT в `hrStatus` указывает только на том, что в первой части загрузки сборки.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** CorProf.idl, CorProf.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Интерфейс ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
