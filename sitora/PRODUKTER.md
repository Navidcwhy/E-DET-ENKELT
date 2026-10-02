# Vermo: produkter och två leveransval (2 okt 2026)

Kunden ser en produkt och väljer **Snabb leverans** (EU-partnern Ownprint) eller **Standardleverans** (CN-partnern CJdropshipping). Partnernas namn syns aldrig på sajten. Varje val är en egen Shopify-produkt från respektive app, så ordern går automatiskt till rätt partner.

## Beslut 2 okt (ägarens svar)
- **Presentask och meddelandekort ingår inte.** Ownprint har bara ett allmänt tackkort som kostar €1,50 extra.
  - Löftet tas bort från sajten och fraktpolicyn.
  - Hälsningen erbjuds i stället som gravyr på baksidan (max 50 tecken, ingår).
- **Tackkortet:** rekommendationen är att inte slå på det vid lanseringen. Det kostar cirka 17 kr per order och är inte personligt. Det prövas senare om data visar att det behövs.
- **CJ:** ingen produkt uppfyllde kraven. Standardleveransen förblir avstängd (ECONOMY_ENABLED=false), och lanseringen sker med endast Snabb leverans.

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
