# Kamgo FB Sourcing (KGFBS) – Automatizovaný Scraping a Kategorizácia

<p align="center">
  <img src="image.png" alt="Architektúra riešenia n8n" width="100%">
</p>

## 📋 Prehľad projektu
[cite_start]Tento repozitár obsahuje návrh a proof-of-concept systému pre subprojekt **Kamgo (KGFBS)**[cite: 3]. [cite_start]Cieľom systému je zabezpečiť prísun vytvorených alebo upravených podujatí publikovaných na definovaných FB stránkach[cite: 6]. [cite_start]Systém automatizuje zber dát, ich inteligentnú kategorizáciu pomocou AI a distribúciu cez Kamgo API[cite: 11, 15].

## 🏗️ Architektúra riešenia (n8n Workflow)
Riešenie je postavené na platforme **n8n**, ktorá zabezpečuje orchestráciu celého procesu. [cite_start]Systém je navrhnutý s prioritou na **nákladovú efektivitu (cost-efficiency)**[cite: 13].

### Kľúčové fázy procesu:
1.  [cite_start]**Zber zdrojov:** Načítanie zoznamu 4 000 sledovaných subjektov z API (https://podujatia.relaxos.sk/api/subjects) s využitím autorizačného tokenu[cite: 19, 21].
2.  [cite_start]**Inkrementálny scraping (Lightweight Check):** * Systém najprv kontroluje unikátne `fbId` a čas začiatku `startAt`[cite: 31, 44].
    * [cite_start]Plnohodnotný scraping sa spustí len vtedy, ak je zistená zmena alebo nové podujatie, čo výrazne šetrí náklady na scraping služby[cite: 13].
3.  [cite_start]**AI Kategorizácia:** * Zozbierané dáta (názov, popis, FB tagy) sú spracované pomocou AI[cite: 11].
    * [cite_start]AI navrhne zaradenie do stromu kategórií Kamgo (napr. *Pre deti, Mládež, Hudba, Pohyb a šport...*)[cite: 9].
4.  [cite_start]**Human-in-the-loop:** * Proces kategorizácie zahŕňa spätnú väzbu od človeka[cite: 14].
    * [cite_start]Systém sa učí z ľudských vstupov pre neustále zlepšovanie presnosti[cite: 14].

## 🛠️ Použité technológie
* **n8n:** Hlavný nástroj pre automatizáciu a prepojenie služieb.
* **Python:** Skripty pre logiku porovnávania duplicít a validáciu polí.
* **OpenAI API:** Kategorizácia podujatí na základe textovej analýzy.
* **PostgreSQL:** Databáza pre uchovávanie štruktúrovaných dát o podujatiach.

## 🚀 Dátový model (Fields Mapping)
[cite_start]Systém spracováva všetky povinné a voliteľné atribúty podľa špecifikácie[cite: 25]:
* [cite_start]**Povinné:** `fbId`, `fbUrl`, `name`, `city`, `startAt`[cite: 31, 32, 33, 39, 44].
* [cite_start]**Doplnkové:** `description`, `placeName`, `street`, `imageUrl`, `category`, `ticketUrl`[cite: 35, 37, 41, 49, 51, 53].

---
*Vypracované ako technické riešenie pre výberové konanie Kamgo (KGFBS).*
