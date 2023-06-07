---
title: Implementera at.js 2.0 i ett enkelsidigt program (SPA)
description: Adobe Target at.js 2.0 har många funktioner som gör det möjligt för ditt företag att utföra personalisering på nästa generations klienttekniker. Följ de här stegen för att implementera at.js 2.0 i ett enkelsidigt program (SPA).
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 955f0571-5791-4dbb-9931-e6d5c8bb42a7
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# Implementera Adobe Target at.js 2.0 i ett enkelsidigt program (SPA)

Adobe Target `at.js` 2.0 har många funktioner som gör det möjligt för ert företag att genomföra personalisering på nästa generations klienttekniker. Den här versionen fokuserar på uppgradering `at.js` att ha harmonisk interaktion med applikationer för en enda sida (SPA).

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## Implementera at.js 2.0 i en SPA

* Implementera `at.js` 2.0 i &lt;head> av ditt Single Page-program.
* Implementera `adobe.target.triggerView()` fungerar när du visar ändringar i SPA. Du kan använda olika tekniker för att göra detta, till exempel avlyssna ändringar i URL-hashen, avlyssna anpassade händelser som utlöses av SPA eller bädda in `triggerView()` direkt i programmet. Du bör välja det alternativ som fungerar bäst för ditt specifika enkelsidiga program.
* Vynamnet är den första parametern i `triggerView()` funktion. Använd enkla, tydliga och unika namn för att göra dem enkla att välja i Target visuella upplevelsedisposition.
* Du kan utlösa vyer som ändras i små vyer, liksom i andra sammanhang än SPA, t.ex. halvvägs nedåt och en oändlig rullningssida.
* `at.js` 2.0 och `triggerView()` kan implementeras via en tagghanteringslösning, som Adobe Experience Platform Launch.

## at.js 2.0 Begränsningar

Observera följande begränsningar i `at.js` 2.0 före uppgradering:

* Spårning av korsdomän stöds inte i `at.js` 2.0
* Parametrarna mboxOverride.browserIp och mboxSession URL stöds inte i `at.js` 2.0
* De äldre funktionerna mboxCreate, mboxDefine, mboxUpdate är inaktuella i `at.js` 2.0. Standardinnehåll visas och inga nätverksbegäranden görs.

## Bibliotekets sidfotskod som används i videon

Koden nedan har lagts till i delen Library Footer i `at.js` under videon. Det aktiveras när appen först läses in och sedan när någon hash-ändring görs i appen. Den använder en rensad version av hash som visningsnamn och&quot;home&quot; när hash-filen är tom. Observera att koden söker efter texten&quot;reagerar/&quot; i URL:en för att identifiera SPA, som troligen behöver uppdateras på webbplatsen. Tänk också på att det kan vara lämpligare för din SPA att avfyra `triggerView()` av anpassade händelser eller genom att bädda in koden direkt i appen.

```javascript
function sanitizeViewName(viewName) {
  if (viewName.startsWith('#')) {
    viewName = viewName.substr(1);
  }
  if (viewName.startsWith('/')) {
    viewName = viewName.substr(1);
  }
  return viewName;
}
function triggerView(viewName) {
  viewName = sanitizeViewName(viewName) || 'home';
  // Validate if the Target Libraries are available on your website
  if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
    adobe.target.triggerView(viewName);
    console.log('AT: View triggered on page load: '+viewName)
  }
}
//fire triggerView when the SPA loads and when the hash changes in the SPA
if(window.location.pathname.indexOf('react/') >-1){
    triggerView(location.hash);
}
window.onhashchange = function() {
    if(window.location.pathname.indexOf('react/') >-1){
        triggerView(location.hash);
    }
}
```

## Ytterligare resurser

* [Understanding How at.js 2.0 Works (Architecture Diagrams)](understanding-how-atjs-20-works.md)
* [Använda Adobe Target Visual Experience Composer för enkelsidiga program (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
