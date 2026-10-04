# Prompt till Claude Desktop: bygg, granska och publicera TikTok-kampanjen (4 okt 2026)

**Så används den:**
1. Spara profilbilden `vermo-profilbild-mork.png` från projektchatten i Hämtade filer. Filmerna ligger redan där sedan Meta-kampanjen.
2. Öppna Claude Desktop med Claude in Chrome påslaget, i den Chrome där du är inloggad på TikTok Ads Manager.
3. Klistra in prompten nedan.
4. Claude stannar före Publicera. Klistra in sammanfattningen i projektchatten, så granskar jag den innan du skriver "Publicera".

```text
Hjälp mig att bygga, granska och publicera en TikTok-annonskampanj för min webbutik Vermo (vermo.se, graverade smycken, säljer bara i Sverige). Använd tillägget Claude in Chrome i min Chrome, där jag är inloggad på TikTok Ads Manager (ads.tiktok.com). Det är samma test som Meta-kampanjen vi publicerade i dag: tre filmer med samma texter.

REGLER
- Ändra inga betalningsuppgifter och lägg inte till kort. Betalmetod och eventuell verifiering av företaget gör jag själv. Säg till var.
- Publicera inte förrän jag har skrivit "Publicera" i chatten. Visa först sammanfattningen i steg 6.
- Skapa bara den här kampanjen. Rör inte andra kampanjer, kontoinställningar, pixlar eller kopplingen till Shopify.
- Ta inte bort något utan att fråga.
- Godkänn inga automatiska förslag (Smart+, automatiska förbättringar, budgethöjningar) utan att fråga.
- Om något ser annorlunda ut än jag beskriver: välj närmaste motsvarighet och skriv det i sammanfattningen. Gissa aldrig när det gäller pengar eller målgrupp. Fråga.

STEG 1: KONTOT
Öppna https://ads.tiktok.com och välj annonskontot som är kopplat till Shopify-butiken (Vermo eller Sitora). Rapportera:
- Annonskontots namn och ID, valuta och tidszon. Valutan ska vara SEK. Om den inte är det: stanna och fråga.
- Om betalmetod finns och om kontot kräver verifiering av företaget.
- Pixeln DAVPCUBC77UD1K9H6HKG: status och vilka händelser den har tagit emot de senaste 7 dagarna (t.ex. Visa innehåll, Lägg i varukorg, Påbörja betalning, Slutför betalning).
- Vilka identiteter som finns (TikTok-konton eller anpassade identiteter).

STEG 2: KAMPANJEN
- Manuell kampanj, inte Smart+. Mål: Försäljning, med webbplatsen som destination, utan produktkatalog och utan TikTok Shop.
- Namn: Vermo | Försäljning | Kreativtest okt
- Kampanjbudgetoptimering: av. A/B-test: av.
- Tak: sätt en livstidsbudget eller utgiftsgräns på 1 400 kr för kampanjen, om det går utan budgetoptimering. Annars sätts taket i annonsgruppen (steg 3).

STEG 3: ANNONSGRUPPEN (EN ENDA)
- Namn: SE | Bred | 200 kr
- Optimeringsplats: Webbplats. Pixel: DAVPCUBC77UD1K9H6HKG. Optimeringshändelse: Slutför betalning (Complete payment). Om den inte går att välja: Påbörja betalning, annars Lägg i varukorg. Skriv vilken du valde.
- Placering: välj placeringar manuellt, bara TikTok. Avmarkera Pangle, Global App Bundle, Lemon8 och övriga.
- Målgrupp: plats Sverige. Ålder 25–34, 35–44, 45–54 och 55+. Alla kön. Inga intressen, beteenden eller egna målgrupper. Utökad målgrupp (targeting expansion): av.
- Budget: daglig budget 200 kr. Om TikTok kräver mer: använd minimibeloppet och skriv det. Om kampanjen inte fick något tak i steg 2: använd i stället livstidsbudget 1 400 kr för hela perioden.
- Schema: start vid publicering. Slut 7 dagar senare kl. 23:59 svensk tid, alltså 10 oktober om du publicerar i dag och 11 oktober om du publicerar i morgon.
- Budstrategi: högsta leverans (lägsta kostnad), inget kostnadsmål. Leveranstyp: standard. Attribution: standard.
- Användarkommentarer: av. Nedladdning av video: av. Stitch och Duett: av.

STEG 4: ANNONSERNA
Filmerna ligger i Hämtade filer. Kontrollera längd och text innan du använder dem:
- vermo_mamma_kroken_10s.mp4: 9,8 s. Börjar med en ask med "Mamma" och texten "Julklappen hon aldrig tar av sig". I mitten: "Graverat med dina ord".
- vermo_julberattelsen_12s.mp4: 12,0 s. Samma första text. I mitten: "Graverat med hennes namn".
- vermo_familjen_rose_8s.mp4: 8,4 s. Börjar med en närbild på gravyren och texten "Barnets namn och födelsesten". I mitten: "Alltid nära hjärtat".
Alla tre slutar med "Fri frakt · vermo.se" och "Beställ senast 7 december för leverans före jul". Filerna har ett tyst ljudspår.

Gäller alla tre annonserna:
- Format: en enda video. Inte karusell och inte Spark Ads.
- Identitet: ett TikTok-konto som heter Vermo, om ett sådant finns. Annars en anpassad identitet med visningsnamnet Vermo och profilbilden vermo-profilbild-mork.png från Hämtade filer. Använd inte namnet Sitora här. Om bara TikTok-konton går att använda och inget heter Vermo: stanna och fråga.
- Musik: lägg till ett spår från TikToks kommersiella musikbibliotek (Commercial Music Library). Lugnt och instrumentalt, t.ex. piano eller stråkar, utan sång. Samma spår i alla tre. Det ersätter det tysta ljudspåret.
- AI-genererat innehåll: slå på märkningen (AIGC). Filmerna visar AI-genererade personer.
- Uppmaning: Handla nu, eller närmaste motsvarighet (t.ex. Köp nu).
- Automatiska förbättringar och kreativ optimering (Smart creative, automatiska undertexter, genererade texter eller röster): av.
- Spårning: pixeln DAVPCUBC77UD1K9H6HKG. Ingen tredjepartsspårning.

Annons 1: namn mamma_kroken
- Video: vermo_mamma_kroken_10s.mp4
- Annonstext: Hjärtat med hennes namn, graverat med dina ord. Fri frakt – beställ senast 7/12 för julleverans.
- Webbadress: https://vermo.se/smycken/hjartat?utm_source=tiktok&utm_medium=paid&utm_campaign=jul_test&utm_content=mamma_kroken

Annons 2: namn julberattelsen
- Video: vermo_julberattelsen_12s.mp4
- Annonstext: samma som annons 1.
- Webbadress: https://vermo.se/smycken/hjartat?utm_source=tiktok&utm_medium=paid&utm_campaign=jul_test&utm_content=julberattelsen

Annons 3: namn familjen_rose
- Video: vermo_familjen_rose_8s.mp4
- Annonstext: Barnens namn och födelsesten på ett mynt. Fri frakt – beställ senast 7/12 för julleverans.
- Webbadress: https://vermo.se/smycken/familjen?utm_source=tiktok&utm_medium=paid&utm_campaign=jul_test&utm_content=familjen_rose

STEG 5: GRANSKNING
Öppna förhandsvisningen för varje annons och kontrollera:
- Texterna i filmen syns och täcks inte av TikToks knappar, namn eller annonstext.
- Musiken hörs och är densamma i alla tre.
- Knappen och länken leder till rätt produktsida, och webbadressen laddar rätt sida på vermo.se.
- TikTok har inte lagt till genererade texter, undertexter eller röster.

STEG 6: SAMMANFATTNING INNAN PUBLICERING
Svara med:
1. Kontot (namn, ID, valuta, tidszon), betalmetod och verifiering.
2. Varje inställning från steg 2–4, markerad OK eller ÄNDRAD (vad och varför), inklusive vald optimeringshändelse, identitet och musikspår.
3. Avvikelser, varningar och frågor.
4. Maxbelopp (tak) och slutdatum.
5. Det jag behöver göra själv.
Vänta sedan på mitt "Publicera".

STEG 7: EFTER PUBLICERING
Kontrollera att status blir "Granskas" eller "Aktiv" och att ingen annons är avvisad. Rapportera kort. Godkänn inga förslag som dyker upp efter publiceringen.
```
