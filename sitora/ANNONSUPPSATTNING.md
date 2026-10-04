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
   - *Annonsnivån granskad från skärmbilder (3 okt, kl. 16.20). Så görs den:*
     - **Annons 1** heter `mamma_kroken`.
       - Video: Mamma-kroken. URL: `https://vermo.se/smycken/hjartat`. Visningslänk: `vermo.se`.
       - Under **Test av innehåll → Konfigurera test** läggs Julberättelsen till som version 2, med samma text och länk. Då får båda Hjärtat-filmerna leverans.
     - **Annons 2** heter `familjen_rose` och ligger i samma annonsgrupp.
       - Video: Familjen rosé. URL: `https://vermo.se/smycken/familjen`.
     - **Webbadressparametrar** för båda: `utm_source=meta&utm_medium=paid&utm_campaign=jul_test&utm_content={{ad.name}}`. Meta fyller i annonsens namn själv.
     - **Avmarkera "Annonser från flera annonsörer"**, så att filmen och texten inte beskärs och annonsen inte visas bredvid konkurrenter.
     - **Identitet:** välj Instagram-profilen Vermo. Varningen under Evenemangsinformation visade att den saknades.
     - **Anpassade destinationer** ska vara inaktiverade. **Evenemang** och **Språk** ska vara av.
4. **Betalmetod:** Ads Manager → Fakturering. Kontrollera allt och tryck **Publicera**.

## Claude Desktop-körningen 4 okt: rapport och svar
Prompten finns i DESKTOP-PROMPT-META.md. Inget publicerat, inget borttaget och inga betalningsuppgifter ändrade.
- **Klart enligt rapporten:**
  - Valutan är SEK. Kampanjens inställningar och beloppsgräns (1 050 kr) stämde redan.
  - Annonsgruppen har bytt namn, lägsta ålder är 25 och starten är flyttad till 4 okt.
  - Annonsen heter nu mamma_kroken och har visningslänk vermo.se, AI-märkning, UTM-parametrar och förbättringarna avstängda (utom "Relevanta kommentarer").
  - Knappen är "Köp nu", eftersom "Handla nu" saknas i listan.
- **Rotorsak till blockeringen:**
  - Annonskontot 3439617542952505 låg utanför företagsportföljen "Shopify: sitorassentiments…" (1089341350349253), som äger datasetet 1042319362191805.
  - Ads Manager kräver en portfölj för webbplatshändelser.
  - **Svar:** lägg till annonskontot i portföljen och ge det åtkomst till datasetet. Det är permanent.
- **Sidan:** det fanns ingen Vermo-sida, så annonsen använde sidan Sitora. **Svar:** byt namn på sidan till Vermo.
- **Instagram:** kontot var inte kopplat till annonskontot. **Svar:** koppla det via portföljen, eller via "Anslut profil" (ägaren loggar in).
- **Filmerna:**
  - Mediebiblioteket hade 1000019137–1000019139.mp4, troligen uppladdade från mobilen.
  - Våra filmer känns igen på längd och text: mamma_kroken 9,8 s, julberattelsen 12,0 s och familjen_rose 8,4 s.
  - Varje annons får bara sin film. De fyra bilderna tas bort ur annonsen.
- **Annonsgruppens egen gräns (150 kr/dag):** tas bort. Kampanjens gräns på 1 050 kr räcker som tak.
- **Upptäckt:** produktsidorna nämnde inte sista beställningsdag 7 december, som annonstexten gör.
  - Åtgärdat i Lovable runda 8: raden står nu vid köpknappen.
  - 7 december är ännu inte bekräftat, se LANSERING.md.
- **Profilbild för sidan och Instagram:** `sitora/brand/vermo-profilbild-mork.png` (rekommenderas) och `vermo-profilbild-ljus.png`, båda i 1080×1080 med sajtens ordmärke.

**Andra rapporten och ägarens beslut (4 okt, eftermiddag):**
- **Klart:**
  - Annonsgruppens egen gräns är borttagen. Konverteringsplatsen är Webbplats.
  - Schemat är från i dag kl. 13.21 till 10 okt kl. 23.59. Publiceras det i morgon blir slutet 11 okt.
