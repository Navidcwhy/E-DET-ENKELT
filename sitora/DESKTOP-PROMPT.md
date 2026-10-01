# Prompt till Claude Desktop: skapa produkterna i Ownprint och CJ

## Innan du klistrar in
1. Öppna en **ny chatt** i Claude Desktop. Använd inte molnsessionen som sköter repot.
2. Slå på **Claude in Chrome**. Det rekommenderas, eftersom du redan är inloggad i Shopify där. Datorstyrning fungerar också.
3. Logga in i Shopify admin i Chrome innan du startar.
4. Klistra in texten nedan. Godkänn bara steg du förstår. Claude ska fråga innan allt som kostar pengar.
5. När den är klar: klistra in rapporten i molnsessionen. Där publiceras produkterna till kanalen "Lovable", kopplas på sajten och kontrolleras (priser, frakt och gravyrfält).

```text
Du ska hjälpa mig att lägga upp produkter i min Shopify-butik via apparna Ownprint och CJdropshipping. Använd Claude in Chrome, alltså min Chrome där jag är inloggad. Om du inte kommer åt webbläsaren eller Shopify: säg till direkt och stanna.

BUTIK
- Namn: Vermo. Shopify admin: https://admin.shopify.com/store/sitora-s-sentiments-m92xh-0dypfzx1
- Apparna "Ownprint: Print on Demand" och "CJdropshipping" är installerade.
- Sajten vermo.se hämtar produkterna från Shopify. En annan Claude kopplar ihop dem efteråt.

REGLER (gäller alltid)
1. Fråga mig innan du betalar, beställer något, godkänner en avgift, startar ett abonnemang, gör en provbeställning eller godkänner nya appbehörigheter.
2. Ändra inte testprodukten "TEST – Hjärthalsband (radera före lansering)".
3. Ändra inte frakt- och leveransinställningarna. Sverige ska ha "Fri frakt" för 0 kr.
4. Ändra inte heller policyer, domäner, språk, marknader, betalningar eller webbutikens lösenord. Om en app vill ändra något av detta: avbryt och fråga mig.
5. Radera ingenting.
6. Sätt aldrig ett jämförpris ("Compare-at price"). Inga överstrukna priser.
7. Skriv aldrig Ownprint, CJ eller någon annan leverantör i produkttitlar eller beskrivningar.
8. Gör en produkt i taget. Kontrollera efter den första att den syns under Produkter i Shopify innan du fortsätter.
9. Är du osäker: stanna och fråga.

DEL 1: OWNPRINT (Snabb leverans från EU). Gör den först.
Skapa dessa fyra produkter i Ownprint-appen. Om namnet skiljer sig, välj närmaste motsvarighet.

| Produkt i Ownprint | Titel i Shopify | Pris |
|---|---|---|
| Heart Necklace (Fine Link) | Hjärtat – Snabb leverans | 599 kr |
| Coin Necklace with Birthstone (Fine Link) | Familjen – Snabb leverans | 699 kr |
| Horizontal Bar Necklace (Fine Link) | Vår dag – Snabb leverans | 599 kr |
| Premium Engraved Men's Leather Bracelet | Pappa – Snabb leverans | 599 kr |

För varje produkt:
- Färger: silver, guld och roséguld, de som finns. Om appen låter mig namnge färgerna: använd Silverfärg, Guldfärg och Roséguldfärg. Annars behåll appens namn.
- Samma pris för alla färger och varianter. Priset anges i SEK inklusive moms.
- Kunden ska kunna skriva egen gravyrtext på framsidan. Slå på gravyr på baksidan om det finns. Kontrollera att å, ä och ö är tillåtna.
- Familjen: kunden ska kunna välja födelsesten. Notera om det är en variant eller ett textfält.
- Behåll appens bilder och beskrivning.
- Publicera till Shopify. Försäljningskanalerna behöver du inte ställa in, det sköter min andra Claude.

Kontrollera sedan Ownprints inställningar för varumärke och förpackning:
- Paketet ska vara neutralt (white label), utan Ownprint-loggor och utan priser. Rapportera vad som gäller.
- Presentask och meddelandekort ska ingå i varje order, om det går. Slå på det bara om det inte kräver betalning nu. Rapportera kostnaden per order.

Viktigt att ta reda på: de exakta fältnamnen (line item properties) som Ownprint läser för gravyr fram, gravyr bak, meddelandekort, typsnitt och födelsesten. Leta i produktens personaliseringsinställningar, i appens inställningar och på Ownprints hjälpsidor om "line item properties", "headless" eller API. Skriv av namnen exakt, med stora och små bokstäver.

DEL 2: CJDROPSHIPPING (Standardleverans från Kina). Gör den efter del 1.
Hitta en motsvarighet till var och en av de fyra produkterna i del 1. Kraven är:
- rostfritt stål 316L, inte "alloy", "zinc alloy", "copper" eller "brass"
- färgerna silver, guld och roséguld
- kundens egen text graveras med laser, och å, ä och ö stöds
- spårbar frakt till Sverige (CJPacket eller liknande); notera antal dagar
- bra betyg och riktiga produktbilder

Lägg till dem i butiken med dessa titlar och priser:

| Motsvarar | Titel i Shopify | Pris |
|---|---|---|
| Hjärtat | Hjärtat – Standardleverans | 449 kr |
| Familjen | Familjen – Standardleverans | 529 kr |
| Vår dag | Vår dag – Standardleverans | 449 kr |
| Pappa | Pappa – Standardleverans | 449 kr |

- Samma regler för färger och pris som i del 1.
- Beställ inga prover och betala ingenting.
- Ta reda på hur CJ får kundens gravyrtext: via fältnamn (line item property) eller via deras funktion för POD/customization.
- Om ingen produkt uppfyller kraven: lägg inte till något. Rapportera i stället de bästa alternativen med länkar.

RAPPORT (skicka när du är klar)
1. En tabell med en rad per produkt och dessa kolumner:
   - titel i Shopify
   - färgvarianternas namn
   - försäljningspris
   - inköpspris
   - frakt till Sverige
   - leveranstid till Sverige
   - om gravyr på baksidan, presentask och meddelandekort finns, och vad de kostar
2. Fältnamnen för gravyr, kort, typsnitt och födelsesten, exakt stavade, för både Ownprint och CJ.
3. Vad du inte kunde göra, och varför.
```
