---
title: Adobe Target API - översikt
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations innehåller en dedikerad uppsättning API:er som gör att du kan hantera din katalog med rekommenderade produkter och/eller innehåll. hantera era rekommendationsalgoritmer och -kampanjer, och leverera rekommendationer i JSON-, HTML- och XML-objekt som ska visas i webben, mobiler, e-post, IOT och andra kanaler.
kt: null
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: b66dbae616c9559f5d1b7bbedf2d9b383840973b
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# Adobe Target API - översikt

Adobe Target API:er kan grupperas efter typ.

| API-typ | Vad du kan göra | Hämta länk |
| --- | --- | --- |
| Administratör | Skapa, ändra och ta bort aktiviteter, målgrupper, erbjudanden och andra objekt (inklusive [!DNL Recommendations] enheter, kriterier, design osv.). API: [!DNL Recommendations] erna är en typ av admin-API.) | <UL><li>[Target Admin API Postman Collection](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Recommendations API Postman Collection](https://developers.adobetarget.com/api/recommendations/#section/Postman)</li></ul> |
| Leverans | Hämta optimerat och personaliserat innehåll från [!DNL Target] för leverans till slutanvändare. | [Target Delivery API Postman Collection](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection) |
| Rapportering | Exportera aktivitetsresultat och andra rapportresultat. | Rapporterings-API:er ingår i [Target Admin API Postman-samlingen](https://developers.adobetarget.com/api/#admin-postman-collection). |
| Profil | Hämta och ändra användarprofiler som lagras i Adobe Target. | [Målprofil-API Postman Collection](https://developers.adobetarget.com/api/#profiles) |

Observera skillnaden mellan **admin-API:er** (inklusive [!DNL Recommendations] API:er), som gör att du kan konfigurera olika aspekter av Adobe Target jämfört med **leverans-API:er**, som du kan använda för att hämta innehåll. Admin-API:er kräver autentisering, men leverans-API:er gör det inte.

Om du vill använda Adobe Target Admin API:er måste du först konfigurera autentiseringen med Adobe I/O.

[Nästa Konfigurera autentisering >](configure-io-target-integration.md)