- **Portföljen hade redan ett annonskonto** som Shopify skapade: 2766771640404009, utan betalmetod.
  - **Beslut:** flytta ändå in annonskonto 3439617542952505, så att kampanjen och betalmetoden finns kvar. Shopifys konto används inte.
- **Sidan Sitora används till annat:** biografin gäller bröllopstryck och Nordic Meadow på Etsy.
  - **Ägarens beslut:** sidan Sitora behålls oförändrad och används som avsändare i annonserna.
  - Det går att försvara: sidfoten på vermo.se säger redan "En skapelse av Sitora", och Sitora är säljarens firmanamn.
  - Nackdelen är att den som trycker på avsändaren hamnar på en sida om bröllopstryck. Räkna med något lägre förtroende och klickfrekvens. Avsändaren är densamma i alla annonser, så jämförelsen mellan filmerna håller ändå.
  - **Före Black Week:** skapa en egen Vermo-sida. Det kräver inget Instagram, och profilbilden är klar.
- **Instagram:**
  - **Ägarens beslut:** inget Instagram-konto kopplas. Annonserna visas ändå på Instagram, under sidan Sitora ("Använd Facebook-sida").
  - Kommentarer på annonserna hanteras i Meta Business Suite.
- **Filmerna i mediebiblioteket** (1000019137–1000019139) är andra klipp, inte våra. Ägaren lägger våra tre filer i Hämtade filer.

**Tredje rapporten, sammanfattning enligt steg 6 (4 okt):**
- **Klart som utkast:** tre annonser i en annonsgrupp.
  - mamma_kroken, julberattelsen och familjen_rose har rätt filmer (längd och text kontrollerad) och identiteten Sitora.
  - Knappen är "Köp nu". AI-märkning och UTM är satta, och alla förbättringar är avstängda utom "Relevanta kommentarer".
  - Metas förval av ett evenemang "mån 7 dec" är borttaget. Spenderat: 0 kr.
- **Innehållstestet** kräver minst två testannonser. Därför är julberattelsen en egen annons.
- **Blockerande:**
  - Meta nekade flytten till portföljen, eftersom den redan har sitt största tillåtna antal annonskonton. Fler tillåts först efter några veckor.
  - Utan dataset kan annonsgruppen inte publiceras.
- **Beslut:**
  - **Dataset:** prova först att dela datasetet direkt med annonskontot, vilket går att ta tillbaka.
    - Räcker det inte byggs kampanjen om i portföljens konto 2766771640404009.
    - Där lägger ägaren själv till betalmetoden. Den gamla kampanjen stängs av men tas inte bort.
  - **Annonserna** slås på före publiceringen. Annars skapas de pausade.
  - **Beskärning:** textblocken ligger på y 236–549 i Hjärtat-filmerna och 236–1304 i familjen_rose (av 1920).
    - 4:5 förankrad i överkant (y 0–1350) visar alla texter i alla tre filmerna.
    - 1:1 förankras i överkant för Hjärtat-filmerna. För familjen_rose läggs rutan på ca y 230–1310.
  - **Musik:** Ads Manager har inget musikval för video. Testet körs tyst, lika för alla tre. Spår kan läggas in i filerna till nästa omgång och till TikTok.
- **Påminnelse:** julklappsraden på vermo.se syns först när ägaren publicerar Lovable runda 8. Det är gjort och verifierat live 4 okt.

**Fjärde rapporten (4 okt): datasetet går bara att använda i portföljens konto**
- **Delning:** "Dela med ett annonskonto" listar bara konton i portföljen. Det personliga kontot kan inte få datasetet så länge det står utanför portföljen.
- **Datasetet har inga kopplade annonskonton**, inte heller Shopify-kontot 2766771640404009.
- **Kontroll av Shopify-kontot:** valutan är SEK och sidan Sitora går att välja. Tidszonen visas inte i kontoinställningarna.
- **Desktop skapade ett tomt utkast** i Shopify-kontot, "Ny Försäljning-kampanj". Det är inte publicerat.
- **Beslut: alternativ A.** Att vänta några veckor skulle kosta inlärning före Black Week.
  - Datasetet kopplas till Shopify-kontot. Det görs under Datauppsättningar och pixlar → Kopplade resurser och går att ta tillbaka.
  - Kampanjen byggs om där i utkastet, med samma inställningar, påslagna reglage och beskärningen ovan.
  - Den gamla kampanjen i det personliga kontot stängs av men tas inte bort.
  - **Ägaren själv:** lägger till betalmetod och verifierar telefonnumret i Shopify-kontot (Kontoöversikt → "Kom igång med konfigureringen").
  - Slutdatumet ska vara 23.59 svensk tid. Tidszonen kontrolleras i annonsgruppens schema.

