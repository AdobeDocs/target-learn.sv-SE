---
title: Så här använder du svarstoken och anpassade at.js-händelser
description: Lär dig hur du använder responstoken och anpassade at.js-händelser för att dela profilinformation från Target till tredjepartssystem.
role: Developer
level: Experienced
topic: Personalization, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: d6ce5367-a453-4e6c-8545-9fa676977f04
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Använd svarstoken och anpassade at.js-händelser med Adobe Target

Svarstoken och `at.js` Med anpassade händelser kan du dela profilinformation från [!DNL Target] till system från tredje part. Alla objekt i [!DNL Target] besökarprofil, inklusive anpassade profilattribut, geografisk information, aktivitetsinformation och inbyggda profiler kan läggas till i [!DNL Target] -svar där du kan använda anpassad JavaScript för att integrera med tredje part.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## Så här använder du Response Tokens och at.js anpassade händelser

1. Ta reda på vilka data du behöver från [!DNL Target]
1. Aktivera svarstoken för de data som du behöver genom att växla till på skärmen Inställningar->Svarstoken
1. Ta reda på vilken händelseavlyssnare du behöver använda
1. Skriv det JavaScript som behövs för att avlyssna Adobe Target-händelsen, läsa svarstoken och göra vad du behöver för integreringen
1. Distribuera händelseavlyssnaren JavaScript med en anpassad kodsåtgärd i Launch efter åtgärden Load Target eller lägg till den i delen Library Footer i at.js på installationsskärmen > Implementeringsskärmen och spara en ny at.js-fil
1. Kvalitetssäkring och publicera integreringen

## Ytterligare resurser

* [Använda Experience Cloud Debugger med Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Dokumentation för svarstoken](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)
* [Använda Data Providers i Adobe Target](use-data-providers-to-integrate-third-party-data.md)
