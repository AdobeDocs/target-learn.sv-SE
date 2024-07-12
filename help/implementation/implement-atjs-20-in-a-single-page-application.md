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
source-wordcount: '408'
ht-degree: 0%

---

# Implementera Adobe Target at.js 2.0 i ett enkelsidigt program (SPA)

Adobe Target `at.js` 2.0 innehåller funktionsrika uppsättningar som gör det möjligt för ditt företag att utföra personalisering på nästa generations klienttekniker. Den här versionen är inriktad på att uppgradera `at.js` för att få harmoniska interaktioner med program för en sida (SPA).

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## Implementera at.js 2.0 i en SPA

* Implementera `at.js` 2.0 i &lt;head> för Single Page-programmet.
* Implementera funktionen `adobe.target.triggerView()` när du visar ändringar i SPA. Du kan använda olika tekniker för att göra detta, t.ex. avlyssna ändringar i URL-hash, avlyssna anpassade händelser som utlösts av din SPA eller bädda in `triggerView()`-koden direkt i ditt program. Du bör välja det alternativ som fungerar bäst för ditt specifika enkelsidiga program.
* Vynamnet är den första parametern i funktionen `triggerView()`. Använd enkla, tydliga och unika namn för att göra dem enkla att välja i Target visuella upplevelsedisposition.
* Du kan utlösa vyer som ändras i små vyer, liksom i andra sammanhang än SPA, t.ex. halvvägs nedåt och en oändlig bläddringssida.
* `at.js` 2.0 och `triggerView()` kan implementeras via en tagghanteringslösning, till exempel Adobe Experience Platform Launch.

## at.js 2.0 Begränsningar

Tänk på följande begränsningar för `at.js` 2.0 innan du uppgraderar:

* Spårning av korsdomän stöds inte i `at.js` 2.0
* Parametrarna mboxOverride.browserIp och mboxSession URL stöds inte i `at.js` 2.0
* De äldre funktionerna mboxCreate, mboxDefine, mboxUpdate är inaktuella i `at.js` 2.0. Standardinnehåll visas och inga nätverksbegäranden görs.

## Bibliotekets sidfotskod som används i videon

Koden nedan lades till i delen Library Footer i biblioteket `at.js` under videon. Det aktiveras när appen först läses in och sedan när någon hash-ändring görs i appen. Den använder en rensad version av hash som visningsnamn och&quot;home&quot; när hash-filen är tom. Observera att koden söker efter texten&quot;reagerar/&quot; i URL:en för att identifiera SPA, som troligen behöver uppdateras på webbplatsen. Kom ihåg att det kan vara lämpligare för din SPA att avaktivera `triggerView()` av anpassade händelser eller genom att bädda in koden direkt i din app.

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

* [Förstå hur at.js 2.0 fungerar (arkitekturdiagram)](understanding-how-atjs-20-works.md)
* [Använda Adobe Target Visual Experience Composer för enkelsidiga program (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