**Femte rapporten (4 okt): kampanjen är ombyggd i Shopify-kontot 2766771640404009**
- **ID:n:**
  - Kampanj 120250857227530005, annonsgrupp 120250857227510005.
  - mamma_kroken 120250857227520005, julberattelsen 120250857567470005 och familjen_rose 120250857567480005.
  - Allt är utkast och reglagen är på. Spenderat: 0 kr. Den gamla kampanjen i det personliga kontot är avstängd.
- **Granskat och godkänt:**
  - Utkastet hade Shopify-katalogen påslagen. Den är nu "Använd inte en katalog".
  - Datasetet och Köp är satta, och slutdatumet är 10 okt kl. 23.59 svensk tid.
  - Sitora med "Använd Facebook-sida", Köp nu, UTM, AI-märkning och avstängda förbättringar är som tidigare.
- **Beskärning:**
  - Verktyget har bara 9:16, 1:1 och 16:9. Flödena använder därför 1:1 (överkant, och för familjen_rose från strax ovanför slutskylten). Stories, Reels och Utforska visar hela 9:16-filmen.
  - Desktop kontrollerade att alla texter syns.
- **Meta föreslog igen evenemanget "mån 7 dec"** i familjen_rose. Det är urbockat.
- **Varningar:** inga köp de senaste 14 dagarna (väntat), högerkolumnen kräver bild och liggande 16:9-placeringar använder originalfilmen. Ingen åtgärd.
- **Beslut:**
  - **Ålder:** strikt 25+. Personer på WhatsApp med okänd ålder tas inte med.
  - **Test av innehåll med alla tre annonserna,** så att budgeten fördelas jämnt och varje film når cirka 300 kr, som stopp-regeln kräver.
    - Testet får inte höja budgeten, ändra beloppsgränsen eller flytta slutdatumet. Kräver det något annat hoppas det över.
  - **Ägaren** lägger till betalmetod och verifierar telefonnumret och skriver sedan "Publicera".

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

## Obs: UTM-länkarna syns inte i Shopify (kontrollerat 3 okt)
- Shopify Analytics räknar bara besök på Shopify-sidor. För senaste 7 dagarna visar den 2 sessioner, båda "direct", fast sajten har haft många besök.
- Sajten (Lovable) skickar alltså inte besöken till Shopify, och UTM följer inte med till kassan.
- **Facit för vilken film som säljer är Metas och TikToks egna rapporter.** De bygger på pixel och Conversions API.
- **Möjlig Lovable-ändring** (en liten runda): spara utm_* från landningen och skicka dem som dolda radattribut (`_utm_source`, `_utm_campaign`, `_utm_content`) när varukorgen skapas. Då står annonsen på varje order i Shopify.

## Efter start
- **Granskning:** båda plattformarna granskar annonserna, oftast inom några timmar.
- **Gör ingenting de första 48 timmarna.** Därefter gäller gränserna i ANNONSTEST.md:
  - Stäng av en video efter 300 kr utan lägg-i-varukorg och med CTR under 0,7 %.
  - Skala upp vinnaren med 20–30 % var tredje dag.
- **Första köpet:**
  - Kontrollera gravyrtexten i Ownprint innan du betalar.
  - Kontrollera att köpet syns som Purchase hos Meta och som Complete payment hos TikTok.
- **Total testbudget:** Meta 150 kr × 7 = 1 050 kr. TikTok 200 kr × 7 = 1 400 kr. Totalt ca 2 450 kr.
