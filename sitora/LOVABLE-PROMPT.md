# Lovable-prompt – Sitora-butiken

*v2 · 28 sep 2026: leverantörsneutral (Ownprint eller CJdropshipping). Skickad till Lovable i workspace "Navid's Lovable".*

**Status 28 sep 2026, 14:41: steg 1 klart**
- Projekt: https://lovable.dev/projects/8532ae5e-908b-45df-8d28-00525d2e69c7 (auto-namn "Sitora's Sentiments")
- Förhandsvisning: https://id-preview--8532ae5e-908b-45df-8d28-00525d2e69c7.lovable.app

Klart och fungerar:
- design, startsida, kollektion och produktsida med personaliserare (live-förhandsvisning, å/ä/ö, meddelandekort, baksidesgravyr)
- varukorg med testdata
- config för leverantör, kampanj och personalisering
- leveransberäkning
- sidstommar
- Lovable Cloud påslaget

Blockerat: Shopify-integrationen gick inte att nå från API-sessionen. Den måste slås på i Lovable-editorn, och sedan körs steg 2 (butik, priser, checkout).

**28 sep, 18:24: steg 2 skickat till Lovable**
- Shopify-koppling och testprodukt. Varukorgen går via Storefront API med line attributes.
- Bolagsuppgifter från metodkoll.se/villkor läggs i `src/config/company.ts`: enskild näringsidkare som driver Sitora, inte AB. Telefon saknas och är platshållare.
- WCAG 2.2 AA: guld #B8925A (ca 2,7:1 mot bakgrunden) används inte för text, i stället #8A6A3B (ca 4,7:1). Tangentbord, fokus, produktsökning.
- Hero-bilden görs om med svensk gravyr ("Alltid med dig").
- Ärligt utkast till "Om Sitora".

**29 sep, 17:24: steg 2 klart**
- Shopify-sandbox skapad (SEK, SE), testprodukt 599 kr i 3 färger, varukorg och kassa via Storefront API.
- Produktsökning, bolagsuppgifter, svensk hero-bild och WCAG-fixar.

Granskning av koden hittade:
- Baksidesgravyren +99 kr visades men debiterades inte i Shopify.
- Summorna räknades lokalt.
- Erbjudandet "2 för 999" syntes utan att någon rabatt fanns i Shopify.
- Köpknappen var inaktiverad utan förklaring.

**29 sep, 17:30: skickat till Lovable**
- Rättelser av punkterna ovan. Baksidesgravyren ingår tills vidare. Summorna hämtas från cart.cost. Paketerbjudandet stängs av till Black Week.
- Telefonnummer ifyllt.
- Steg 3: köpvillkor (ARN, ingen ODR-länk), integritetspolicy, cookie-banner med Consent Mode v2, ångerformulär och produktsäkerhet.

**29 sep, 18:02: steg 3 klart och granskat**
- Rättat och verifierat i koden:
  - telefon
  - baksidesgravyr för 0 kr ("ingår")
  - summor från Shopifys cart.cost och discountAllocations
  - paketerbjudandet avstängt
  - köpknappen visar vad som saknas
- Juridiska sidor klara: köpvillkor (ARN, ingen ODR-länk), integritetspolicy, leverans och reklamation, cookiepolicy, produktsäkerhet och ångerformulär. Ångerformuläret lagras i tabellen `withdrawal_requests` med låst RLS.
- E-postkvittot till ångerformuläret är blockerat tills en egen e-postdomän finns. Sajten påstår inte att mejl skickas.
- Cookie-rutan (1,6 krediter):
  - Är nu en icke-blockerande panel längst ned.
  - X och Esc betyder "Endast nödvändiga".
  - Consent Mode v2 är denied som standard.
- Shopify via Storefront API: Sverige har frakt "Normal" 0 kr och "Express" 99 kr. Express bör tas bort tills leverantören erbjuder express.
- Lovables Shopify-verktyg kan inte byta butiksnamn. Det görs i Shopify admin.
- Klistra-in-texter till Shopify-policyer finns i `SHOPIFY-POLICYER.md`.
- DNS-kontroll: sitora.se och sitorasmycken.se ger NXDOMAIN (troligen lediga, verifiera hos registrar). sitora.com är registrerad.

**30 sep, 13:29: namnbyte till Vermo och domänen vermo.se (ägarens beslut)**
- vermo.se: DNS hos One.com. A-posten pekar redan på Lovable (185.158.133.1), men domänen serverar idag Lovable-projektet "Vermo" (faktureringstjänsten). Den ersätts via "Move and connect" i samma workspace.
- vermo.se har null-MX ("0 ."), alltså ingen e-post idag. Adressen kundservice@vermo.se kräver att e-post skapas hos One.com.
- Skickat till Lovable:
  - namnbyte till Vermo
  - company.ts med kundservice@vermo.se
  - förlanseringsläge ("Öppnar i oktober" med nyhetsbrevsanmälan och ?preview=vermo2026 för att se hela butiken)
  - uppsättning av e-postdomän med lista över DNS-poster
  - butiksnamnet i Shopify, om verktyget klarar det
- Ordningen är viktig: publicera först, flytta sedan domänen, annars ligger vermo.se nere en stund.

**30 sep, 14:41–15:00: Vermo live i förlanseringsläge**
- Lovable: namnbytet till Vermo är klart, liksom sidan /om-vermo med omdirigering från /om-sitora, metadata och sitemap, förlanseringsgrinden (PRELAUNCH=true, ?preview=vermo2026 via HttpOnly-cookie) och tabellen för nyhetsbrevsanmälningar (låst).
- Publicerat som vermo-smycken.lovable.app, som omdirigerar till vermo.se. Ägaren har flyttat domänen.
- Verifierat via HTTP:
  - vermo.se visar "Öppnar i oktober | Vermo".
  - /smycken/hjartat är spärrad för besökare.
  - /integritetspolicy går att nå.
- Shopify (Storefront API): butiksnamnet är "Vermo". Integritetspolicyn är Shopifys engelska standardmall och måste ersättas. Retur-, frakt- och köpvillkor är tomma. Kort och plånböcker är inte aktiverade. Frakten "Express 99 kr" finns kvar.
- Öppna problem:
  - vermo.se har fortfarande null-MX, så kundservice@vermo.se (som syns publikt) tar inte emot mejl.
  - www.vermo.se pekar på One.com (46.30.211.38) och ger 503. Den ska pekas mot 185.158.133.1.
  - E-postdomänen: ägaren klickar "Konfigurera notify.vermo.se" i Lovable-editorn och lägger in DNS-posterna hos One.com.

