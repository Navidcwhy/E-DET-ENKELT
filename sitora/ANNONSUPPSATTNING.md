# Vermo: uppsättning av annonserna (Meta och TikTok), 3 okt 2026

Filerna finns i chatten: vermo_mamma_kroken_10s.mp4, vermo_julberattelsen_12s.mp4 och vermo_familjen_rose_8s.mp4. Testets logik finns i ANNONSTEST.md.

**Varför ägaren gör det:**
- Shopify-kopplingen kan inte skapa annonser hos Meta eller TikTok.
- Den här sessionen har ingen åtkomst till ägarens dator eller webbläsare.
- Kampanjer byggs som utkast. Det sista steget, "Publicera", startar betalningen och görs alltid av ägaren.

## Gemensamt
- **Spårning:**
  - Meta-pixel 1042319362191805 (med Conversions API).
  - TikTok-pixel DAVPCUBC77UD1K9H6HKG.
  - Båda rapporterar köp från kassan, eftersom samtycket förs över till kassan.
- **Optimering:** köp (Purchase / Complete payment).
- **Annonstexter** (samma för båda Hjärtat-annonserna, så att testet bara jämför videorna):

| Annons | Video | Länk |
|---|---|---|
| Mamma-kroken | vermo_mamma_kroken_10s.mp4 | https://vermo.se/smycken/hjartat?utm_source=KANAL&utm_medium=paid&utm_campaign=jul_test&utm_content=mamma_kroken |
| Julberättelsen | vermo_julberattelsen_12s.mp4 | https://vermo.se/smycken/hjartat?utm_source=KANAL&utm_medium=paid&utm_campaign=jul_test&utm_content=julberattelsen |
| Familjen rosé | vermo_familjen_rose_8s.mp4 | https://vermo.se/smycken/familjen?utm_source=KANAL&utm_medium=paid&utm_campaign=jul_test&utm_content=familjen_rose |

KANAL = `meta` eller `tiktok`.

## Meta: Instagram och Facebook (Ads Manager)
1. **Kampanj:**
   - Skapa → mål **Försäljning**.
   - Namn: `Vermo | Försäljning | Kreativtest okt`.
   - **Advantage+-katalogannonser: AV.** Testet gäller våra tre filmer. Shopify-katalogen innehåller dessutom alla Ownprint-bilder, även ask, kartong och engelsk text som är dolda på sajten. Katalogen visar också en varning om ogiltiga händelsedata, som åtgärdas först.
   - **Kampanjens beloppsgräns: 1 050 kr**, så att testet aldrig kan kosta mer.
   - **Budget:**
     - Kampanjbudget 150 kr/dag med en annonsgrupp går bra, och ger samma resultat som budget per annonsgrupp.
     - Meta kan lägga upp till 262,50 kr en enskild dag, men högst 1 050 kr per vecka.
   - **A/B-test** av, och **specialkategorier** tomma.
   - *Ägaren satte upp kampanjnivån den 3 okt, kl. 15.45. Granskat från skärmbilder: katalogannonserna var på och ingen beloppsgräns fanns.*
2. **Annonsgrupp:** `SE | Advantage+ | 150 kr`
   - Konverteringsplats **Webbplats**. Dataset/pixel **Vermo (1042319362191805)**. Händelse **Köp**.
   - Budget **150 kr/dag**. Start i kväll, slut efter 7 dagar.
   - Målgrupp:
     - **Advantage+-målgrupp**, plats **Sverige**.
     - Lägsta ålder 25 som kontroll. Förslag: kvinnor 25–60, intressen smycken och presenter.
   - Placeringar: **Advantage+-placeringar** (Reels och Stories får de stående filmerna).
   - *Granskat från skärmbilder (3 okt, kl. 15.59):*
     - *Konverteringsplatsen stod på "Webbplats och app". Den ska vara **Webbplats**.*
     - *Konverteringshändelse saknades. Den ska vara dataset Vermo och **Köp**.*
     - *Slutdatum saknades. Det ska vara 10 okt kl. 23.59.*
     - *Annonsör "Vermo", samma som betalaren, är OK.*
