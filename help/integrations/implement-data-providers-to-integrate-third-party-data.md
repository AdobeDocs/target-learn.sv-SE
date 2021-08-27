---
title: Implementera dataleverantörer för att integrera data från tredje part
description: Den här självstudien innehåller implementeringsinformation och exempel på hur du kan använda funktionen Adobe Target Data Providers för att hämta data från tredjepartsleverantörer och skicka dem i Target-begäran.
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
exl-id: fcf6d1a8-e2a7-41ce-9c1c-02985b7afb5a
source-git-commit: d1517f0763290eb61a9e4eef4f2eb215a9cdd667
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Implementera [!UICONTROL Data Providers] för att integrera data från tredje part i Adobe Target

Implementeringsinformation och exempel på hur du använder funktionen Adobe Target [!UICONTROL Data Providers] för att hämta data från tredjepartsdataleverantörer och skicka dem i Target-begäran.

>[!NOTE]
>
>[!UICONTROL Data Providers] kräver  `at.js` 1.3 eller högre

## Implementera de grundläggande komponenterna i Data Providers

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

En snabb översikt över de grundläggande komponenterna i en `dataProvider` och hur du får koden i rätt ordning.\
Ett fungerande exempel med koden som används i videon finns här:
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Integrera med ett tredjeparts-API

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

Ett mer realistiskt exempel på integrering av ett väder-API.\
Ett fungerande exempel med koden som används i videon finns här:
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Integrera med flera leverantörer

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

Så här lägger du in data från flera leverantörer i din globala [!DNL Target]-begäran.\
Ett fungerande exempel med koden som används i videon finns här:
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Minimera sidladdningens påverkan

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Minimera påverkan på sidinläsningstiden genom att lagra data i ett sessionslagringsobjekt. Du kan också skicka värdena som profilparametrar med prefixet `profile.` och bara skicka dem i sessionens första [!DNL Target]-begäran. Du kan dock bara skicka femtio profilparametrar per begäran.

Ett fungerande exempel med koden som används i videon finns här: [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Stödmaterial

* [Använd Data Providers med Adobe Target](use-data-providers-to-integrate-third-party-data.md)

* [Dokumentation för dataleverantörer](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en#data-providers)
