# Vermo: produkter och två leveransval (2 okt 2026)

Kunden ser en produkt och väljer **Snabb leverans** (EU-partnern Ownprint) eller **Standardleverans** (CN-partnern CJdropshipping). Partnernas namn syns aldrig på sajten. Varje val är en egen Shopify-produkt från respektive app, så ordern går automatiskt till rätt partner.

## Beslut 2 okt (ägarens svar)
- **Presentask och meddelandekort ingår inte.** Ownprint har bara ett allmänt tackkort som kostar €1,50 extra. *Osäkert: Ownprints FAQ säger att ask och kort ingår som standard (se 2 okt, eftermiddag).*
  - Löftet tas bort från sajten och fraktpolicyn.
  - Hälsningen erbjuds i stället som gravyr på baksidan (max 50 tecken, ingår).
- **Tackkortet:** rekommendationen är att inte slå på det vid lanseringen. Det kostar cirka 17 kr per order och är inte personligt. Det prövas senare om data visar att det behövs.
- **CJ:** ingen produkt uppfyllde kraven. Standardleveransen förblir avstängd (ECONOMY_ENABLED=false), och lanseringen sker med endast Snabb leverans.

## Nya produkter 2 okt (skapade via Desktop-prompt 2, publicerade till Lovable av Claude)
| Produkt | Handle | Pris | Variant | Särskilt |
|---|---|---|---|---|
| Namnet | `namnet-snabb-leverans` | 499 | baksida × färg | Ownprints design i **skrivstil** ("Sophia"). Bar 10 × 40 mm. |
| Stjärntecknet | `stjarntecknet-snabb-leverans` | 499 | baksida × färg | Valfältet **"Stjärntecken"** med 12 värden ("Väduren/Aries" …). Bilderna visar Lejonet. **Bara i förhandsvisningen** tills Ownprint svarar, se OWNPRINT-FRAGA.md. |
| Initialen | `initialen-snabb-leverans` | 449 | baksida × färg | Bricka 22 × 39 mm, stor initial i rak antikva |
| Armringen | `armringen-snabb-leverans` | 499 | baksida × färg | Armring 6,5 × 5 cm, mynt 20 mm, dekorativ "A&M"-design i skrivstil |
| Pärlan | `parlan-snabb-leverans` | 699 | baksida (bara Guldfärg) | 18 + 5 cm, pärlor av skalpulver (pärlemor) 6 mm, mynt 20 mm. Inga påståenden om "hypoallergen". |
| Nyckelringen | `nyckelringen-snabb-leverans` | 399 | baksida × färg | Hjärta 20 × 25 mm, design "M♥J" |

**Gemensamt för de nya:**
- Alla ligger i Ownprints fraktprofil, och Sverige har Fri frakt 0 (kontrollerat).
- Inga jämförpriser.
- Fälten är `Front engraving text` (20) och `Back engraving text` (50).
- Den gamla Stjärntecknet (stjärntecknet som variant, 72 varianter, inget namnfält) är arkiverad.

**Bilder:**
- Hjärtat, Familjen, Vår dag och alla nya produkter (utom Pärlan) har bilder i guld, roséguld och silver.
- Klassade 2 okt: asken, kartongen och engelsk text är dolda.
- **Namnets bild 11 visar fel produkt** (en liggande silverbar) och visas aldrig.
- Pärlan: leverantörsfoton i guld. Måttbilden har engelsk text och är dold.
- Pappa fick inga nya silverbilder, men två befintliga visar silver.
- Id:na per färg finns i Lovable-prompten för runda 4 (LOVABLE-PROMPT.md).

**Täckningsbidrag före annons** (se LANSERING.md):
- Namnet, Armringen och Stjärntecknet: ca 180 kr.
- Initialen: ca 145 kr.
- Nyckelringen: ca 105 kr, eller ca 150 kr som extra vara.
- Pärlan: ca 270 kr.
- Inköp enligt Desktop-rapporten: silver €11, guld och roséguld €12, baksida +€3,50.

## Beslut 2 okt, kväll
- **Asken:**
  - Ägarens prov kom i presentask, men asken **lovas inte i text**, varken på sajten eller i policyerna. Ask-bilderna visas inte heller.
  - Kassan och orderbekräftelsen visar fortfarande Shopifys bild 0 (asken), vilket stämmer med verkligheten.
