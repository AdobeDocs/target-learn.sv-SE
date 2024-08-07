---
title: Använda Data Providers för att integrera data från tredje part
description: I den här självstudien introduceras användare för Data Providers. Lär dig använda Data Providers för att enkelt skicka data från tredje part till Adobe Target.
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt: null
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---

# Använd Data Providers för att integrera data från tredje part i Adobe Target

[!UICONTROL Data Providers] är en funktion som gör att du enkelt kan skicka data från tredje part till Target.  En tredje part kan vara en vädertjänst, en datahanteringsplattform eller till och med en egen webbtjänst. Sedan kan ni använda dessa data för att skapa målgrupper, målinnehåll och berika besökarprofilen.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## Använda Data Providers

1. Implementeringsexperten lägger till kod före at.js (eller i bibliotekshuvudet i at.js) som gör API-anropet till tredje part, tolkar svaret och anger med namn/värde-par från svaret som ska skickas till [!DNL Target].
1. at.js hanterar flimmer och inkluderar namn/värde-par som anpassade parametrar i den globala Target-begäran.
1. Marketer bygger målgrupper i gränssnittet [!DNL Target] baserat på dessa anpassade parametrar.
1. Marknadsförare använder dessa målgrupper för att inrikta sig på upplevelser, aktiviteter och mätvärden samt för att rapportera målgrupper.

>[!NOTE]
>
>[!UICONTROL Data Providers] kräver at.js 1.3 eller högre

## Stödmaterial

* [Implementera Data Providers i at.js och Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
