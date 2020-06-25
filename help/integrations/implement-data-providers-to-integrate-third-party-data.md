---
title: Implementera dataleverantörer för att integrera data från tredje part i Adobe Target
seo-title: Implementera dataleverantörer för att integrera data från tredje part i Adobe Target
description: Implementeringsinformation och exempel på hur du använder funktionen Adobe Target Data Providers för att hämta data från tredjepartsleverantörer och skicka dem i Target-begäran.
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---


# Implementera [!UICONTROL Data Providers] data från tredje part i Adobe Target

Implementeringsinformation och exempel på hur du kan använda Adobe Target-funktionen för att hämta data från tredjepartsleverantörer av data och skicka dem i Target-begäran. [!UICONTROL Data Providers]

>[!NOTE]
>
>[!UICONTROL Data Providers] kräver `at.js` 1.3 eller högre

## Implementera de grundläggande komponenterna i Data Providers

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

En snabb översikt av grundkomponenterna i en `dataProvider` och hur du får koden i rätt ordning.\
Ett fungerande exempel med koden som används i videon finns här:
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Integrera med ett tredjeparts-API

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

Ett mer realistiskt exempel: att integrera ett väder-API.\
Ett fungerande exempel med koden som används i videon finns här:
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Integrera med flera leverantörer

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

Hur man lägger in data från olika leverantörer i en global [!DNL Target] förfrågan.\
Ett fungerande exempel med koden som används i videon finns här:
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Minimera sidladdningens påverkan

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Minimera påverkan på sidinläsningstiden genom att lagra data i ett sessionslagringsobjekt. Du kan också skicka värdena som profilparametrar med `profile.` prefixet och bara skicka dem i sessionens första [!DNL Target] begäran. Du kan dock bara skicka femtio profilparametrar per begäran.

Ett fungerande exempel med koden som används i videon finns här: [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Stödmaterial

* [Använd Data Providers med Adobe Target](use-data-providers-to-integrate-third-party-data.md)

* [Dokumentation för dataleverantörer](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)