**1 okt: två leveransval och Shopify-kontroll**
- Lovable har byggt två leveransval per smycke, Snabb (EU) och Standard (CN). Standard är dolt publikt (`ECONOMY_ENABLED = false`).
- Shopify kontrollerades via Admin-kopplingen:
  - Butiken har bara testprodukten.
  - Ownprint är kopplad (leveransplats och fraktprofil finns).
  - CJ syns inte.
  - Säljkanalen för sajten heter "Lovable".
- Frakt till Sverige: "Fri frakt" för 0 kr i både allmän profil och Ownprint-profilen. Express 99 kr och Normal 65 kr är borttagna. Detaljer och återställningsvärden finns i PRODUKTER.md.
- Fortfarande öppet:
  - vermo.se har null-MX.
  - www.vermo.se pekar på One.com.
  - Policyerna i kassan är inte bytta.

**1 okt, eftermiddag: Shopify-inställningar, policyer, Lovable och DNS**
- Shopify (via API):
  - Svenska är aktiverat och publicerat.
  - Bekräftat: Sverige är den enda aktiva marknaden, så butiken säljer bara till Sverige.
- Shopify (ägaren behöver ändra själv):
  - Tidszonen är America/New_York. Ändra till Stockholm.
  - Standardspråket är engelska. Ändra till svenska.
  - Kontakt-e-posten är Gmail. Ändra till kundservice@vermo.se när brevlådan fungerar.
  - Butikens telefonnummer saknas.
  - Primär domän är myshopify.com. Byt till shop.vermo.se, se ONECOM-DNS.md.
- Online Store är lösenordsskyddat, och det blockerar headless-kassan.
  - Vid lansering: ta bort lösenordet och skicka Shopify-temats sidor vidare till vermo.se.
  - Provbeställningar före lansering: ange butikslösenordet i samma webbläsare först.
- Policyer: Shopify-kopplingen saknar `write_legal_policies`. SHOPIFY-POLICYER.md är uppdaterad för inklistring.
- Lovable: ändringarna är skickade (umsg_01m3vmg1ace0k83p18g1vgqw20) och väntar på att ägaren godkänner planen i editorn. De gäller:
  - materialtext per färg
  - ursprung flyttat från produktsidan till leveranssidan och FAQ
  - GPSR: Sitora som tillverkare
  - endast Sverige
  - integritetspolicy
  - svensk kassa (@inContext)
  - FAQ
- Ägarens egna ändringar i Lovable:
  - Sitora som moderbolagsnamn.
  - PRELAUNCH=false. Det är inte publicerat ännu. Publicera inte förrän produkterna är kopplade.
- DNS: steg för steg i ONECOM-DNS.md.

**1 okt, kl. 12: Lovable-ändringarna är klara (commit ed8cda5, 4,3 krediter)**
- Granskat i diffen. Alla sju punkterna är gjorda:
  - materialtext per färg
  - inget ursprung på produktsidan; ursprung på leveranssidan och i FAQ
  - Sitora som tillverkare, ingen EU-ansvarig
  - endast Sverige
  - integritetspolicy
  - @inContext SE/SV
  - FAQ
- Extra ändring av Lovable: Klarna är borttaget från förtroenderaden och produktsidan, eftersom Klarna inte är aktiverat. Läggs tillbaka om Klarna aktiveras.
- Oförändrat:
  - PRELAUNCH=false
  - Sitora
  - header och footer
  - butiken är inte publicerad
- Eget test mot Storefront API:
  - Varukorgen skapas med svensk kontext, och totalen blir 599 SEK.
  - Kassalänken hamnar på /password. Det bekräftar att lösenordet på Online Store blockerar kassan.
  - Kassans språk kan inte kontrolleras förrän lösenordet är borttaget.
- Förhandsvisningen kräver inloggning (401). Sidorna är därför kontrollerade via koden och Lovables eget webbläsartest.
- **Uppföljning kl. 15 (commit 3fe6b9a, 2,2 krediter):**
  - E-post: info@vermo.se i company.ts och __root.tsx. Kundservice-adressen är borttagen i hela koden.
  - FAQ: den dubbla raden är borta.
  - Varukorgen visar svenska etiketter för gravyrfälten. Nycklarna som skickas till Shopify är oförändrade.
- **Ägarens ändringar, granskade kl. 15:**
  - shop.vermo.se är primär domän i Shopify, med SSL.
  - Kundernas kontaktadress i Shopify är info@vermo.se.
  - www, MX och SPF fungerar.
  - Lovables avsändardomän är info.vermo.se. TXT-posten finns, men **NS-posterna saknas**.
  - Lovable skapade engelska mallar för inloggningsmejl. De används inte, eftersom butiken inte har kundkonton.
- **Kvar i Shopify:**
  - Tidszonen är Europe/Helsinki. Ändra till Stockholm.
  - Standardspråket är engelska.
  - Butikens telefonnummer saknas.
  - Tre policyer har kundservice@ och ska klistras in igen.
  - Privacy, Terms of service och Legal notice saknas.
  - Avsändaradressen är inte autentiserad.
- **Nästa steg i Lovable, när info.vermo.se är verifierad:**
  - Skicka ett mejl till kunden som bekräftar ånger (ångerknappen kräver bekräftelse på varaktigt medium).
  - Skicka en notis till info@vermo.se när någon ångrar ett köp.
  - Ta bort texten "E-postbekräftelse aktiveras …".
- **Kontroll kl. 15.15:**
  - Standardspråk är svenska. Shopifys automatiska svenska policymallar (med Gmail-adressen) är borta.
  - Alla sex policyer är ifyllda. Refund policy har fortfarande en förekomst av kundservice@.
  - Tidszonen är Europe/Madrid. Klockan är densamma som i Stockholm, så det fungerar.
  - Butikens telefonnummer saknas fortfarande.
  - DNS för info.vermo.se (NS och TXT) är korrekt. Lovables status är "Verifying your domain". Lovable stoppade enligt instruktion innan ångermejlen byggdes (1 kredit). Uppdraget skickas igen när domänen är aktiv.
  - Shopifys autentisering av avsändaradressen (s1–s4._domainkey) saknas.
