---
layout: post
title:  "Skapa ett WoW AddOn"
date:   2022-04-18 14:53 +0200
categories: wow
---

## Att skapa ett addon är enklare än vad man tror.
Folk som vet hur man gör ett macro, kan egentligen grunden till & har en någorlunda aning om hur WoW's LUA integration fungerar.
I denna posten så tänkte jag diskutera lite om hur man faktiskt kan göra ett addon med "low - effort / knowledge".

Till att börja med, så vill jag också påpeka om att vissa funktioner är låsta/säkrade, vilket gör att du inte kan anropa/använda vissa
funktioner.

I denna posten vill jag också visa hur man på enkelt sätt kan hooka scripten till att göra olika grejer.

## Varje AddOn måste ha en .TOC fil.
Yes, och det är för att berätta för WoW, vad det är för addon som gör vad.
Ett exempel på en **.toc** fil finns nedan.
Följande är: `addon.toc`
```
## Interface: 90200 <--- nuvarande version av spelet
## Version: 1.0.0 <--- vilken version du definerar ditt addon på.
## Title: MittAddon <--- addon titel, vad addonet heter.
## Notes: Simpelt addon <--- addon beskrivningen.
## Author: Guwi <--- vem det är som har gjort addonet.

addon.lua <--- Själva addonet.
```

## Frame
**Se till att "addon.lua" ligger i samma map som "addon.toc"**
Alla funktioner som SKALL ha en användning MED event, ska alltid ha en Frame, då det är genom våran egna frame vi kommer ställa in dem olika eventen.
Ett exempel här nedanför.
```lua
local frame = CreateFrame("Frame", "NamnPåMinFrame") -- CreateFrame har 5st argument, frame typ, namn, parent, template och id, varav 1 MÅSTE finnas med, vilket är frame typ.
```

## Registrera event
Ett event som skall registreras kan se ut något såhär.
```lua
function frame:OnEvent(event, ...)
    self[event](self,event,...) -- Laddar in alla registrerade event.
end

function frame:ADDON_LOADED()
    print("hej från mitt addon.") -- Printar ut texten "hej från mitt addon." till chatten.
end

frame:RegisterEvent("ADDON_LOADED")
frame:SetScript("OnEvent", frame.OnEvent)
```

**Jag kommer uppdatera posten, när det finns något annat jag har hittat.**