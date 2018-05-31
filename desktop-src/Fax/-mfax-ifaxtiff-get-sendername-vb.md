---
Description: Retrieves the SenderName property for a FaxTiff object. The SenderName property is a null-terminated string that contains the name of the user who queued the fax transmission.
ms.assetid: 2dad9af7-073b-4434-88db-d0b32b43b972
title: FaxTiff.SenderName property
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
---

# FaxTiff.SenderName property

Retrieves the **SenderName** property for a [FaxTiff](-mfax-faxtiff.md) object. The **SenderName** property is a null-terminated string that contains the name of the user who queued the fax transmission.

This property is read-only.

## Syntax


```VB
Property SenderName As String
```



## Property value

A **String** that receives the name of the sender who initiated the fax transmission.

## Remarks

A fax client application must set the [**Image**](-mfax-ifaxtiff-get-image-vb.md) property before retrieving another property for a [FaxTiff](-mfax-faxtiff.md) object.

The **SenderName** property has meaning only for outbound fax transmissions.

The **get\_SenderName** method sets the *pVal* parameter to the name of the sender of the specified fax file, if it is available. If the information is not available, the method returns an "Unavailable".

The **SenderName** property is a string that represents the name of the sender of the specified fax file, if it is available. If the information is not available, **SenderName** is an empty string.

The **get\_SenderName** method allocates the memory required for the buffer pointed to by the *pVal* parameter. The client application must call the [SysFreeString](8f230ee3-5f6e-4cb9-a910-9c90b754dcd3) function to deallocate the resources associated with this parameter. For more information, see [Freeing Fax Resources](-mfax-freeing-fax-resources.md).

## Requirements



|                                     |                                                                                       |
|-------------------------------------|---------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows 2000 Professional \[desktop apps only\]<br/>                            |
| Minimum supported server<br/> | Windows 2000 Server \[desktop apps only\]<br/>                                  |
| Header<br/>                   | <dl> <dt>Faxcom.h</dt> </dl>   |
| DLL<br/>                      | <dl> <dt>Faxcom.dll</dt> </dl> |



## See also

<dl> <dt>

[**FaxTiff**](-mfax-faxtiff-object-visual-basic-.md)
</dt> <dt>

[Fax Service Client API for Windows 2000](-mfax-fax-service-client-api-for-windows-2000.md)
</dt> <dt>

[Fax Service Client API Interfaces](-mfax-fax-service-client-api-interfaces.md)
</dt> <dt>

[**IFaxTiff**](/previous-versions/windows/desktop/api/Faxcom/nn-faxcom-ifaxtiff)
</dt> <dt>

[**Image**](-mfax-ifaxtiff-get-image-vb.md)
</dt> <dt>

[SysFreeString](8f230ee3-5f6e-4cb9-a910-9c90b754dcd3)
</dt> </dl>

 

 