- **Prompt för produkterna:** DESKTOP-PROMPT.md.
- **Kontroll kl. 15.25:**
  - Klart: Refund policy har info@, butikens telefon (0735362868) är ifylld, och alla sex policyer stämmer.
  - Shopifys avsändarautentisering: inga DKIM-poster hittades under de vanliga namnen (s1–s4._domainkey, shopify1/2._domainkey), inte heller med dubbel domän. Ägaren behöver kontrollera i Settings → Notifications att den visar "Authenticated".
  - Bygget av ångermejlen är skickat igen (umsg_01m3vt1jw4fhdrmyjhp31zpesq) efter att ägaren klickat Verify Domain.
  - Ägaren kör DESKTOP-PROMPT.md i en ny chatt i Claude Desktop.
- **Ångermejlen är klara (commit 0e31864, 4,3 krediter), granskade i diffen:**
  - info.vermo.se är verifierad.
  - Kunden får en bekräftelse på svenska från "Vermo <noreply@vermo.se>" med svar till info@vermo.se. Den innehåller tid i svensk tid, uppgifterna kunden lämnade, referens (8 tecken), nästa steg (returinfo inom två arbetsdagar), återbetalningsregeln, undantaget för gravyr, kontaktuppgifter och säljaruppgifter.
  - En intern notis går till info@vermo.se. Svar går direkt till kunden.
  - Om utskicket misslyckas sparas anmälan ändå, felet loggas och kunden ser reservtexten. Kvittotexten på sidan är uppdaterad.
  - Utformning: Georgia och #8A6A3B, utan spårningspixlar. Lovable lägger alltid till en avregistreringslänk.
  - Diffen innehåller bara mejlfilerna, Lovables e-postställning och WithdrawalForm/withdrawal.functions. Inget annat ändrades och inget publicerades.
  - Test: TEST-1 skickades till info@vermo.se (ref. 42611156) och testraden raderades.
  - **Ägaren åtar sig** att svara med returinformation inom två arbetsdagar.
- Små saker till nästa Lovable-runda, som görs ihop med de riktiga gravyrnycklarna:
  - Varukorgen visar de tekniska fältnamnen på engelska ("Front Engraving", "Spelling Approved"). De bör visas med svenska etiketter.
  - FAQ säger "Vi levererar endast inom Sverige" två gånger.

**2 okt: Ownprint-kopplingen är klar (commit 03f9040 och 09627fc, 9,9 krediter) och granskad**
- **Fungerar:**
  - Handles för de fyra snabba produkterna. Testprodukten är borttagen ur mappningen och **arkiverad** i Shopify.
  - Variantval: alla 92 kombinationer av färg, baksida, månad och band ger rätt köpbar variant med rätt pris. Testat mot Storefront API med sajtens egen matchningslogik.
  - Attributen `Front engraving text`, `Back engraving text`, `_Stavning godkänd` och `_Leveransval`. Fem testvarukorgar gav exakt text med å/ä/ö och ♥, och kassan ligger på shop.vermo.se.
  - Gränserna 20/50 tecken med räknare.
  - Måtten stämmer med Ownprints beskrivningar.
  - "Veganskt läder".
  - Inget typsnittsval.
  - Löftena om presentask och meddelandekort är borta ur texterna.
- **Brister som måste rättas före lansering:**
  1. **Bilderna:**
     - Sajten visar Shopify-bild 0. För Hjärtat, Familjen och Vår dag är det en svart presentask med tryckt kort ("Till dig, med all min kärlek."). Ask och kort ingår inte, så bilden är vilseledande.
     - Samma bild är variantbild och syns därför i kassan och orderbekräftelsen. Se PRODUKTER.md, "Bilderna från Ownprint".
  2. **Förhandsvisningen:**
     - Texten läggs på fasta koordinater ovanpå fotot. Med Ownprints foton hamnar den bredvid hänget, i fel storlek, och fotot har redan exempeltext ("Ebba"). Kontrollerat med en lokal rendering.
     - Den använder skrivstil, men Ownprints bilder visar rak antikva.
  3. **Hero-bilden** (AI) visar ett annat hjärta än det vi säljer, med skrivstil.
  4. **Småsaker:**
     - Familjens köpknapp säger "Kombinationen är inte tillgänglig" innan en månad har valts.
     - "Ingår: … – ingår" står dubbelt.
     - "/", ":" och "°" är spärrade, trots att Vår dag lovar att koordinater får plats.
- **Ägarens ändring 43a0bf4 (08.07), "Renaderade företagsuppgifter":**
  - Köpvillkoren visar inte längre namn, adress och telefon. Produktsidan visar inte längre tillverkaren.
  - Juridiskt går det, eftersom /kontakt och /produktsakerhet har alla uppgifter.
  - Men GPSR art. 19 kräver att själva produkterbjudandet anger tillverkare samt post- och e-postadress. Dessutom leder footerlänken "Företagsuppgifter" till en sektion utan adress och telefon.
- **Publicering:**
  - vermo.se är publicerad med en **äldre version**. Förlanseringssidan visar kundservice@vermo.se, en adress som inte finns.
  - Koden har nu PRELAUNCH=false. Publiceras den som den är blir hela butiken öppen, trots att kassan är blockerad av butikslösenordet.
  - Därför: sätt PRELAUNCH=true, publicera, och sätt false vid lansering.
- **Genomsökning av hela koden (75 filer, ref 09627fc):**
  - Inga löften om ask eller kort finns kvar.
  - Allt "läder" står som "veganskt läder".
  - Inga påståenden om 304/316.
  - Inga leverantörsnamn i kundtext.
  - "Kina" står bara på de dolda Standard-raderna (FAQ och leveranssidan, som bara visas i förhandsvisningen).
  - Skrivstilen (Great Vibes) laddas i __root.tsx. De gamla AI-produktbilderna används inte längre.
- **Rättelse skickad till Lovable** (umsg_01m3xvpjx6fbxag9rsccq6bt5e). Planen var klar kl. 08.35 (2,7 krediter), täcker alla sju punkterna och **väntar på att ägaren godkänner den i editorn**. Innehåll: bild-id:n som allowlist, ett galleri, en fristående SVG-illustration av gravyren i Cormorant Garamond, ny hero, Familjens knapp, tecknen, GPSR-raden, en länk från köpvillkoren till /kontakt och PRELAUNCH=true. Inget publiceras. Prompten finns nedan.
- **Till nästa Lovable-runda (litet):** integritetspolicyn på sajten säger "Gravyr- och korttexter raderas …". Ändra till "Gravyrtexter", eftersom inga kort ingår.
- **Shopify, kontrollerat 08.30:** fraktpolicyn säger fortfarande "Presentask och meddelandekort ingår." Ägaren klistrar in den igen från SHOPIFY-POLICYER.md.