- **Tackkort:** €0,35 per order, betalas av Vermo. Kalkylen är uppdaterad i LANSERING.md.
- **Kassan:** fungerar på vermo.se, testad av ägaren (kort, Klarna, Google Pay). Den fungerar inte i Lovables förhandsvisning, och det är väntat.
- **Sortimentet:**
  - Billigare produkter (399–499 kr) läggs till enligt LANSERING.md och DESKTOP-PROMPT-2.md.
  - Specialprodukterna ligger kvar på 599/699 kr.
  - 399 kr används bara som extravara, inte i annonser.

## Ownprints orderflöde (enligt deras supportsida, 2 okt)
- **Betalning:**
  - Det finns inget sparat kort med automatisk dragning.
  - Varje order granskas och betalas under Orders (kort eller OwnPrint Points). Efter betalningen går den automatiskt till produktion.
  - Faktureringsuppgifter och momsnummer: Settings → Billing.
- **Moms:** säljare i EU med verifierat momsnummer betalar ingen moms. Utan momsnummer tillkommer moms.
- **Stoppade ordrar** ("on hold", t.ex. oklar personalisering): orsaken syns på Orders-sidan.
- **"Enable Personalization"** lägger Ownprints personaliseringsblock i Shopify-temat. Det behövs inte, eftersom temat bara skickar vidare och vermo.se skickar fälten själv. Testordern bekräftar att Ownprint läser dem.
- **Daglig rutin:** betala nya ordrar i Ownprint samma dag. Leveranslöftet (2–5 + 1–10 arbetsdagar) förutsätter det.

## Beslut och fakta 2 okt, eftermiddag
- **Ägaren:**
  - Nej till att byta variantbild i Shopify.
  - Nej till en rabattkod.
  - Ingen provbeställning behövs, eftersom ägaren redan har ett prov i bra skick.
  - **Förlanseringsläget är avstängt för gott** (PRELAUNCH=false). Det slås aldrig på igen.
- **Tillverkare enligt GPSR: Print-on-Demand B.V. (Ownprint).**
  - Ownprints supportsida säger: *"For OwnPrint users, Print-on-Demand B.V. acts as the Economic Operator for all products fulfilled by us."*
  - Uppgifter enligt Ownprint: Groene Hilledijk 211A, 3073 AE Rotterdam, Nederländerna, compliance@print-on-demand-jewelry.eu, +31 85 888 2885.
  - E-postdomänen har MX-poster (Google), så adressen kan ta emot e-post.
  - Sitora är fortfarande säljare.
  - Ownprint nämns på sajten bara i tillverkarraden (ägarens beslut).
- **Förpackning enligt Ownprints FAQ ("What's in the box?"):**
  - Ingår som standard: kraftkartong, skyddsfolie, presentask (egen logga går att lägga till), meddelandekort "tailored to your design", smycket, handgjord vaxkaka, putsduk och tackkort.
  - Ownprints standardtackkort ingår utan kostnad. Eget tackkort kostar €0,35 per order.
  - Ask med egen logga kostar €1,50–1,10 per ask och €30 i startavgift.
  - **Det motsäger beskedet "bara tackkort, €1,50"** under Beslut 2 okt.
  - Ägarens prov avgör: om det kom i ask med kort är ask- och kortbilderna sanna, och löftet kan läggas tillbaka. Fraktpolicyn i Shopify säger redan "Presentask och meddelandekort ingår."
- **Färgbilder:** i Ownprint väljer man i steget Mockups vilka pläteringsfärger som ska få bilder (guld, roséguld, silver). Bara guld valdes, och därför finns inga bilder i silver eller roséguld i Shopify.
  - Ägaren skapar dem i Ownprint, eller laddar ned dem och lägger in dem på produkten i Shopify.
  - Sedan kopplas id:na per färg på sajten. Lovable förbereder det i runda 3.
- **Kassan:** felet "shop.vermo.se avvisade anslutningen" beror på att kassan öppnades inuti Lovables förhandsvisning, som är en ram.
  - Shopify skickar `X-Frame-Options: DENY`.
  - I en vanlig flik går kassalänken till "Utcheckningskassa – Vermo" (HTTP 200, svenska), trots lösenordet på temat.
  - Rättas i Lovable: samma flik på riktiga sajten och ny flik i förhandsvisningen.

