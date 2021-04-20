---
title: Vad är Adobe Recommendations API?
description: I den här självstudiekursen får utvecklare hjälp med praktiska övningar där Adobe Target Recommendations-API:er används för att konfigurera och hantera Recommendations-kataloger och anpassade villkor, samt att använda leverans-API:t för att hämta rekommendationsinnehåll.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Adobe Recommendations API - översikt

API:er som är relevanta för [!DNL Recommendations] inkluderar [admin-API:er](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html) som gör att du kan:

* Hantera din katalog med rekommenderade produkter eller innehåll
* Hantera dina [!DNL Recommendations]-algoritmer och -aktiviteter

Med hjälp av [!DNL Target] [leverans-API](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html) med Recommendations kan du även:

* Hämta rekommendationer i JSON-, HTML- eller XML-objekt så att de kan visas i webben, mobiler, e-post, sakernas internet (IOT) och andra kanaler.

## Beskrivning av självstudiekurs

I den här självstudiekursen får utvecklare hjälp med praktiska övningar med hjälp av [!DNL Recommendations]-API:erna för att konfigurera och hantera [!DNL Recommendations]-kataloger och anpassade villkor, samt med hjälp av leverans-API:t för att hämta rekommendationsinnehåll. I slutet av den här självstudiekursen kan du:

* Konfigurera och hantera entiteter med Recommendations API
* Konfigurera och hantera anpassade villkor med Recommendations API
* Förstå hur du använder Recommendations med leverans-API:t för att använda rekommendationer i andra enheter än HTML

## Målgrupp

Den här självstudiekursen är avsedd för utvecklare som inte använder Target API:er eller Recommendations API:er.

## Krav

För att använda API:erna för måladministratörer krävs [autentiseringsinställningar för Adobe](../apis/configure-io-target-integration.md). Kontrollera att du har konfigurerat den här innan du börjar med den här självstudiekursen.

## Resurser

Observera följande resurser som är nödvändiga för att du ska kunna förstå den här självstudiekursen och kunna följa den ordentligt:

| Resurs | Detaljer |
| --- | --- |
| Postman | Hämta [Postman-appen](https://www.postman.com/downloads/) för ditt operativsystem. Postman Basic är kostnadsfritt när man skapar konto. Även om det inte krävs för att använda Adobe Target API:er i allmänhet, underlättar Postman API-arbetsflödena, och Adobe Target tillhandahåller flera Postman-samlingar som hjälper till att köra API:erna och lära sig hur de fungerar. Resten av den här självstudiekursen förutsätter att Postman har praktiska kunskaper. Om du behöver hjälp kan du läsa [Postman-dokumentationen](https://learning.getpostman.com/). |
| Referenser | Du bör känna till följande resurser under resten av kursen:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Adobe I/O dokumentation](https://developers.adobetarget.com/api/#introduction)</li><li>[Recommendations API-dokumentation](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Nästa&quot;Hantera din Recommendations-katalog&quot; >](manage-catalog.md)