<details><summary>Prompten (2 okt)</summary>

```text
Granskning av commit 09627fc (Ownprint-kopplingen) och 43a0bf4 (företagsuppgifter).

Det här fungerar och ska behållas:
- handles och variantval
- priserna
- attributen "Front engraving text", "Back engraving text" och "_Stavning godkänd"
- teckengränserna 20 och 50
- måtten
- veganskt läder

Jag har testat alla 92 variantkombinationer och fem varukorgar mot Storefront API. Alla blev rätt.

Men bilderna och förhandsvisningen måste rättas före lansering. Gör först en plan och vänta på godkännande. Publicera inte.

1. BILDER: VISA ALDRIG ASK, KORT ELLER ENGELSK TEXT
Flera av Ownprints bilder visar sådant som inte ingår, och de är därför vilseledande:
- svart presentask med tryckt kort ("Till dig, med all min kärlek." och "Till världens bästa pappa.")
- kartong med texten "MORE THAN JUST JEWELRY"
- engelsk text
- gravyr av foton eller fotspår, som vi inte erbjuder

Bild 0 är en av dem, och sajten använder den i dag som huvudbild.

Gör så här:
- Lägg till `imageIds: string[]` på leveransvalet i productGroups.ts.
- Hämta `id` på bilderna i Storefront-frågan.
- Visa bara bilder vars id står i listan, i listans ordning. Andra Shopify-bilder visas aldrig, inte heller bilder som partnern lägger till senare.
- Första id:t är huvudbilden i produktlistor, sök, varukorgen (bilden som skickas med addLine) och på produktsidan.

Godkända bilder:
- hjartat-snabb-leverans:
  gid://shopify/ProductImage/100780440977798,
  gid://shopify/ProductImage/100780440945030,
  gid://shopify/ProductImage/100780440879494,
  gid://shopify/ProductImage/100780440912262
- familjen-snabb-leverans:
  gid://shopify/ProductImage/100781280002438,
  gid://shopify/ProductImage/100781279904134,
  gid://shopify/ProductImage/100781279969670,
  gid://shopify/ProductImage/100781279936902,
  gid://shopify/ProductImage/100781280100742 (tabell med födelsestenarnas färger)
- var-dag-snabb-leverans:
  gid://shopify/ProductImage/100781319061894,
  gid://shopify/ProductImage/100781319029126,
  gid://shopify/ProductImage/100781318963590,
  gid://shopify/ProductImage/100781318996358
- pappa-snabb-leverans:
  gid://shopify/ProductImage/100781359071622,
  gid://shopify/ProductImage/100781358973318,
  gid://shopify/ProductImage/100781359038854,
  gid://shopify/ProductImage/100781359006086,
  gid://shopify/ProductImage/100781359104390,
  gid://shopify/ProductImage/100781359137158

Övrigt om bilderna:
- Om ingen godkänd bild hittas: visa gravyrillustrationen från punkt 2, aldrig en okänd Shopify-bild.
- Produktsidan får ett bildgalleri med de godkända bilderna: huvudbild och miniatyrer, och svepbart på mobil.
- Alt-texter på svenska, till exempel "Hjärtat i guldfärg med exempelgravyr, bild 2 av 4".
- Under galleriet: "Bilderna visar exempeltext och oftast guldfärg. Din färg och din text syns i illustrationen."

2. GRAVYRFÖRHANDSVISNINGEN: LÄGG INTE TEXT OVANPÅ FOTON
I dag lägger EngravingPreview kundens text på fasta koordinater mitt i bilden. Med Ownprints foton blir det fel:
- texten hamnar utanför smycket och blir större än hänget
- fotona har redan exempeltext ("Ebba", "12.06.2021", "Pappa") som syns samtidigt

Gör om förhandsvisningen till en fristående SVG-illustration, alltså inte ovanpå något foto.

Form per produkt:
- Hjärtat: hjärta.
- Familjen: runt mynt med en liten berlock i födelsemånadens färg. Ungefärliga färger:
  jan #8B1A2B, feb #6B3FA0, mar #7FD3E6, apr #F2F2F2 med tunn kant, maj #1E8C4E, jun #E7A6C8,
  jul #C2182B, aug #9ACD32, sep #1F3F9A, okt #F4A3C0, nov #F2C14E, dec #2E7DD7.
  Ingen berlock förrän en månad är vald.
- Vår dag: smal bar med proportionerna 6 × 39 mm.
- Pappa: ny form "plate", en liggande rektangulär platta på ett band i vald bandfärg (svart eller brunt). Pappa använder i dag "bar", vilket är fel form.

Utseende och innehåll:
- Metallfärg efter vald färg, med diskret gradient: Silverfärg #C0C0C0, Guldfärg #D4AF37, Roséguldfärg #B76E79.
- Texten sätts i rak antikva, var(--font-display) (Cormorant Garamond), aldrig i skrivstil. Ownprints produktbilder visar gravyr i rak antikva.
  - Ta bort `font="script"` och skrivstilen ur förhandsvisningen.
- Framsidan visas på en rad som skalas för att få plats.
- När kunden har valt hälsning på baksidan: visa en andra illustration, "Baksida", bredvid eller under.
  - Radbrytning till högst 3 rader på hjärta och mynt, och högst 2 rader på bar och platta.
  - Texten skalas för att få plats.
- Bildtext: "Illustration av gravyren. Typsnitt, storlek och radbrytning anpassas till smycket och kan skilja något."

Placering:
- Illustrationen placeras direkt under galleriet. På mobil kommer den direkt efter huvudbilden.
- Den uppdateras medan kunden skriver och väljer färg, månad och band.
- Startsidan, steg 2: byt "Se texten direkt på smycket medan du skriver." mot "Se en förhandsvisning av gravyren medan du skriver."

3. HERO-BILDEN
hero-heart-sv.jpg är AI-genererad: ett symmetriskt hjärta i roséguld med "Alltid med dig" i skrivstil. Det vi säljer är Ownprints sneda hjärta med gravyr i rak antikva.
- Byt hero-bilden på startsidan och förlanseringssidan, och og:image, mot Hjärtats godkända foto:
  https://cdn.shopify.com/s/files/1/1109/0355/8534/files/customzied_mockup_0d8d616d-5c3f-4519-b0e5-c9eed43cb4b0.jpg?v=1790861993
  - Ladda ned den till src/assets och public om det går. Använd annars URL:en med width-parameter.
  - Bilden är kvadratisk (2000 × 2000). Hjärtat ligger till höger om mitten, så beskär så att hjärtat syns i heron på både mobil och dator.
- Ta bort de gamla AI-bilderna (src/assets/product-*.jpg, src/assets/hero-heart*.jpg, public/hero-heart-sv.jpg) när de inte längre används.

4. FAMILJEN: FÖDELSEMÅNAD
- Så länge ingen månad är vald ska köpknappen säga "Välj födelsemånad", inte "Kombinationen är inte tillgänglig".
- Knappen ska vara klickbar när bara månaden saknas. Ett klick flyttar fokus till månadsväljaren och visar felet.
- Visa ingen röd varning innan kunden har försökt. Visa hjälptexten "Ingen månad är förvald." som i dag.

5. SMÅSAKER
- includedItems: "Ingår: Fri frakt · Gravera en hälsning på baksidan – ingår · Inga tullavgifter" säger "ingår" två gånger. Ändra punkten till "Hälsning graverad på baksidan".
  - Bannern och USP-raden får behålla sin text.
- Tillåtna tecken: lägg till "/", ":" och "°", så att datum som 14/6 2019 och koordinater som 59°19'N fungerar.
  - Ändra Vår dags hjälptext till: "Datum eller namn på framsidan (max 20 tecken). Koordinater, t.ex. 59°19'N 18°04'E, får plats på baksidan."
  - Tecknen kontrolleras i provbeställningen.
- När skrivstilen inte används längre:
  - Ta bort laddningen av Great Vibes från Google Fonts i src/routes/__root.tsx.
  - Ta bort --font-script och skrivstilsvalet i personalization.ts.
  - Den uppläsningsbara texten i förhandsvisningen ska säga "rak stil".

6. ÄGARENS ÄNDRING 43a0bf4: BEHÅLL DEN, MEN KOMPLETTERA
- Produktsidan:
  - GPSR (EU 2023/988, art. 19) kräver att själva erbjudandet anger tillverkarens namn samt post- och e-postadress.
  - Lägg tillbaka det som en hopfällbar rad, "Produktsäkerhet och tillverkare", längst ned i "Om smycket".
  - Den ska vara stängd från början och innehålla `profile.safety.manufacturer` och varningen om smådelar.
- Köpvillkor:
  - Footerlänken "Företagsuppgifter" går till #foretagsuppgifter, där adress och telefon nu saknas.
  - Lägg till meningen "Fullständiga uppgifter med namn, adress och telefon finns på sidan Kontakt." och länka till /kontakt.

7. FÖRLANSERING
- vermo.se är publicerad med en äldre version. Förlanseringssidan visar kundservice@vermo.se, en adress som inte finns.
- Sätt PRELAUNCH = true i src/config/launch.ts.
  - När ägaren publicerar nästa gång visar vermo.se då bara förlanseringssidan, med info@vermo.se.
  - Förhandsvisningen och förhandsvisningskakan visar fortfarande hela butiken.
  - Vid lansering sätts PRELAUNCH = false igen.
- Publicera inte i den här ändringen.

KONTROLL INNAN DU ÄR KLAR
- Inga bilder med ask, kort eller engelsk text visas någonstans, varken i listor, sök, på produktsidan, i varukorgen eller i heron.
- Illustrationen visar rätt form, färg, berlock och band, med texten i Cormorant Garamond.
- Testa fyra varukorgar igen: Hjärtat Roséguldfärg med baksida, Familjen Guldfärg mars utan baksida, Vår dag Silverfärg med baksida och Pappa Guldfärg brunt band.
  - Variant, pris och attribut ska vara oförändrade.
- Svara med en kort lista över ändrade filer.
```