## Ownprint-produkterna i Shopify (2 okt, läst via API)
Produkterna är aktiva, säljaren är "Vermo", inga jämförpriser är satta, och alla ligger i Ownprints fraktprofil (92 varianter). Sverige har fortfarande "Fri frakt" för 0. Alla är publicerade till kanalen "Lovable".

| Grupp | Handle | Pris | Variantalternativ |
|---|---|---|---|
| Hjärtat | `hjartat-snabb-leverans` | 599 | back engraving (Without/With back engraving) × plating (Roséguldfärg/Guldfärg/Silverfärg) |
| Familjen | `familjen-snabb-leverans` | 699 | birthstone (January–December) × back engraving × plating (72 varianter) |
| Vår dag | `var-dag-snabb-leverans` | 599 | back engraving × plating |
| Pappa | `pappa-snabb-leverans` | 599 | band (Brown Leather/Black Leather) × back engraving × plating (Guldfärg/Silverfärg) |

**Ownprints fält** (metafältet `ownprint.personalization_fields`):
- `Front engraving text`: max 20 tecken, obligatoriskt.
- `Back engraving text`: max 50 tecken. Visas bara när varianten är "With back engraving".
- Födelsesten, band och baksida väljs via **variant**, inte via fält.
- Det finns **inget fält** för meddelandekort eller typsnitt.

**Konsekvenser för sajten:**
- Varianten måste väljas utifrån färg, baksida (med/utan text), födelsesten och band.
- Teckengränsen är 20 för framsidan och 50 för baksidan.
- Inget val av typsnitt.
- Pappa är **veganskt läder**, inte läder.
- Meddelandekort och presentask ska bara lovas om Ownprints förpackning bekräftar dem.
- Baksidesgravyren kostar oss cirka €3,50 extra (ingår för kunden enligt beslut).

**Kontroll:** Storefront API (kanalen Lovable) ser alla fyra produkterna. En testvarukorg med "Front engraving text"/"Back engraving text" skapades, och kassan ligger på shop.vermo.se. Inga CJ-produkter är upplagda än.

**Kontroll efter Lovables koppling (2 okt, commit 09627fc):**
- Alla 92 kombinationer som sajten kan välja ger rätt variant, är köpbara och kostar rätt (599/699/599/599 SEK). Kombinationerna är färg × baksida × födelsemånad × band.
- Alla alternativvärden är NFC-normaliserade, så "é" och "ä" matchar exakt.
- Fem testvarukorgar gav rätt variant, pris, `Front engraving text` och `Back engraving text`. Kassan ligger på shop.vermo.se. ♥ och å/ä/ö gick igenom oförändrade.
- Testprodukten är **arkiverad**. Den kan återställas, och sajten använder den inte längre.

## Bilderna från Ownprint (2 okt)
Varje produkt har 8–9 bilder i 2000 × 2000. **Alla varianter använder bild 0 som variantbild**, och den visas därför i Shopifys kassa och orderbekräftelse.

| Produkt | Visa aldrig (vilseledande) | Godkända, i ordning (första = huvudbild) |
|---|---|---|
| Hjärtat | 0, 1, 7: svart ask med tryckt kort "Till dig, med all min kärlek." · 6: kartong "MORE THAN JUST JEWELRY" | 5, 4, 2, 3 |
| Familjen | 0, 1, 6, 7 (samma som Hjärtat) | 5, 2, 4, 3, 8 (tabell över födelsestenar) |
| Vår dag | 0, 1, 6, 7 (samma som Hjärtat) | 5, 4, 2, 3 |
| Pappa | 6: engelsk text på plattan · 7: gravyr av foton och fotspår, som vi inte erbjuder · 8: ask med kort "Till världens bästa pappa." | 3, 0, 2, 1, 4, 5 |

