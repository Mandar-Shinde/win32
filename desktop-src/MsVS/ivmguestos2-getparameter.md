---
title: IVMGuestOS2 GetParameter method
description: Retrieves a configuration parameter inside the guest operating system.
ms.assetid: e8051245-f063-49b6-bb5e-90e5a79cd4ea
keywords:
- GetParameter method Virtual Server
- GetParameter method Virtual Server , IVMGuestOS2 interface
- IVMGuestOS2 interface Virtual Server , GetParameter method
- GetParameter method Virtual Server , VMGuestOS2 interface
- VMGuestOS2 interface Virtual Server , GetParameter method
topic_type:
- apiref
api_name:
- IVMGuestOS2.GetParameter
- VMGuestOS2.GetParameter
api_location:
- VsComInterfaces.h
api_type:
- COM
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
---

# IVMGuestOS2::GetParameter method

Retrieves a configuration parameter inside the guest operating system.

## Syntax


```C++
HRESULT GetParameter(
  [in]  BSTR inParameterName,
  [out] BSTR *outParameterValue
);
```



## Parameters

<dl> <dt>

*inParameterName* \[in\]
</dt> <dd>

The parameter name. It must be between 1 and 255 characters in length and cannot contain a backslash (\) character.

</dd> <dt>

*outParameterValue* \[out\]
</dt> <dd>

The parameter value.

</dd> </dl>

## Return value

This method can return one of these values.



| Return code                                                                                                          | Description                                                                 |
|----------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| <dl> <dt>**S\_OK**</dt> </dl>                                 | The operation was successful.<br/>                                    |
| <dl> <dt>**E\_INVALIDARG**</dt> </dl>                         | The *outParameterValue* parameter is not valid or not specified.<br/> |
| <dl> <dt>**VM\_E\_VM\_NOT\_RUNNING**</dt> </dl>               | The virtual machine is not running.<br/>                              |
| <dl> <dt>**VM\_E\_VM\_PAUSED**</dt> </dl>                     | The virtual machine is paused.<br/>                                   |
| <dl> <dt>**VM\_E\_ADDITIONS\_FEATURE\_NOT\_AVAIL**</dt> </dl> | Additions are not installed in this virtual machine.<br/>             |
| <dl> <dt>**DISP\_E\_EXCEPTION**</dt> </dl>                    | An unexpected error has occurred.<br/>                                |



 

## Remarks

The virtual machine must be running and Additions must be installed when this method is invoked. This method is supported only for Windows-based guest operating systems.

With Additions installed, the following key is automatically added to the guest operating system's registry:

-   **HKEY\_LOCAL\_MACHINE**\\**SOFTWARE**\\**Microsoft**\\**Virtual Machine**\\**Guest**\\**Parameters**

When the guest operating system starts, the following registry string values are populated in the Parameters key:

-   HostName
-   PhysicalHostName
-   PhysicalHostNameFullyQualified
-   VirtualMachineName

## Requirements



|                     |                                                                                                   |
|---------------------|---------------------------------------------------------------------------------------------------|
| Download<br/> | Microsoft Virtual Server 2005 R2 SP1 Update onWindows Server 2008orWindows Server 2003<br/> |
| Header<br/>   | <dl> <dt>VsComInterfaces.h</dt> </dl>      |



## See also

<dl> <dt>

[**IVMGuestOS2**](ivmguestos2.md)
</dt> <dt>

[**IVMGuestOS::SetParameter**](ivmguestos-setparameter.md)
</dt> </dl>

 

 