</details>

**2 okt, eftermiddag: rättelsen är klar, och nya önskemål från ägaren**
- **Rättelsen är genomförd** (6b55cfa) och granskad i diffen. Allt i planen är gjort:
  - vitlistade bild-id:n, med illustrationen som reserv
  - galleri
  - fristående SVG (hjärta, mynt med månadens berlock, bar, platta med band) i Cormorant Garamond
  - Great Vibes borttaget
  - ny hero och ny og:image
  - Familjens knapp
  - tecknen / : °
  - GPSR-raden
  - länk från köpvillkoren till Kontakt
  - Lovable har testat varukorgarna.
- **Ägarens egna ändringar:**
  - Heron är förenklad (333a46a).
  - **PRELAUNCH=false (c03c9ce).** Ägaren vill inte ha förlanseringsläget alls, så det slås aldrig på igen.
  - vermo.se visar fortfarande oktober-skärmen tills ägaren publicerar.
- **Ägarens svar:**
  - Nej till att byta variantbild i Shopify.
  - Nej till en rabattkod.
  - Ingen provbeställning, eftersom ägaren redan har ett prov.
- **Kassafelet "shop.vermo.se avvisade anslutningen":**
  - Shopify skickar `X-Frame-Options: DENY` och `frame-ancestors 'none'`.
  - I en vanlig flik går kassalänken till "Utcheckningskassa – Vermo" (HTTP 200, svenska). Lösenordet på temat stoppar alltså inte kassan.
  - Felet uppstår när kassan hamnar i Lovables förhandsvisning, som är en ram.
- **Runda 3 skickad** (umsg_01m3xxxsfhe9fvx1297nf9vg98). Lovable genomför direkt utan planrunda, enligt ägarens önskemål:
  - kassalänk: samma flik på sajten, ny flik i ram
  - tillverkare: Print-on-Demand B.V. (Ownprint), med Ownprints GPSR-uppgifter
  - AddToCartButton: laddning, cirkel med bock och skakning vid fel
  - pling på varukorgsikonen
  - bild-id:n per färg, med guld som reserv