- **Ask och kort ingår inte** (ägarens besked 2 okt), så bilderna med ask och kort är vilseledande enligt marknadsföringslagen.
- **Sajten:** Lovable ska bara visa godkända bild-id:n. Prompten är skickad, se LOVABLE-PROMPT.md 2 okt.
- **Kassan och mejlen:** visar bild 0 (ask med kort). Ägaren sa nej till att byta variantbild (2 okt). Det är rätt bild om asken faktiskt ingår.
  - Bara bilden byts. Pris, SKU, alternativ och lager rörs inte.
  - Alternativet är att ta bort ask-bilderna i Ownprint-appen.
- **Gravyrens typsnitt** på Ownprints bilder ("Ebba", "12.06.2021", "Pappa") är rak antikva, inte skrivstil. Sajtens förhandsvisning byts därför till Cormorant Garamond. Det slutliga beskedet ger provbeställningen.
- **Hero-bilden** på vermo.se är AI-genererad: ett symmetriskt hjärta med "Alltid med dig" i skrivstil, alltså inte produkten vi säljer. Den byts mot Hjärtats bild 5 tills egna foton finns.

## Läget 1 okt (kontrollerat via Shopify-kopplingen)
| Område | Läge |
|---|---|
| Produkter | 1 produkt totalt, oavsett status: testprodukten. Inga produkter från Ownprint eller CJ finns, inte ens som utkast. |
| Ownprint | Kopplad. Leveransplatsen "Ownprint Fulfillment" och fraktprofilen "Ownprint" finns. |
| CJ | Syns inte i Shopify. CJ:s koppling märks inte förrän en produkt listas, så kontrollera i CJ-appen att butiken står som auktoriserad. |
| Säljkanal för sajten | "Lovable" (`vibe-ide-app-lovable`). Apparna publicerar normalt bara till Online Store. Jag publicerar därför nya produkter till "Lovable" via API. |
| Shopify-temat (Online Store) | Lösenordsskyddat. Bra. |
| Moms | Priserna anges inklusive moms. Bra. |
| Policyer i kassan | Bara Shopifys engelska integritetsmall finns. Den visar Gmail-adressen och saknar telefonnummer. Övriga policyer saknas. Byts mot SHOPIFY-POLICYER.md. |
| Lovable | Två leveransval är byggda. Testprodukten är platshållare för Hjärtat med snabb leverans. |

**Frakt till Sverige, ändrat 1 okt**
- **Allmän fraktprofil:** "Normal" (65 kr, gratis från 470 kr) och "Express" (99 kr) är ersatta med "Fri frakt" för 0 kr.
  - Annars hade Standardvalet för 449 kr fått 65 kr i frakt, trots att sajten lovar fri frakt.
  - Annars hade Express sålts utan att någon partner kan leverera det.
- **Ownprint-profilen:** Sverige ändrat från €6,95 till "Fri frakt" för 0. Kontrolleras igen när Ownprint har skapat produkterna, ifall appen skriver över värdet.
- **Återställning:** i allmän profil "Normal" 65 kr med gratis frakt från 470 kr och "Express" 99 kr. I Ownprint-profilen Sverige €6,95.
- **Beslut 1 okt: bara Sverige vid lanseringen.**
  - I Shopify är Sverige den enda aktiva marknaden, så bara svenska adresser kan gå till kassan. EU-zonerna i fraktprofilerna används därför inte.
  - EU utan OSS går inte: 10 000-euro-gränsen gäller bara varor som skickas från Sverige, och Ownprint skickar från Nederländerna.
  - EU prövas när den svenska försäljningen fungerar, och då med OSS-registrering.

## Produktval
| Vermo | Snabb: Ownprint (exakt namn i appen) | Standard: CJ (sökord i CJ-appen) |
|---|---|---|
| **Hjärtat** | Heart Necklace (Fine Link), €11–12 | "custom engraved heart necklace stainless steel" |
| **Familjen** | Coin Necklace with Birthstone (Fine Link), €13,50 | "custom coin necklace engraved names birthstone" |
| **Vår dag** | Horizontal Bar Necklace (Fine Link), €11–12 | "custom engraved bar necklace stainless steel" |
| **Pappa** | Premium Engraved Men's Leather Bracelet, €16,50 | "engraved leather bracelet men stainless steel" |

Ownprints frakt inom EU kostar €6,95 för första varan och €3 per extra vara. Färgerna är Silver (stål), 18K Guld och 18K Roséguld.