3. **Tre annonser** i samma annonsgrupp (namn enligt tabellen):
   - Identitet: Facebook-sidan och Instagram-kontot Vermo.
   - Format: en video. Ladda upp filen.
   - **Musik:** välj en låt i annonsens musikval. Filerna är tysta.
   - **Advantage+-förbättringar:**
     - Stäng av textförbättringar och det som ändrar bild eller text, t.ex. överlägg och visuella justeringar.
     - Musik får vara på.
   - **Primär text (Hjärtat):** `Ett hjärta med hennes namn, graverat med dina ord. Fri frakt. Beställ senast 7 december för leverans före jul.`
   - **Primär text (Familjen):** `Barnens namn och födelsesten, nära hjärtat varje dag. Fri frakt. Beställ senast 7 december för leverans före jul.`
   - **Rubrik:** `Hjärtat – graverat halsband` eller `Familjen – namn och födelsesten`.
   - **Beskrivning:** `Fri frakt · 599 kr` eller `Fri frakt · 699 kr`.
   - **Uppmaning:** **Handla nu**. Webbadress enligt tabellen med `utm_source=meta`. Visningslänk `vermo.se`.
   - Erbjuder Ads Manager **Kreativt test** (Creative testing) för annonserna: använd det. Då fördelas budgeten jämnt mellan de tre videorna.
4. **Betalmetod:** Ads Manager → Fakturering. Kontrollera allt och tryck **Publicera**.

## TikTok (Ads Manager)
1. **Kampanj:**
   - Mål **Försäljning**, webbplats.
   - Namn: `Vermo | Försäljning | Kreativtest okt`.
   - Ingen kampanjbudget (CBO av).
2. **Annonsgrupp:** `SE | Bred | 200 kr`
   - Optimeringsplats **Webbplats**. Pixel **DAVPCUBC77UD1K9H6HKG** (via Shopify). Händelse **Slutför betalning** (Complete payment).
   - Placering: **endast TikTok**. Avmarkera Pangle och övriga appar.
   - Målgrupp: **Sverige**, 25–55+, alla kön. Bred målgrupp, inga intressen behövs.
   - Budget **200 kr/dag**. TikTok kräver minst cirka 20 USD per dag och annonsgrupp. Kör i 7 dagar.
3. **Tre annonser:**
   - Identitet: Vermo.
   - Ladda upp videon och lägg till musik från **Commercial Music Library**.
   - Slå på **AI-genererat innehåll** (AIGC). Filmerna visar realistiska AI-personer.
   - **Annonstext Hjärtat** (96 tecken): `Hjärtat med hennes namn, graverat med dina ord. Fri frakt – beställ senast 7/12 för julleverans.`
   - **Annonstext Familjen** (90 tecken): `Barnens namn och födelsesten på ett mynt. Fri frakt – beställ senast 7/12 för julleverans.`
   - **Uppmaning:** **Handla nu**. Webbadress enligt tabellen med `utm_source=tiktok`.
4. **Betalmetod och verifiering:**
   - TikTok kan kräva verifiering av företaget, t.ex. registreringsbevis för den enskilda firman.
   - Tryck **Publicera**.

## Efter start
- **Granskning:** båda plattformarna granskar annonserna, oftast inom några timmar.
- **Gör ingenting de första 48 timmarna.** Därefter gäller gränserna i ANNONSTEST.md:
  - Stäng av en video efter 300 kr utan lägg-i-varukorg och med CTR under 0,7 %.
  - Skala upp vinnaren med 20–30 % var tredje dag.
- **Första köpet:**
  - Kontrollera gravyrtexten i Ownprint innan du betalar.
  - Kontrollera att köpet syns som Purchase hos Meta och som Complete payment hos TikTok.
- **Total testbudget:** Meta 150 kr × 7 = 1 050 kr. TikTok 200 kr × 7 = 1 400 kr. Totalt ca 2 450 kr.
