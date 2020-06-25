---
title: Så här fungerar Adobe Target.js 2.0
seo-title: Så här fungerar Adobe Target.js 2.0
description: at.js 2.0 har förbättrat Adobe Target stöd för SPA (single page applications) och kan integreras med andra Experience Cloud-lösningar. I den här videon och tillhörande diagram förklaras hur allt hänger ihop.
audience: developer
difficulty: 3
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---


# Så här fungerar Adobe Target.js 2.0

`at.js` 2.0 har förbättrat Adobe Target stöd för SPA (single page applications) och är integrerat med andra Experience Cloud-lösningar. I den här videon och tillhörande diagram förklaras hur allt hänger ihop.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Arkitekturdiagram

![at.js 2.0-beteende vid sidinläsning](assets/pageload.png)

1. Anropet returnerar Experience Cloud-ID (ECID). Om användaren är autentiserad synkroniseras kundens ID med ett annat samtal.

1. `at.js` biblioteket läses in synkront och döljer dokumentets brödtext (`at.js` kan också läsas in asynkront med ett valfritt fördolt fragment som implementeras på sidan).

1. Begäran om sidinläsning omfattar alla konfigurerade parametrar, ECID, SDID och kund-ID.

1. Profilskript körs och matas in i [!UICONTROL Profile Store]. Store begär kvalificerade målgrupper från [!UICONTROL Audience Library] (t.ex. målgrupper som delas från [!DNL Analytics], Audience Manager). [!UICONTROL Customer Attributes] skickas till [!UICONTROL Profile Store] i en gruppbearbetning.
1. Baserat på URL-adress, begärandeparametrar och profildata, bestämmer [!DNL Target] vilka aktiviteter och upplevelser som ska returneras till besökaren för den aktuella sidan och framtida vyer

1. Målinriktat innehåll som skickas tillbaka till sidan, eventuellt med profilvärden för ytterligare personalisering.

   Målinriktat innehåll på den aktuella sidan visas så snabbt som möjligt utan att du behöver flimra standardinnehållet.

   Målanpassat innehåll för framtida vyer av ett enkelsidigt program cachelagras i webbläsaren så att det kan tillämpas direkt utan ett extra serveranrop när vyerna aktiveras. (Se nästa diagram för `triggerView()` beteendet).

1. [!DNL Analytics] data som skickas från sidan till [!UICONTROL Data Collection] servrarna
1. [!DNL Target] data matchas mot Analytics-data via SDID och bearbetas till [!DNL Analytics] rapportlagringen. [!DNL Analytics] data kan sedan visas både [!DNL Analytics] och [!DNL Target] via A4T-rapporter.

![at.js 2.0-beteende när funktionen triggerView() används](assets/triggerview.png)

1. `adobe.target.triggerView()` anropas i enkelsidigt program
1. Målinnehåll för vyn läses från cachen

1. Målanpassat innehåll visas så snabbt som möjligt utan att man behöver flimra standardinnehållet

1. Begäran om meddelande skickas till användaren [!DNL Target] [!UICONTROL Profile Store] för att räkna besökaren i aktiviteten och öka mätvärdena
1. [!DNL Analytics] data skickas från SPA till [!UICONTROL Data Collection] servrarna

1. [!DNL Target] data skickas från backend- [!DNL Target] servern till [!UICONTROL Data Collection] servrarna. [!DNL Target] data matchas mot [!DNL Analytics] data via SDID och bearbetas till [!DNL Analytics] rapportlagringen. [!DNL Analytics] data kan sedan visas både [!DNL Analytics] och [!DNL Target] via A4T-rapporter.

## Ytterligare resurser

* [Implementera at.js 2.0 i ett enkelsidigt program](implement-atjs-20-in-a-single-page-application.md)
* [Använd Adobe Target Visual Experience Composer för Single Page-program (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [How at.js Works Documentation](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/at-js/how-atjs-works.html)