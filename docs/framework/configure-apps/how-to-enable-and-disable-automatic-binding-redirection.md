---
title: "Практическое руководство. Включение и отключение автоматического перенаправления привязки | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
  - "VB"
  - "CSharp"
  - "C++"
helpviewer_keywords: 
  - "сборки [платформа .NET Framework], перенаправление привязки"
  - "параллельное выполнение, перенаправление привязки сборок"
ms.assetid: 5fca42f3-bdce-4b81-a704-61e42c89d3ba
caps.latest.revision: 17
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 17
---
# Практическое руководство. Включение и отключение автоматического перенаправления привязки
Начиная с [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)] при компиляции приложений, нацеленных на [!INCLUDE[net_v451](../../../includes/net-v451-md.md)], в файл конфигурации приложения могут автоматически быть добавлены переадресации привязок для переопределения унификации сборок.  Переадресации привязок добавляются, если приложение или его компоненты ссылаются на несколько версий одной сборки, даже если вручную указать переадресации привязок в файле конфигурации приложения.  Функция автоматической переадресации привязки затрагивает классические приложения и веб\-приложения, нацеленные на [!INCLUDE[net_v451](../../../includes/net-v451-md.md)], хотя в случае веб\-приложений она ведет себя несколько иначе.  Автоматическую переадресацию привязки можно включить при наличии существующих приложений, нацеленных на предыдущие версии .NET Framework; также можно отключить эту функцию, если требуется сохранить созданные вручную переадресации привязок.  
  
## Отключение автоматической переадресации привязок в классических приложениях  
 Автоматические переадресации привязки включены по умолчанию для классических приложений, нацеленных на [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] и более позних версий.  Переадресации привязок добавляются в выходной файл конфигурации \(app.config\), когда приложение компилируется и переопределяет унификацию сборок, которая может произойти в противном случае.  Исходный файл app.config не изменяется.  Для отключения этой функции необходимо внести изменения в файл проекта для приложения.  
  
#### Отключение автоматических переадресаций привязки  
  
1.  В Visual Studio выберите проект в **Обозревателе решений** и выберите **Открыть папку в проводнике** в контекстном меню.  
  
2.  В проводнике найдите файл проекта \(с расширением .csproj или .vbproj\) и откройте его в Блокноте.  
  
3.  Найдите в файле проекта следующую запись свойства:  
  
     `<AutoGenerateBindingRedirects>true</AutoGenerateBindingRedirects>`  
  
4.  Измените `true` на `false`:  
  
     `<AutoGenerateBindingRedirects>false</AutoGenerateBindingRedirects>`  
  
## Ручное включение автоматической переадресации привязок  
 Можно включить автоматические переадресации привязок в существующих приложениях, нацеленных на более старые версии .NET Framework, либо в случаях, когда не появляется автоматический запрос на добавление переадресации.  Если вы ориентируетесь на более новую версию платформы, но не получаете автоматический запрос на добавление переадресации, скорее всего, в полученных выходных данных сборки вам будет предложено пересопоставить сборки.  
  
#### Ручное добавление свойства автоматической переадресации привязки  
  
1.  В Visual Studio выберите проект в **Обозревателе решений** и выберите **Открыть папку в проводнике** в контекстном меню.  
  
2.  В проводнике найдите файл проекта \(с расширением .csproj или .vbproj\) и откройте его в Блокноте.  
  
3.  Добавьте следующий элемент в первую группу свойств конфигурации \(ниже тега \<PropertyGroup\>\):  
  
     `<AutoGenerateBindingRedirects>true</AutoGenerateBindingRedirects>`  
  
     Ниже показан пример файла проекта со вставленным элементом.  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <Project ToolsVersion="12.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
      <Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" Condition="Exists('$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props')" />  
      <PropertyGroup>  
        <Configuration Condition=" '$(Configuration)' == ''     ">Debug</Configuration>  
        <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>  
        <ProjectGuid>{123334}</ProjectGuid>  
        ...  
        <AutoGenerateBindingRedirects>true</AutoGenerateBindingRedirects>  
      </PropertyGroup>  
    ...  
    </Project>  
  
    ```  
  
4.  Скомпилируйте приложение.  
  
## Включение автоматической переадресации привязок в веб\-приложениях  
 Для веб\-приложений автоматические переадресации привязок реализованы иным образом.  Поскольку в исходный файл конфигурации \(web.config\) для веб\-приложений должны вноситься изменения, переадресации привязки не добавляются в файл конфигурации автоматически.  Однако Visual Studio уведомляет вас о конфликтах привязки, и вы можете добавлять переадресации привязок для разрешения конфликтов.  Поскольку на добавление переадресации привязок всегда выводятся запросы, нет необходимости явно отключать эту функцию для веб\-приложения.  
  
#### Добавление переадресаций привязок в файл web.config  
  
1.  В Visual Studio скомпилируйте приложение и проверьте его на наличие предупреждений сборки.  
  
     ![Предупреждение сборки для конфликтов ссылок сборок](../../../docs/framework/configure-apps/media/clr-assemblyrefwarning.png "CLR\_AssemblyRefWarning")  
  
2.  При наличии конфликтов привязки сборок выводится предупреждение.  Дважды щелкните предупреждение.  \(Клавиатура: выберите предупреждение и нажмите клавишу **ВВОД**.\)  
  
     Откроется диалоговое окно, которое позволяет автоматически добавить необходимые переадресации привязки в исходный файл web.config.  
  
     ![Диалоговое окно разрешений для переадресации привязки](../../../docs/framework/configure-apps/media/clr-addbindingredirect.png "CLR\_AddBindingRedirect")  
  
## См. также  
 [Элемент \<bindingRedirect\>](../../../docs/framework/configure-apps/file-schema/runtime/bindingredirect-element.md)   
 [Перенаправление версий сборки](../../../docs/framework/configure-apps/redirect-assembly-versions.md)