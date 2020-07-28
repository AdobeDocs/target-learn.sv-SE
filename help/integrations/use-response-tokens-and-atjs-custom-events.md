---
title: Använd svarstoken och anpassade at.js-händelser med Adobe Target
seo-title: Använd svarstoken och anpassade at.js-händelser med Adobe Target
description: Med responstoken och anpassade at.js-händelser kan du dela profilinformation från Target till tredjepartssystem. Alla objekt i Target besökarprofil, inklusive anpassade profilattribut, geografisk information, aktivitetsinformation och inbyggda profiler, kan läggas till i Target-svaret där du kan använda anpassad JavaScript för att integrera med tredje part.
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# Använd svarstoken och anpassade at.js-händelser med Adobe Target

Med svarstoken och `at.js` anpassade händelser kan du dela profilinformation från [!DNL Target] till tredjepartssystem. Alla objekt i [!DNL Target] besökarprofilen, inklusive anpassade profilattribut, geografisk information, aktivitetsinformation och inbyggda profiler, kan läggas till i [!DNL Target] svaret där du kan använda anpassad JavaScript för att integrera med tredje part.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## Så här använder du Response Tokens och at.js anpassade händelser

1. Ta reda på vilka data du behöver från [!DNL Target]
1. Aktivera svarstoken för de data som du behöver genom att växla till på skärmen Inställningar->Svarstoken
1. Ta reda på vilken händelseavlyssnare du behöver använda
1. Skriv det JavaScript som behövs för att avlyssna händelsen Adobe Target, läsa svarstoken och göra vad du behöver för integreringen
1. Distribuera händelseavlyssnaren JavaScript med en anpassad kodsåtgärd i Launch efter åtgärden Load Target eller lägg till den i delen Library Footer i at.js på installationsskärmen > Implementeringsskärmen och spara en ny at.js-fil
1. Kvalitetssäkring och publicera integreringen

## Ytterligare resurser

* [Använd Experience Cloud Debugger med Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Dokumentation för svarstoken](https://docs.adobe.com/help/en/target/using/administer/response-tokens.html)
* [Anpassad händelsedokumentation för At.js](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/atjs-custom-events.html)
* [Använda Data Providers i Adobe Target](use-data-providers-to-integrate-third-party-data.md)