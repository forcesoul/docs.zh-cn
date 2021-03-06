---
title: 属性设计
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- member design guidelines, properties
- properties [.NET Framework], design guidelines
ms.assetid: 127cbc0c-cbed-48fd-9c89-7c5d4f98f163
author: KrzysztofCwalina
ms.openlocfilehash: 1d119b48f0524b3e997aa2cb9ea2cbbd855afdf0
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53131451"
---
# <a name="property-design"></a>属性设计
虽然属性在技术上与方法非常相似，但它们的使用场景却截然不同。 属性应被视为聪明的字段。 它们兼具字段的调用语法和方法的灵活性。  
  
 **✓ 务必** 创建仅限 get 的属性，如果调用方应不能更改属性的值。  
  
 请记住，如果属性的类型是可变的引用类型，则即使属性为 get-only，也可以更改属性值。  
  
 **X 切忌** 仅属性的 setter 具有更广泛的可访问性比 getter 提供。  
  
 例如，不要使用具有公共 setter 和受保护的 getter 的属性。  
  
 如果无法提供属性 getter，请将该功能实现为方法。 考虑将方法名称以 `Set` 开始，在后面添加你对该属性的命名。 如，<xref:System.AppDomain> 有一个名为 `SetCachePath` 的方法，而不是一个名为 `CachePath` 的 set-only 属性。  
  
 **✓ 务必** 提供的所有属性，确保，默认值不会导致安全漏洞或您对此低效代码的意义的默认值。  
  
 **✓ 务必** 允许将属性按任何顺序设置，即使这会导致临时无效状态的对象。  
  
 在给定同一对象上的其他属性的值的情况下，一个属性的某些值可能是无效的，这是导致两个或多个属性相关联的一种常见况。 在这种情况下，无效状态导致的异常应该会推迟，直到对象实际将这些相关属性一起使用。  
  
 **✓ 务必** 保留以前的值，如果属性 setter 将引发异常。  
  
 **X 避免** 属性 getter 从引发异常。  
  
 属性 getter 应该是简单的操作，不应该有任何前置条件。 如果某个 getter 可能会引发异常，则应该将其重新设计为方法。 请注意，此规则不适用于索引器，因为我们确实会因验证参数而导致异常。  
  
### <a name="indexed-property-design"></a>索引属性设计  
 索引属性是一个特殊属性，可以具有参数，并且可以使用与数组索引类似的特殊语法进行调用。  
  
 索引属性通常称为索引器。 索引器应仅用于提供对逻辑集合中项目的访问的 API。 例如，字符串是字符的集合，在索引器上添加了 <xref:System.String?displayProperty=nameWithType> 即可访问其字符。  
  
 **✓ 考虑**使用索引器提供对存储在内部数组中的数据的访问权限。  
  
 **✓ 考虑**为表示项目集合的类型提供索引器。  
  
 **X 避免**使用带有一个以上参数的索引属性。  
  
 如果设计需要多个参数，请重新考虑该属性是否真正代表逻辑集合的访问者。 如果不是，请改用方法。 考虑使用 `Get` 或 `Set` 开头的方法名称。  
  
 **X 避免** 使用具有 <xref:System.Int32?displayProperty=nameWithType>、<xref:System.Int64?displayProperty=nameWithType>、<xref:System.String?displayProperty=nameWithType>、<xref:System.Object?displayProperty=nameWithType> 以外参数类型的索引器，或枚举。  
  
 如果设计需要其他类型的参数，请仔细重新评估 API 是否真正代表逻辑集合的访问者。 如果不是，请使用方法。 考虑使用 `Get` 或 `Set` 开头的方法名称  
  
 **✓ 务必**使用 `Item` 作为索引属性的名称，除非有明显更好的名称（例如，请参阅 `System.String` 上的 <xref:System.String.Chars%2A>属性）。  
  
 在 C# 中，索引器默认名称为 Item。 <xref:System.Runtime.CompilerServices.IndexerNameAttribute> 可用于自定义此名称。  
  
 **X 切忌**提供在语义方面等效的索引器和方法。  
  
 **X 切忌**在一种类型中提供多个重载索引器系列。  
  
 此准则由 C# 编译器强制执行。  
  
 **X 切忌**使用非默认索引属性。  
  
 此准则由 C# 编译器强制执行。  
  
### <a name="property-change-notification-events"></a>属性更改通知事件  
 有时，提供用于通知用户属性值更改的事件是很有用的。 例如，`System.Windows.Forms.Control` 在其 `Text` 属性的值发生变化后引发 `TextChanged` 事件。  
  
 **✓ 考虑** 引发更改通知事件修改高级 Api （通常是设计器组件） 中的属性值时。  
  
 如果具备可让用户知道对象的属性何时发生变化的有效方案，则该对象应该该属性引发更改通知事件。  
  
 但是，可能并不值得为基础类型或集合等低级 API 引发此类事件。 例如，向列表添加新项且 `Count` 属性更改时，<xref:System.Collections.Generic.List%601> 不会引发此类事件。  
  
 **✓ 考虑** 引发更改通知事件的属性的值更改通过外部强制时。  
  
 如果在属性值更改通过某种外部因素 （以通过在对象上调用方法以外的其他方式），则引发事件指示向开发人员的值正在更改和已更改。 一个典型示例是`Text`文本框控件的属性。 当用户键入文本中的`TextBox`，会自动更改的属性值。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *通过从 Pearson Education，Inc.的权限重新打印[Framework 设计准则：约定、 语法和模式的可重用.NET 库，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison-wesley 专业人员。*  
  
## <a name="see-also"></a>请参阅

- [成员设计准则](../../../docs/standard/design-guidelines/member.md)  
- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
