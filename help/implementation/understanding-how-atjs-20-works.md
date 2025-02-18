---
title: Hur fungerar at.js 2.0?
description: Se hur at.js 2.0 förbättrar Adobe Target stöd för SPA (single page applications) och kan integreras med andra Experience Cloud-lösningar.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 7f037665-88a7-469c-8df5-c82cb0f65382
source-git-commit: fcd2273ba373dc2b3bc59a77f1925cdb7b2ed3ee
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Se hur Adobe Target at.js 2.0 fungerar

`at.js` 2.0 förbättrar Adobe Target stöd för SPA (Single page applications) och är integrerat med andra Experience Cloud-lösningar. I den här videon och tillhörande diagram förklaras hur allt hänger ihop.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Arkitekturdiagram

Beteendet ![at.js 2.0 vid sidinläsning](assets/pageload.png)

1. Anropet returnerar Experience Cloud ID (ECID). Om användaren är autentiserad synkroniseras kundens ID med ett annat samtal.

1. `at.js`-biblioteket läses in synkront och döljer dokumentinnehållet (`at.js` kan också läsas in asynkront med ett valfritt fördolt fragment implementerat på sidan).

1. Begäran om sidinläsning omfattar alla konfigurerade parametrar, ECID, SDID och kund-ID.

1. Profilskript körs och matas in i [!UICONTROL Profile Store]. Store begär kvalificerade målgrupper från [!UICONTROL Audience Library] (t.ex. målgrupper som delas från [!DNL Analytics], Audience Manager osv.). [!UICONTROL Customer Attributes] skickas till [!UICONTROL Profile Store] i en gruppbearbetning.
1. Baserat på URL, begäranparametrar och profildata avgör [!DNL Target] vilka aktiviteter och upplevelser som ska returneras till besökaren för den aktuella sidan och framtida vyer

1. Målinriktat innehåll som skickas tillbaka till sidan, eventuellt med profilvärden för ytterligare personalisering.

   Målinriktat innehåll på den aktuella sidan visas så snabbt som möjligt utan att du behöver flimra standardinnehållet.

   Målanpassat innehåll för framtida vyer av ett enkelsidigt program cachelagras i webbläsaren så att det kan tillämpas direkt utan ett extra serveranrop när vyerna aktiveras. (Se nästa diagram för `triggerView()`-beteende).

1. [!DNL Analytics] data har skickats från sidan till [!UICONTROL Data Collection]-servrarna
1. [!DNL Target] data matchas mot analysdata via SDID och bearbetas till rapportlagringen [!DNL Analytics]. [!DNL Analytics] data kan sedan visas i både [!DNL Analytics] och [!DNL Target] via A4T-rapporter.

Beteendet ![ at.js 2.0 när funktionen triggerView() används](assets/triggerview.png)

1. `adobe.target.triggerView()` anropas i enkelsidigt program
1. Målinnehåll för vyn läses från cachen

1. Målanpassat innehåll visas så snabbt som möjligt utan att man behöver flimra standardinnehållet

1. Meddelandebegäran skickas till [!DNL Target] [!UICONTROL Profile Store] för att räkna besökaren i aktiviteten och öka måtten
1. [!DNL Analytics] data skickas från SPA till [!UICONTROL Data Collection]-servrarna

1. [!DNL Target] data skickas från [!DNL Target]-serverdelen till [!UICONTROL Data Collection]-servrarna. [!DNL Target]-data matchas mot [!DNL Analytics]-data via SDID och bearbetas till rapportlagringen [!DNL Analytics]. [!DNL Analytics] data kan sedan visas i både [!DNL Analytics] och [!DNL Target] via A4T-rapporter.

## Ytterligare resurser

* [Implementera at.js 2.0 i ett enkelsidigt program](implement-atjs-20-in-a-single-page-application.md)
* [Använda Adobe Target Visual Experience Composer för Single Page-program (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