- **Runda 3 är klar (b4377172), granskad och publicerad på vermo.se** (kontrollerat i CSS: cart-pling och add-to-cart-ring finns):
  - "Till kassan" är en riktig länk: samma flik på sajten, och ny flik bara när sajten visas i en ram.
  - Tillverkarraden är exakt enligt Ownprint. Ownprint och Print-on-Demand B.V. nämns i kundtext bara där, och i övrigt bara i AGENTS.md och roadmap.
  - AddToCartButton: ring, bock och skakning, med ett eget tillstånd vid reducerad rörelse.
  - Plinget styrs av `addedCount`, som inte sparas mellan sidladdningar.
  - Bild-id:n per färg med guld som reserv, och alt-texten anger bildens verkliga färg.
  - PRELAUNCH=false och regeln står i AGENTS.md.
  - Test 09.35: 92 av 92 variantkombinationer och fem varukorgar är OK.

<details><summary>Prompten för runda 3 (2 okt)</summary>

```text
Fyra ändringar från ägaren. Genomför dem direkt utan att vänta på att en plan godkänns, eftersom ägaren vill slippa det steget. Publicera inte.

VIKTIGT: Förlanseringsläget ska vara avstängt (PRELAUNCH = false). Ändra det aldrig och slå aldrig på det igen. Skriv in den regeln i AGENTS.md.

1. KASSAN: "SHOP.VERMO.SE AVVISADE ANSLUTNINGEN"
Shopifys kassa skickar X-Frame-Options: DENY och frame-ancestors 'none', så den får aldrig visas inuti en ram. Ägaren testar i Lovables förhandsvisning, som är en ram, och där blockeras kassan. I en vanlig flik fungerar kassalänken: den går till "Utcheckningskassa – Vermo" på svenska.
- Byt `window.open(checkoutUrl, "_blank", "noopener,noreferrer")` i varukorg.tsx mot en riktig länk (`<a href={checkoutUrl}>`), som ser ut som knappen gör i dag.
  - Vanlig flik (window.self === window.top): öppna kassan i samma flik. Det fungerar bäst på mobil och i Instagrams och TikToks inbyggda webbläsare.
  - Sajten visas i en ram, till exempel Lovables förhandsvisning: lägg till target="_blank" och rel="noopener", så att kassan alltid öppnas i en ny riktig flik och aldrig i ramen.
  - Avgör om sidan visas i en ram på klienten, efter mount, så att serverrenderingen inte bryts.
- Byt texten "Kassan öppnas säkert hos Shopify i en ny flik." mot "Du går vidare till Shopifys säkra kassa."
- Knappen är inaktiv så länge varukorgen uppdateras, som i dag.

2. TILLVERKARE = OWNPRINT (PRINT-ON-DEMAND B.V.)
Enligt Ownprints supportsida är Print-on-Demand B.V. ansvarig ekonomisk aktör enligt GPSR för allt de tillverkar. De anger uppgifterna nedan för butikerna.
- I supplier.ts, EU-profilen: ändra `safety.manufacturer` till exakt
  "Print-on-Demand B.V. (Ownprint), Groene Hilledijk 211A, 3073 AE Rotterdam, Nederländerna, compliance@print-on-demand-jewelry.eu, +31 85 888 2885"
- Det syns i den hopfällbara raden "Produktsäkerhet och tillverkare" på produktsidan och på /produktsakerhet.
  - På /produktsakerhet står Sitora kvar som säljare, med raden "Säljare: …".
  - Köpvillkor, Kontakt, kvitton och mejl ändras inte. Där är det Sitora som säljer.
- Ownprint och Print-on-Demand B.V. får nämnas bara i tillverkarraden. Ingen annanstans: inte i rubriker, produkttexter eller FAQ. Uppdatera regeln i AGENTS.md.
- CN-profilen är oförändrad.

3. KÖPKNAPPENS ANIMATION OCH VARUKORGENS "PLING"
Skapa en gemensam komponent, AddToCartButton, och använd den för både datorknappen och knappen i mobilens fasta köpfält. De ska dela samma tillstånd.
- **Vila:** "Lägg i varukorgen".
- **Laddar** (från klick tills addLine är klar):
  - Knappen behåller sin bredd.
  - Texten tonas ut och en liten roterande ring tonas in i mitten (SVG-cirkel med stroke-dasharray, rotate med keyframes).
  - aria-busy="true", och knappen är spärrad mot dubbelklick.
- **Klart:**
  - Ringen slutar snurra och sluts till en hel cirkel (stroke-dashoffset till 0, cirka 250 ms ease-out).
  - Sedan ritas en bock inuti cirkeln (stroke-dashoffset, cirka 300 ms).
  - "Tillagd" tonas in bredvid.
  - Efter cirka 1,4 sekunder glider knappen tillbaka till vila (cirka 300 ms).
- **Fel:** en kort skakning (translateX ±4 px, cirka 300 ms). Sedan vila, och felmeddelandet visas som i dag.
- **Varukorgsikonen** uppe till höger i sidhuvudet, vid varje lyckad tillägg, en gång per tillägg:
  - Ett "pling": ikonen studsar (scale 1 → 1,25 med −8° → 0,92 med 6° → 1,05 → 1, totalt cirka 600 ms).
  - En tunn ring expanderar och tonas ut bakom ikonen en gång.
  - Siffran poppar (scale 0,6 → 1,15 → 1).
  - Styr det med en räknare i varukorgen, till exempel `addedCount` som ökar vid varje lyckad addLine, så att animationen startar om varje gång.
- **60 FPS:** animera bara transform, opacity och stroke-dashoffset. Använd CSS keyframes och inga JS-loopar per bildruta. Lägg will-change bara på de animerade elementen.
- **Rörelsekänsliga** (prefers-reduced-motion): ingen rotation, studs eller skakning. Visa tillstånden direkt: texten "Lägger till …", bocken utan ritning och siffran utan pop.
- **Skärmläsare:** "Tillagd i varukorgen." ska fortfarande läsas upp (aria-live).

4. BILDER PER FÄRG (förbereds nu, ägaren skapar bilderna i Ownprint)
I dag visar alla bilder guldfärg. Ownprint kan skapa produktbilder även i silver och roséguld. Gör så här:
- Gör `imageIds` i productGroups.ts till en lista per färg: `{ guld: [...], silver: [], rose: [] }`. De nuvarande id:na hamnar under guld.
- Galleriet visar bilderna för vald färg. Saknas bilder för färgen visas guldbilderna.
  - Bildtexten blir då: "Bilderna visar guldfärg och exempeltext. Din färg och din text syns i illustrationen."
  - När det finns bilder i rätt färg: "Bilderna visar exempeltext. Din text syns i illustrationen."
- Alt-texten ska beskriva bildens verkliga färg, inte vald färg. I dag står det "i silverfärg" även på guldbilder.
- Produktlistor, sök och varukorg visar huvudbilden för vald färg, eller guld som reserv.
- Okända bilder visas fortfarande aldrig. Bara id:n i listorna gäller.

KONTROLL
- Testa i en vanlig flik att "Till kassan" går till Shopifys kassa, och i förhandsvisningen att kassan öppnas i en ny flik.
- Testa animationen på mobil och dator, och med prefers-reduced-motion.
- Testa fyra varukorgar igen: Hjärtat Roséguldfärg med baksida, Familjen Guldfärg mars, Vår dag Silverfärg med baksida och Pappa Guldfärg brunt band. Variant, pris och attribut ska vara oförändrade.
- Svara med en kort lista över ändrade filer.
```