**Krav på CJ-produkterna:**
- 316L rostfritt stål. Inte "alloy", "zinc alloy" eller "copper", där risken för bly och kadmium är högre.
- Tre färger: silver, guld och roséguld, gärna PVD/IP-plätering.
- Kunden ska kunna lägga in egen text (laser). Kontrollera att å, ä och ö fungerar.
- Frakt till Sverige med CJPacket (9–18 dagar).
- Bra betyg och riktiga produktbilder.
- Anteckna inköpspris och frakt till Sverige, så att marginalen kan räknas.

## Priser (inkl. moms, samma pris för alla färger)
| Produkt | Snabb leverans | Standardleverans |
|---|---|---|
| Hjärtat | 599 kr | 449 kr |
| Familjen | 699 kr | 529 kr |
| Vår dag | 599 kr | 449 kr |
| Pappa | 599 kr | 449 kr |

- **Täckningsbidrag före annonser** (uppdaterat 2 okt, räknat med cirka 11,2 kr/€ och kortavgift cirka 13 kr):
  - Intäkt för Hjärtat snabb: 599 kr inklusive moms, alltså 479 kr exklusive moms.
  - Kostnad: produkt cirka €11,5, frakt €6,95 och baksidesgravyr €3,50 när kunden använder den. Tackkort tillkommer med €1,50 om det slås på.
  - **Täckningsbidrag:** cirka 240 kr utan baksida, 220 kr med baksida och 205 kr med baksida och tackkort.
  - Standard (CJ) är pausad, eftersom ingen produkt uppfyllde kraven (2 okt).
- **Gravyr:** framsidan ingår alltid. Baksidan ingår vid snabb leverans. Vid standard erbjuds den bara om CJ-produkten stöder det.

## Steg för ägaren
1. **Ownprint-appen:** skapa de fyra produkterna med tre färger var, sätt priserna i kolumnen "Snabb leverans" och publicera till Shopify.
2. **CJ-appen:** välj fyra motsvarigheter enligt kraven ovan, sätt priserna i kolumnen "Standardleverans" och skicka dem till Shopify.
3. **Säg till.** Jag publicerar då de åtta produkterna till kanalen "Lovable" via API och kontrollerar priser och frakt.
4. **Lovable:** jag fyller i handles och färgnamn per val i `productGroups.ts`. I samma ändring blir materialtexten per färg:
   - Silver: rostfritt stål.
   - Guld och Roséguld: stål med plätering.

   I dag står "18K guldpläterat" även för Silver.

## Instruktion till Claude i Desktop-appen

Den aktuella prompten finns i **DESKTOP-PROMPT.md** (uppdaterad 1 okt).
- Kör den i en ny lokal chatt i Claude Desktop, med Claude in Chrome påslaget.
- Prompten har titlar och priser för alla åtta produkterna.
- Den sätter säkerhetsregler: fråga före allt som kostar, rör inte frakt och policyer, inga jämförpriser och inga leverantörsnamn.
- Den ber om en rapport med gravyrfältens exakta namn.

## Innan standardleveransen öppnas för kunder (ECONOMY_ENABLED)
1. **IOSS:** registrera IOSS hos Skatteverket, eller använd tillfälligt CJ:s, och lägg in numret i CJ. Annars får kunden betala moms och avgift vid leverans.
2. **Prover från CJ godkända:** kvalitet, å/ä/ö och leveranstid uppmätt.
3. **Testrapport för nickel (EN 1811), bly och kadmium.** Vi är importör och har ansvaret.
4. **Materialtext** bekräftad för varje CJ-produkt.
5. **Förpackning:** antingen köps CJ-förpackning och kort, eller så visar sajten tydligt vad som ingår, vilket den redan gör per val.
6. **Ursprung och policyer:**
   - Visa på sajten att Standard skickas från Kina, utan att nämna partnern. Annars kan kunden tro att den skickas från EU som Snabb, vilket kan räknas som vilseledande utelämnande.
   - Lägg till överföringen av personuppgifter till Kina, med skyddsåtgärd, i integritetspolicyn.
   - Lägg till Standardtiderna i Fraktpolicy.

## Sista beställningsdag för jul
- Snabb leverans: 7 december.
- Standardleverans: 27 november. Därefter visas valet som "Hinner inte fram till julafton".
