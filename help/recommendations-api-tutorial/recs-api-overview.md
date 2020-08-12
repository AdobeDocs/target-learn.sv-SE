---
title: Adobe Recommendations API - översikt
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations innehåller en dedikerad uppsättning API:er som gör att du kan hantera din katalog med rekommenderade produkter och/eller innehåll. hantera era rekommendationsalgoritmer och -kampanjer, och leverera rekommendationer i JSON-, HTML- och XML-objekt som ska visas i webben, mobiler, e-post, IOT och andra kanaler.
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 78b30bc0018527f9d8b2a5b50edee86e877d14c7
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Adobe Recommendations API - översikt

API:er som är relevanta för [!DNL Recommendations] inkluderar [admin-API:er](https://docs.adobe.com/content/help/en/target-learn/apis/api-overview.md) som gör att du kan:

* Hantera din katalog med rekommenderade produkter eller innehåll
* Hantera dina [!DNL Recommendations] algoritmer och aktiviteter

Med [!DNL Target] leverans-API [](https://docs.adobe.com/content/help/en/target-learn/apis/api-overview.md) med Recommendations kan man också

* Hämta rekommendationer i JSON-, HTML- eller XML-objekt så att de kan visas i webben, mobiler, e-post, sakernas internet (IOT) och andra kanaler.

## Beskrivning av självstudiekurs

I den här självstudiekursen får utvecklare hjälp med praktiska övningar där API:erna [!DNL Recommendations] används för att konfigurera och hantera [!DNL Recommendations] kataloger och anpassade villkor, samt att använda leverans-API:t för att hämta rekommendationsinnehåll. I slutet av den här självstudiekursen kan du:

* Konfigurera och hantera entiteter med Recommendations API
* Konfigurera och hantera anpassade villkor med Recommendations API
* Förstå hur du använder Recommendations med leverans-API:t för att använda rekommendationer i andra enheter än HTML

## Målgrupp

Den här självstudiekursen är avsedd för utvecklare som inte använder Target API:er eller Recommendations API:er.

## Krav

Om du vill använda API:erna för måladministratörer måste du konfigurera [Adobe-autentisering](../apis/configure-io-target-integration.md). Kontrollera att du har konfigurerat den här innan du börjar med den här självstudiekursen.

## Resurser

Observera följande resurser som är nödvändiga för att du ska kunna förstå den här självstudiekursen och kunna följa den ordentligt:

| Resurs | Detaljer |
| --- | --- |
| Postman | Skaffa [Postman-appen](https://www.postman.com/downloads/) för ditt operativsystem. Postman Basic är kostnadsfritt när man skapar konto. Även om det inte krävs för att använda Adobe Target API:er i allmänhet, underlättar Postman API-arbetsflödena, och Adobe Target tillhandahåller flera Postman-samlingar som hjälper till att köra API:erna och lära sig hur de fungerar. Resten av den här självstudiekursen förutsätter att Postman har praktiska kunskaper. Om du behöver hjälp kan du läsa [Postmans dokumentation](https://learning.getpostman.com/). |
| Referenser | Du bör känna till följande resurser under resten av kursen:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Adobe I/O-dokumentation](https://developers.adobetarget.com/api/#introduction)</li><li>[Recommendations API-dokumentation](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Nästa&quot;Hantera din Recommendations-katalog&quot; >](manage-catalog.md)