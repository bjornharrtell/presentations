---
marp: true
theme: default
style: |
  section {
    font-size: 1.75em;
  }
---

<!-- class: invert -->

# 3FB / KAS arkitektur

---

## Foranalys

"I en ny it-understøttelse anbefales det, at it-arkitekturen klart adskiller det pågældende systems registerkerne, der skal håndtere systemets data på en sikker måde, dels fra den funktionalitet, som et fagsystem inden for det pågældende område skal levere – dels fra systemets udstilling af data."

---

## De gamla systemer har en räkke brister (fra start)

* Monoliter
* Ikke dokumenterat API
* Ingen möjlighet att integrera eller skifta ut en del

---

## Det nya system vara modulärt (till viss del)

* Ett antal (stora) "domäner" / "moduler" / "komponenter" där det ger mening
* Basis/felles (både frontend och backed)
* Register-specifikt
* Integration
* Dokumenterat REST API
* Tilsynsklient?

---

## Same but better (looking)