</details>

**2 okt kl. 12: snyggare ångermejl (umsg_01m3y0jwj2e6j9mtqgn2mxw6xc)**
- **Problem:**
  - All text var guldbrun (#8A6A3B) på vit bakgrund.
  - I mörkt läge (ägarens webbmejl) blir bakgrunden grå medan texten förblir brun, så den blir svårläst.
  - Ingen logga och ingen struktur.
- **Beställt:**
  - En gemensam EmailLayout: color-scheme light, vitt kort på #F4EFE8 och ordmärket VERMO.
  - Brödtext i #1C1B19, 16 px, och guld bara som accent.
  - Referensen i en ruta och en sidfot med länkar.
  - En svensk version av Lovables avregistreringsrad, om det går.
  - Testanmälan till info@vermo.se, och testraden raderas efteråt.

**Att göra för ägaren (Shopify admin, efter claim)**
- Claima butiken senast ca 29 okt.
- Butiksnamn "Sitora".
- Aktivera Shopify Payments och Klarna.
- Policies i Shopify: klistra in texterna från `SHOPIFY-POLICYER.md`.
- Radera testprodukten före lansering.
- Skatter: slå på "Priser inkluderar moms" och lägg in svenskt momsregistreringsnummer.
- ~~Frakt: ta bort "Express 99 kr" om leverantören inte skickar express.~~ Klart 1 okt (via API).
- Domän: registrera sitora.se. Koppla den sedan i Lovable (egen domän och e-postdomän) för e-post som kundservice@sitora.se.

Att fylla i:
- bolagsuppgifter
- tillverkare och EU-ansvarig per produkt
- text till "Om Sitora"
- riktiga produktbilder (hero-bilden är AI-genererad med engelsk text)

**Efter första bygget**

1. Claima Shopify-sandboxbutiken som Lovable skapat. Detta måste göras inom 30 dagar.
2. Installera den valda leverantörens app och publicera produkterna därifrån.
3. Gör testordern i PLAN.md avsnitt 5. Byt sedan platshållarnycklarna i `attributeKeys` till leverantörens exakta nycklar och radera testprodukten.

---

```text
Bygg e-handelsbutiken för Sitora: personliga, graverade smycken för den svenska marknaden. All text på svenska. Nästan all trafik kommer från Instagram- och TikTok-annonser på mobil, så bygg mobil först.

## 1. Teknik (viktigt)
- Använd Lovables Shopify-integration: en headless butik där Shopify sköter checkout, betalning (Klarna, kort, Apple Pay), moms och order. Om ingen Shopify-butik är kopplad: skapa en ny sandbox-butik.
- De riktiga produkterna publiceras senare från leverantörens Shopify-app (Ownprint eller CJdropshipping, beslutas efter prover).
  - Skapa, ändra eller radera ALDRIG leverantörens produkter, varianter eller SKU:er, eftersom ordrarna då slutar gå automatiskt till fabriken.
  - Läs produkterna via Storefront API.
- Tills leverantörens produkter finns:
  - Använd tydligt markerad mockdata i koden.
  - Du får skapa EN testprodukt i Shopify, "TEST – Hjärthalsband (radera före lansering)", för att testa varukorg och checkout.
- Använd Lovable Cloud (databas, edge functions, e-post) för nyhetsbrev, ångerformulär och prislogg.

## 2. Leverantörsinställningar (ingen text får påstå något som inte stämmer)
Skapa src/config/supplier.ts med region: "EU" | "CN" (startvärde "EU").
- EU:
  - Produktion 2–5 arbetsdagar, frakt 1–10 arbetsdagar.
  - USP "Graveras och skickas från EU – inga tullavgifter".
  - Julklappsdeadline 2026-12-07 23:59.
- CN:
  - Produktion 1–3 dagar, frakt 9–18 dagar.
  - Ingen EU-USP.
  - Julklappsdeadline 2026-11-27 23:59.
All text om ursprung, leveranstid och julklappsdeadline på hela sajten ska hämtas härifrån.

## 3. Sortiment (priser sätts i Shopify, inte i koden)
- Hjärtat: graverat hjärthalsband med meddelandekort, 599 kr
- Familjen: mynt eller bar med barnens namn (+ födelsesten), 699 kr
- Vår dag: bar med datum eller koordinater, 599 kr
- Pappa: graverat armband eller nyckelring, 549 kr
- Tillval baksidesgravyr +99 kr. Digitala presentkort 300/500/700 kr.
Material: 18K guldpläterat rostfritt stål (även silver- och roséguldfärg).

## 4. Varumärke och design
- Känsla: premium, skandinavisk, varm och personlig. Absolut inte en "billig dropshipping-butik".
- Färger: bakgrund #FAF7F2, text #1C1B19, guld #B8925A, rosé #E9D9D0.
- Typsnitt: Cormorant Garamond (rubriker) och Inter (brödtext). För förhandsvisning av gravyr: Great Vibes (skrivstil) och Cormorant Garamond (rak).
- Stora bilder, mycket luft, tydliga knappar ("Skapa ditt smycke") och en sticky köpknapp på mobil. Mål: LCP under 2,5 s på mobil.

## 5. Sidor
1. Startsida:
   - Hero (bild eller video) med rubriken "Smycket hon aldrig tar av sig" (platshållare).
   - USP-rad: "Graverat efter din text · Presentask och meddelandekort ingår · Fri frakt", plus ursprungs-USP från supplier.ts.
   - Kampanjbanner som styrs av config.
   - "Handla efter mottagare": Mamma, Dotter, Partner, Syster/Vän, Pappa.
   - Bästsäljare, "Så funkar det" i tre steg, recensioner (endast verifierade köp), FAQ-utdrag och nyhetsbrev.
2. Kollektionssidor med filter för mottagare, färg och pris.
3. Produktsida med personaliserare (avsnitt 6).
4. Presentkort (Shopify gift card): "Låt mottagaren välja sin egen gravyr". Levereras direkt via e-post.
5. Om Sitora, FAQ och Kontakt.
6. Juridiska sidor: Köpvillkor, Leverans & reklamation, Integritetspolicy, Cookiepolicy, Produktsäkerhet och Ångra köp.

## 6. Personaliseraren (viktigast på hela sajten)
- Allt styrs per produkt från src/config/personalization.ts: vilka fält som finns (framsida, baksida, meddelandekort), max antal tecken och rader, om fältet är obligatoriskt eller valfritt, och eventuellt tilläggspris.
- Tillåtna tecken: A–Ö, a–ö, é, siffror, mellanslag och . , ! ? & - ' ♥. Validera direkt med ett tydligt felmeddelande. Å, Ä och Ö måste fungera överallt.
- Live-förhandsvisning: rendera texten som SVG ovanpå produktbilden i rätt form (hjärta, mynt, bar). Uppdatera medan kunden skriver. Liten text under: "Förhandsvisningen är en illustration."
- Meddelandekort: kunden väljer en mall – Till min dotter / Till min mamma / Till min fru / Till min syster / Till min bästa vän / Egen text. Mallen förifyller en redigerbar text (max 300 tecken) och kortet förhandsvisas.
- Baksidesgravyr som tillval (+99 kr) när produkten tillåter det.
- Obligatorisk kryssruta före "Lägg i varukorgen": "Jag har kontrollerat stavningen. Smycket tillverkas efter mina anvisningar och omfattas därför inte av ångerrätten. Blir det fel från er sida gör ni om det kostnadsfritt."
- Skicka alla val som cart line attributes via Storefront API, så att de hamnar som line item properties på Shopify-ordern.
  - Nyckelnamnen ska ligga samlade i config (attributeKeys) med platshållare, till exempel "Front Engraving", "Back Engraving" och "Message Card". Jag byter till leverantörens exakta nycklar efter en testorder.
  - Samma produkt med olika text blir separata rader i varukorgen.
- Visa personaliseringen i varukorgen, med möjlighet att ändra den.

## 7. Kampanjer och leveranslöfte (bara sanna uppgifter)
- src/config/campaign.ts styr aktuell fas (lansering, early-black-week, black-week, julklappsdeadline, presentkort), bannertexter och datum.
- Leveransberäkning från supplier.ts: räkna arbetsdagar med svenska helgdagar. Exempel: "Beställ idag – beräknad leverans 12–19 okt".
- Julklappsdeadline: nedräkning ENDAST till det verkliga datumet i supplier.ts. Efter deadline byter bannern automatiskt till presentkort.
- Paketpriset "2 för 999 kr" genomförs som en automatisk rabatt i Shopify på de vanliga produkterna, utan egna paket-SKU:er. Visa villkoren tydligt. Uppsäljning i varukorgen: "Lägg till ett till – 2 för 999 kr".
- Förbjudet på sajten:
  - överstrukna "ord. pris" eller "rek. pris" utan verklig prishistorik
  - påhittade rabattprocent
  - falska lagersaldon ("bara 2 kvar")
  - "X personer tittar nu"
  - påhittade recensioner
  - nedräkningar som startar om
- Prislogg:
  - En edge function sparar varje dag alla varianters pris i databasen.
  - En funktion returnerar lägsta pris de senaste 30 dagarna.
  - Om en produkt någon gång visar jämförpris ska det vara detta värde, märkt "Lägsta pris senaste 30 dagarna" (prisinformationslagen 7 a §).

## 8. Förtroende och konvertering
- Vid köpknappen: Klarna, Fri frakt, Presentask + kort ingår, Fri omgravering om vi gör fel, plus ursprungs-USP från supplier.ts.
- Plats för Klarnas meddelande om att betala senare.
- Recensioner: endast verifierade köp.
- Pop-up efter 15 sekunder eller vid exit intent, högst en gång per 7 dagar: "Få tidig tillgång till Black Week".
  - E-post, samtycke och tidsstämpel sparas i databasen.
  - Bekräftelse via e-post (dubbel opt-in).

## 9. Juridik (Sverige/EU)
- Footer och Kontakt: [Sitora AB], org.nr [XXXXXX-XXXX], adress, e-post och telefon (platshållare).
- Priser visas inklusive moms. Leveranstid och fraktkostnad syns före köp.
- Materialtext: "18K guldpläterat rostfritt stål".
  - Skriv aldrig "guld", "guldhalsband", "nickelfri" eller "hypoallergen".
  - Lägg till skötselråd och varningen "Innehåller smådelar – ej för barn under 3 år".
- Produktsäkerhet per produkt: tillverkare, EU-ansvarig, material och varningar (platshållare).
- Ångra köp (krav sedan 19 juni 2026):
  - En tydligt märkt länk i footern och i orderbekräftelsen leder till ett formulär: namn, e-post, ordernummer och vad som ångras.
  - Formuläret sparas i databasen och ett mottagningsbevis skickas via e-post.
  - Texten förklarar att personaliserade smycken är undantagna enligt 2 kap. 11 § distansavtalslagen, men att presentkort och icke-personaliserade varor omfattas.
  - Reklamationsrätt 3 år enligt konsumentköplagen.
- Cookie-banner med val: nödvändiga, statistik och marknadsföring.
  - Meta Pixel, TikTok Pixel och Google-taggar laddas först efter samtycke (Google Consent Mode v2).
  - Pixel-ID:n ligger i config.
- Skicka ViewContent, AddToCart och InitiateCheckout med event_id, för deduplicering mot servern. Purchase spåras av Shopifys Facebook & Instagram- och TikTok-appar.

## 10. SEO
Svenska titlar och metabeskrivningar, structured data (Product, Offer, Organization), sitemap, OG-bilder och snygga URL:er (/smycken/hjartat).

## Bygg i den här ordningen
1. Design, startsida och produktsida med personaliserare.
2. Shopify-koppling, varukorg och checkout med attributes.
3. Juridiska sidor, cookie-banner och ångerformulär.
4. Kampanj- och leverantörs-config, leveransberäkning, nyhetsbrev och prislogg.
Hinner du inte allt i ett svep: stanna efter ett avslutat steg och sammanfatta vad som är klart, vad som återstår och vad jag behöver fylla i.
```
