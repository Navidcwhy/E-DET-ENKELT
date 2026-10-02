# Provbeställning: Ownprint (uppdaterad 2 okt 2026)

**Leverantör:** Ownprint (ownprint.co). Graverar i Rotterdam, alltså inom EU. Shopify-appen heter "Ownprint: Print on Demand".
**Syfte:** att testa på en gång:
- gravyrens kvalitet och typsnitt
- specialtecken
- leveranstid till dörren
- förpackning
- hela orderflödet från vermo.se till Ownprint

**Klart:**
- De fyra produkterna finns i Shopify och är kopplade på sajten.
- Ownprint läser fälten `Front engraving text` och `Back engraving text`.
- Sajten skickar dem exakt så. Det är testat med varukorgar 2 okt.

## Före beställningen
1. **Vänta tills Lovables bildrättelse är klar** (se LOVABLE-PROMPT.md, 2 okt), så att du testar den riktiga förhandsvisningen.
2. **Betalning.** Välj ett av sätten:
   - **A (rekommenderas):** en rabattkod på 100 %, för ett enda köp och giltig i 7 dagar. Ordern blir 0 kr och går igenom kassan utan kortbetalning, och Ownprint debiterar dig produktionen som vanligt. Säg till, så skapar jag koden.
   - **B:** betala vanligt med kort. Kräver att Shopify Payments är aktiverat. Pengarna går till dig själv, minus avgift.
3. **Butikslösenordet.** Shopify-temat är lösenordsskyddat, och det blockerar kassan. Öppna shop.vermo.se, ange lösenordet och använd sedan samma webbläsare.
4. **Öppna butiken via förhandsvisningen:** vermo.se/?preview=vermo2026. Annars visas bara förlanseringssidan.

## Prover (en order, fyra rader)
| # | Produkt | Val | Fram (max 20) | Bak (max 50) | Testar |
|---|---|---|---|---|---|
| 1 | Hjärtat | Roséguldfärg, med baksida | `Åsa & Öjvind` | `Alltid med dig ♥ 14/6` | å, Ö, &, ♥, /, baksida |
| 2 | Familjen | Guldfärg, mars, utan baksida | `Märta, Björn & Liv` | – | ä, ö, lång text på myntet, födelsesten |
| 3 | Vår dag | Silverfärg, med baksida | `Linnéa 14.06.2019` | `59°19'N 18°04'E` | é, siffror, °, ' |
| 4 | Pappa | Guldfärg, brunt band, med baksida | `Bästa pappa` | `Från Ella: 2026` | ä, kolon, band, plattan |

**Kostnad (uppskattning):**
- Produkter: €11,5 + €13,5 + €11,5 + €16,5.
- Baksida: 3 × €3,50.
- Frakt: €6,95 + 3 × €3.
- Totalt cirka €79, alltså cirka 880 kr.

## Kontrollera
1. **I Shopify admin**, på ordern:
   - Varje rad har rätt variant (färg, baksida, månad, band).
   - `Front engraving text` och `Back engraving text` står exakt som du skrev, med å/ä/ö.
2. **I Ownprint-appen:** ordern har tagits emot med samma texter. Ta en skärmdump.
3. **När paketet kommer:**
   - **Typsnitt:** rak antikva, som på Ownprints bilder? Jämför med sajtens illustration.
   - **Tecken:** ♥, °, /, : och & ska vara graverade och inte bytta eller borttagna.
   - **Skärpa och placering:** hur 18–20 tecken på myntet och 50 tecken på baksidan ser ut.
   - **Plätering:** färgton per färg. Stämmer Roséguldfärg med bilden?
   - **Förpackning:**
     - Vad ingår (påse, ask, kort)?
     - Finns Ownprints logga eller priser? Packsedeln?
     - Fotografera allt. Bilderna blir sajtens "Så kommer ditt smycke".
   - **Leveranstid:** beställningsdag, avsändningsdag och leveransdag. Jämför med löftet 2–5 + 1–10 arbetsdagar.
4. **Mejl:** orderbekräftelsen och fraktbekräftelsen kommer från info@vermo.se, och bilden i mejlet visar ingen ask.

## Beslut runt 12 oktober
- **Godkänt:**
  - Lansera med Snabb leverans.
  - Byt hero- och produktbilder mot egna foton av proverna.
  - Justera förhandsvisningens typsnitt och de tillåtna tecknen efter resultatet.
- **Underkänt** (å/ä/ö fungerar inte, dålig kvalitet eller mer än 10 arbetsdagar):
  - Reklamera hos Ownprint och gör ett nytt prov.
  - CJ är pausad tills vidare (se PRODUKTER.md).
- Tillverkare enligt GPSR är fortfarande **Sitora**, eftersom vi säljer under eget varumärke. Ownprint anges inte på sajten.
