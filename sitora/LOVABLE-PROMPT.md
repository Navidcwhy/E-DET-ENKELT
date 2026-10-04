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
- **Klart (8f62061, 3,6 krediter) och granskat i diffen:**
  - EmailLayout med color-scheme light, vitt kort på #F4EFE8 och ordmärket VERMO med guldlinje.
  - Brödtext #1C1B19 i 16 px, och guld bara på etiketter och länkar.
  - Referensruta och sidfot med länkar.
  - Den interna notisen har raden "Svara på det här mejlet …".
  - Lovable har renderat mejlen i ljust och mörkt läge.
  - Två testmejl gick till info@vermo.se (ordernummer TEST-EMAIL-DESIGN), och testraden är raderad.
  - Lovables engelska avregistreringsrad går inte att ändra per mejl, så den är kvar.
  - PRELAUNCH=false.
  - Gäller på vermo.se när ägaren publicerar.

**2 okt kl. 13: runda 4, sex nya produkter och färgbilder (umsg_01m3y6gbx8edb9tt0kx93rysk6)**
- **Shopify:** de sex nya är publicerade till Lovable-kanalen (Namnet, Stjärntecknet, Initialen, Armringen, Pärlan, Nyckelringen).
- **Bilderna:** 206 bilder är klassade per färg och stil. Asken, kartongen, engelsk text och fel produkt är bortvalda.
- **Beställt i Lovable:**
  - produktgrupper med texter och mått
  - typsnitt per produkt (skrivstil för Namnet och Armringen)
  - nya former: vbar, tag, bangle och keyring
  - bild-id:n per färg
  - ett generellt valfält för Stjärntecken med radegenskapen "Stjärntecken"
  - previewOnly för Stjärntecknet
  - sitemap
- Inget publiceras.
- **Klart (7747c32, 12,7 krediter) och granskat i diffen:**
  - Alla bild-id:n per produkt och färg stämmer exakt mot listan. Asken, kartongen, engelsk text och Namnets bild 11 syns inte.
  - Texter, mått, mottagare och färger stämmer. Pärlan finns bara i guld och har en egen materialtext utan "hypoallergen".
  - Skrivstil (Great Vibes) för Namnet och Armringen. Nya former: vbar, tag, bangle och keyring.
  - Valfältet är generellt i personalization-konfigurationen:
    - Familjens månad styr varianten.
    - Stjärntecknet skickar radegenskapen "Stjärntecken" med exakt värde, t.ex. "Fiskarna/Pisces".
    - Varukorgen visar bara den svenska delen.
  - Stjärntecknet är dolt publikt: 404 på produktsidan, och den syns inte i listor, sök eller sitemap. Den syns i förhandsvisningen.
  - Startsidans rutnät visar nu bara de tre utvalda (Hjärtat, Familjen, Vår dag). "Se alla" leder till alla nio publika.
  - PRELAUNCH=false.
- **Testat via Storefront API med sajtens egen mappning:**
  - Alla 124 variantkombinationer gav rätt variant, 0 fel.
  - Sex testvarukorgar gav rätt pris och kassa på shop.vermo.se:
    - Namnet Roséguld med baksida, 499 kr
    - Stjärntecknet Silver "Fiskarna/Pisces", 499 kr
    - Initialen Guld, 449 kr
    - Armringen Silver, 499 kr
    - Pärlan Guld med baksida, 699 kr
    - Nyckelringen Rosé, 399 kr

<details><summary>Prompten för runda 4</summary>

```text
Sex nya produkter och bilder i alla färger. Genomför direkt utan planrunda och publicera inte. Ändra inte PRELAUNCH (false).

Alla nya produkter finns i Shopify och är publicerade till kanalen Lovable. De har samma upplägg som Hjärtat:
- varianter: "back engraving" (Without/With back engraving) × "plating" (Roséguldfärg/Guldfärg/Silverfärg)
- radegenskaper: "Front engraving text" (max 20) och "Back engraving text" (max 50)
- Pärlan finns bara i Guldfärg.
- Stjärntecknet har dessutom ett valfält, se nedan.

1. NYA PRODUKTGRUPPER (productGroups.ts, alla med fast-leverans EU)
Ordning på sajten: Hjärtat, Familjen, Vår dag, Namnet, Stjärntecknet, Initialen, Armringen, Pärlan, Pappa, Nyckelringen. Bestseller ändras inte (Hjärtat, Familjen, Vår dag).

a) Namnet: handle namnet-snabb-leverans
- tagline "Namnhalsband med ditt namn"
- beskrivning "En smal lodrät bar med ett namn i skrivstil – personligt och lätt att bära varje dag."
- mått ["Bar: 10 × 40 mm", "Kedja: 45 + 5 cm"]
- mottagare mamma, dotter, partner, syster-van
- färger silver, guld, rose
- framsida: etikett "Namn", hjälptext "Namnet graveras i skrivstil (max 20 tecken).", placeholder "T.ex. Sophia"
- form "vbar" (ny, lodrät bar 10 × 40)
- typsnitt i illustrationen: skrivstil

b) Stjärntecknet: handle stjarntecknet-snabb-leverans, previewOnly: true (se punkt 4)
- tagline "Mynt med stjärntecken och namn"
- beskrivning "Ett graverat mynt med ditt stjärntecken och ett namn."
- mått ["Mynt: 20 × 20 mm", "Kedja: 45 + 5 cm"]
- mottagare mamma, dotter, partner, syster-van
- färger silver, guld, rose
- framsida: etikett "Namn", hjälptext "Namnet graveras under stjärntecknet (max 20 tecken).", placeholder "T.ex. Elsa"
- form "coin" med stjärnteckenssymbolen (♈︎–♓︎ i textstil) ovanför namnet
- typsnitt rak antikva
- Galleriets bildtext: "Bilderna visar stjärntecknet Lejonet och exempeltext."

c) Initialen: handle initialen-snabb-leverans
- tagline "Bricka med en initial"
- beskrivning "En rektangulär bricka med en stor initial – enkel, tidlös och personlig."
- mått ["Bricka: 22 × 39 mm", "Kedja: 45 + 5 cm"]
- mottagare mamma, dotter, partner, syster-van, pappa
- färger silver, guld, rose
- framsida: etikett "Initial eller kort text", hjälptext "Graveras stort på brickan. En bokstav blir tydligast (max 20 tecken).", placeholder "A"
- form "tag" (ny, stående bricka 22 × 39 med avfasade hörn)
- typsnitt rak antikva

d) Armringen: handle armringen-snabb-leverans
- tagline "Armring med era initialer"
- beskrivning "En öppen armring med ett graverat mynt – era initialer i en dekorativ design."
- mått ["Armring: 6,5 × 5 cm (en storlek)", "Mynt: 20 mm"]
- mottagare partner, mamma, dotter, syster-van
- färger silver, guld, rose
- framsida: etikett "Initialer", hjälptext "T.ex. A & M. Graveras i en dekorativ design på myntet (max 20 tecken).", placeholder "A & M"
- form "bangle" (ny: tunn öppen båge med ett hängande mynt där texten står)
- typsnitt skrivstil

e) Pärlan: handle parlan-snabb-leverans
- tagline "Pärlarmband med graverat mynt"
- beskrivning "Pärlor och guldfärgade kulor med ett graverat mynt för en initial, ett datum eller ett namn."
- mått ["Armband: 18 cm + 5 cm förlängning", "Mynt: 20 mm", "Pärlor: 6 mm", "Kulor: 4 mm"]
- materialOverride "Pärlor av skalpulver (pärlemor). Kulor, kedja och mynt i rostfritt stål med 18K guldplätering. Vaxad bomullstråd i pärldelen."
- Skriv INTE "hypoallergen" eller "äkta pärlor".
- mottagare mamma, partner, syster-van, dotter
- färger bara guld
- framsida: etikett "Gravyr framsida", hjälptext "T.ex. en initial och ett datum (max 20 tecken).", placeholder "H 17.03.96"
- form "coin"
- typsnitt rak antikva

f) Nyckelringen: handle nyckelringen-snabb-leverans
- tagline "Graverad nyckelring"
- beskrivning "En hjärtformad nyckelring med era initialer – en vardaglig påminnelse."
- mått ["Hjärta: 20 × 25 mm", "Nyckelring: 4–5 cm"]
- mottagare pappa, partner
- färger silver, guld, rose
- framsida: etikett "Initialer eller kort text", hjälptext "T.ex. M ♥ J (max 20 tecken).", placeholder "M ♥ J"
- form "keyring" (ny: hjärta med en liten ring ovanför)
- typsnitt rak antikva

Baksidan för alla nya: samma som i dag (valfri hälsning, max 50 tecken, ingår).

2. TYPSNITT PER PRODUKT
- Lägg till `font: "serif" | "script"` per produkt. Standard är serif (Cormorant Garamond).
- Namnet och Armringen använder skrivstil. Ownprints design för dem är skriven skrivstil, enligt deras bilder.
- Ladda tillbaka Great Vibes från Google Fonts för det, med display=swap.

3. GODKÄNDA BILDER PER FÄRG (gid://shopify/ProductImage/<id>, i den här ordningen)
Befintliga guld-listor är oförändrade, utom för Pappa.
- hjartat: rose 100798222860678, 100798222827910, 100798222762374, 100798222795142 · silver 100798241046918, 100798241014150, 100798240948614, 100798240981382
- familjen: rose 100798284104070, 100798284005766, 100798284071302, 100798284038534, 100781280100742 · silver 100798292885894, 100798292787590, 100798292853126, 100798292820358, 100781280100742
- var-dag: rose 100798323655046, 100798323622278, 100798323556742, 100798323589510 · silver 100798333747590, 100798333714822, 100798333649286, 100798333682054
- pappa (ersätt guld-listan): guld 100781359071622, 100781358973318, 100781359006086, 100781359137158, 100781359104390 · silver 100781359038854, 100781359104390
- namnet: guld 100798383063430, 100798382965126, 100798382997894, 100798383030662 · rose 100798391714182, 100798391615878, 100798391681414 · silver 100798393155974, 100798393057670, 100798393090438, 100798393123206
- armringen: guld 100798565351814, 100798565319046 · rose 100798566269318, 100798566236550 · silver 100798566465926, 100798566433158
- initialen: guld 100798575640966, 100798575608198, 100798575542662, 100798575575430 · rose 100798576624006, 100798576591238, 100798576525702, 100798576558470 · silver 100798576886150, 100798576853382, 100798576787846, 100798576820614
- nyckelringen: guld 100798628594054, 100798628561286 · rose 100798632198534, 100798632165766 · silver 100798632427910, 100798632395142
- parlan: guld 100798656086406, 100798656217478, 100798656184710, 100798656250246, 100798656119174, 100798656283014
- stjarntecknet: guld 100798946345350, 100798946247046, 100798946312582, 100798946279814 · rose 100798954537350, 100798954439046, 100798954504582, 100798954471814 · silver 100798954799494, 100798954701190, 100798954766726, 100798954733958

Alla andra bilder ska fortsätta vara dolda:
- asken
- kartongen
- engelsk text
- Namnets bild 11, som visar fel produkt

Galleriet byter nu till rätt färg när kunden väljer färg.

4. STJÄRNTECKNET: VALFÄLT OCH FÖRHANDSVISNINGSLÄGE
Valfältet:
- Obligatoriskt fält "Stjärntecken" med en tom startrad "Välj stjärntecken".
- Alternativen ska visas med svenskt namn och datum. Värdet som skickas ska vara EXAKT värdet till höger:
  Väduren (21 mars–19 april) = "Väduren/Aries"
  Oxen (20 april–20 maj) = "Oxen/Taurus"
  Tvillingarna (21 maj–20 juni) = "Tvillingarna/Gemini"
  Kräftan (21 juni–22 juli) = "Kräftan/Cancer"
  Lejonet (23 juli–22 augusti) = "Lejonet/Leo"
  Jungfrun (23 augusti–22 september) = "Jungfrun/Virgo"
  Vågen (23 september–22 oktober) = "Vågen/Libra"
  Skorpionen (23 oktober–21 november) = "Skorpionen/Scorpio"
  Skytten (22 november–21 december) = "Skytten/Sagittarius"
  Stenbocken (22 december–19 januari) = "Stenbocken/Capricorn"
  Vattumannen (20 januari–18 februari) = "Vattumannen/Aquarius"
  Fiskarna (19 februari–20 mars) = "Fiskarna/Pisces"
- Skicka det som radegenskap med nyckeln EXAKT "Stjärntecken". Det är Ownprints fältnamn.
- Varukorgen visar etiketten "Stjärntecken" och bara den svenska delen.
- Köpknappen beter sig som för Familjens månad: "Välj stjärntecken" tills ett tecken är valt.
- Lös det generellt, med ett valfritt valfält per produkt i personalization-konfigurationen, inte som specialfall i koden.

Förhandsvisningsläget:
- previewOnly: true betyder att produkten bara visas när showPreviewOptions är sant (Lovables förhandsvisning eller kakan ?preview=vermo2026).
- Publikt syns den inte i listor, sök, sitemap eller som produktsida (404).
- Det här påverkar INTE förlanseringsläget. PRELAUNCH ska vara false.
- Orsak: vi väntar på att Ownprint bekräftar att de graverar det stjärntecken kunden väljer.

5. SITEMAP OCH LISTOR
- Lägg till de nya produktsidorna i sitemap.xml, utom de med previewOnly.
- Mottagarfilter, sök och startsidans lista tar med de nya automatiskt.

KONTROLL
Testa varukorgar via sajtens egen kod:
- Namnet Roséguldfärg med baksida
- Stjärntecknet Silverfärg, Fiskarna (kontrollera att radegenskapen "Stjärntecken" = "Fiskarna/Pisces")
- Initialen Guldfärg
- Armringen Silverfärg
- Pärlan Guldfärg med baksida
- Nyckelringen Roséguldfärg

Alla ska ge rätt variant och pris (499/499/449/499/699/399). De fyra befintliga ska vara oförändrade.

Kontrollera också:
- Galleriet byter bilder när färgen byts.
- Inga bilder med ask eller kort syns någonstans.

Svara med en kort lista över ändrade filer.
```

</details>

**2 okt kl. 14: runda 5, rester på live-sajten före annonserna (umsg_01m3y7mjmjfqsrajepmcyewe6y)**
- **Hittat vid genomsökning av vermo.se** (fanns före runda 4, mitt förbiseende i de första promptarna):
  - Startsidan:
    - rubriken "Bästsäljare" utan en enda försäljning
    - platshållaren "[Anmälan kopplas till databasen i steg 4.]"
    - metabeskrivningen "två leveransval", fast bara snabb leverans är på
  - Presentkort i menyn leder till en sida som inte går att köpa från, med "[Presentkorten kopplas till Shopifys gift cards i steg 2.]".
  - Om Vermo visar "UTKAST – granskas".
  - Produktsäkerhet:
    - Listan skulle visa det dolda Stjärntecknet.
    - Pärlans material saknas.
  - Integritetspolicyn nämner "korttexter".
- **Beställt:**
  - "Våra favoriter" i stället för "Bästsäljare"
  - nyhetsbrevet kopplat till den befintliga tabellen, med ett nytt samtycke
  - sann metabeskrivning
  - Recensioner dolda tills det finns verifierade recensioner
  - Presentkort ur menyer och sitemap, med tillfällig vidarekoppling till /smycken
  - utkastetiketten borttagen
  - Produktsäkerhet rättad
  - texträttelser
- Inget publiceras.
- **Klart (d892d92, 5,4 krediter) och granskat i diffen:**
  - "Våra favoriter".
  - Nyhetsbrevet:
    - Ny konstant NEWSLETTER_CONSENT_TEXT, och samma text sparas i consent_text.
    - source "startsida". Tabellens kontroll av source utökades med en migration.
    - Fälten har unika id.
    - Lovable testade en anmälan och raderade testraden.
  - Metabeskrivningen och steg 1 i "Så funkar det" är rättade.
  - REVIEWS_ENABLED=false.
  - Presentkort är borttaget ur menyerna, sidfoten och sitemap, och /presentkort ger 307 till /smycken.
  - "UTKAST" är borta.
  - Produktsäkerhet: previewOnly filtreras bort, och Pärlans material har en egen rad.
  - "gravyrtexter" och "normalt samma arbetsdag".
  - PRELAUNCH=false. Inga produkter, bilder eller priser ändrades.

<details><summary>Prompten för runda 5</summary>

```text
Små rättelser före annonserna. Genomför direkt utan planrunda och publicera inte. Ändra inte PRELAUNCH (false), produktkonfigurationen, bilderna eller priserna.

1. STARTSIDAN
a) Byt rubriken "Bästsäljare" till "Våra favoriter".
- Butiken har ännu ingen försäljning, så "Bästsäljare" är ett påstående vi inte kan belägga.
- Flaggan bestseller ligger kvar i koden och styr urvalet.

b) Nyhetsbrevet: ersätt platshållaren "[Anmälan kopplas till databasen i steg 4.]" med den befintliga komponenten NewsletterSignup (tabellen newsletter_signups).
- Rubrik: "Nyhetsbrev"
- Text: "Nya smycken och erbjudanden. Ett mejl då och då, inget mer."
- Samtyckestext, som en ny konstant och inte PRELAUNCH_CONSENT_TEXT: "Ja, jag vill få Vermos nyhetsbrev med nyheter och erbjudanden. Jag kan avregistrera mig när som helst."
- Spara exakt den visade samtyckestexten i consent_text, och source "startsida".
- Bekräftelsen efter anmälan:
  - rubrik "Tack för din anmälan"
  - text "Du kan avregistrera dig när som helst genom att mejla info@vermo.se."
  - Texten "Du får information när Vermo öppnar" ska bort.
- Fältens id ska vara unika på sidan och får inte börja med "prelaunch-".
- Testa att en anmälan sparas och radera testraden efteråt.

c) Metabeskrivningen säger "två leveransval", men bara snabb leverans är på. Ny text: "Personliga graverade smycken från Vermo. Skapa en unik gåva med din egen text – fri frakt och gravyr på baksidan ingår."

d) "Så funkar det", steg 1: "Halsband, armband eller nyckelring – i guld-, silver- eller roséguldfärg."

e) Dölj sektionen "Recensioner" tills det finns verifierade recensioner, med en flagga i config: REVIEWS_ENABLED = false.

2. PRESENTKORT (de går inte att köpa än)
- Ta bort "Presentkort" från huvudmenyn, mobilmenyn och sidfoten.
- Ta bort /presentkort från sitemap.xml.
- /presentkort ska tillfälligt skicka vidare till /smycken med 302 eller 307, inte 301.
- Behåll sidans kod och beloppen till senare.
- Texterna om presentkort och ångerrätt i villkoren och FAQ ändras inte.

3. OM VERMO
- Ta bort introt "UTKAST – granskas" och ersätt det med "Personliga, graverade smycken."
- Brödtexten är godkänd som den är.

4. PRODUKTSÄKERHET
- "Gäller smyckena": visa inte produkter med previewOnly publikt. Det är samma regel som i listor och sök.
- Byt "Material för halsbanden" mot "Material för halsband, armring och nyckelring".
- Lägg till en rad per produkt som har materialOverride i productGroups, t.ex. "Pärlan: Pärlor av skalpulver (pärlemor). …". Det kommer utöver Pappa-raden och utan dubbletter.

5. SMÅ TEXTER
- Integritetspolicyn: byt "gravyr- och korttexter" mot "gravyrtexter" på båda ställena. Kunderna skriver inga korttexter.
- FAQ: byt "Hör av dig så svarar vi samma arbetsdag." mot "Hör av dig så svarar vi normalt samma arbetsdag.", samma formulering som på Kontakt.

KONTROLL
- Sök igenom koden efter text som syns för kunder och som står inom hakparenteser, eller innehåller UTKAST, TILLFÄLLIG, PLATSHÅLLARE, "steg 2" eller "steg 4".
- Lista allt som fortfarande kan visas publikt. Ändra inget utöver punkterna ovan.
- Svara med en kort lista över ändrade filer.
```

</details>


**2 okt kl. 14.15: runda 6, annonsspårning (umsg_01m3y8h4g8fnpaenae84hag8x1)**
- **Läget i Shopify, avläst via API:t och butikens sidkod:**
  - TikTok är kopplat. Apppixeln DAVPCUBC77UD1K9H6HKG har datadelningen "optimized" och rapporterar kassan och köpen.
  - **Meta är inte kopplat än.** Ingen Meta-pixel finns i butikens pixellista, och facebookCapiEnabled är false.
  - Shopify kräver samtycke för Sverige (consentPolicy SE: consentRequired true). Utan överfört samtycke skickar kassan inga köp till TikTok och Meta.
  - Butiken har fortfarande lösenord. Alla shop.vermo.se-adresser går till /password, och temat skickar sedan alla till startsidan. Produkterna saknar därför onlineStoreUrl, och katalogerna saknar alltså produktlänkar.
  - Kassan fungerar. Med vanliga webbläsarhuvuden går kedjan cart/c → shop.app → shop.vermo.se/checkouts/cn och ger 200. Utan dem hamnar curl på /password, vilket inte gäller riktiga besökare.
- **Gjort via API:t:** de fem nya publika produkterna är publicerade till Facebook & Instagram och TikTok, utom Stjärntecknet. Nu ligger alla nio publika där.
- **Beställt i Lovable:**
  - TikTok-pixeln och Meta-pixeln, som är avstängd tills id:t finns. De laddas bara efter samtycke till marknadsföring och bara på vermo.se.
  - setTrackingConsent till Shopify med headlessStorefront, checkoutRootDomain shop.vermo.se och storefrontRootDomain vermo.se.
  - Händelserna PageView, ViewContent och AddToCart med variant-id. Inga kassa- eller köphändelser, eftersom apparna redan skickar dem.
  - 301 från Shopifys sökvägar (/products/<handle> → /smycken/<slug> m.fl.) med bevarade query-parametrar.
  - En kaklista i cookiepolicyn.
- **Efter publicering:**
  - Temainställningen "External Redirect": storefront_hostname "vermo.se" och custom_redirects "/>/", så att sökvägen följer med. Görs via API:t (write_themes finns).
  - Ägaren tar bort lösenordet.
- **Klart (bb827b0, 5,6 krediter) och granskat i diffen:**
  - Ny src/lib/tracking.ts:
    - Pixlarna laddas bara efter samtycke till marknadsföring och bara på vermo.se och www.vermo.se. Ett PLACEHOLDER-id stänger av pixeln.
    - fbq consent grant/revoke och ttq grantConsent/revokeConsent.
    - setTrackingConsent med headlessStorefront, shop.vermo.se, vermo.se och den publika token, vid varje sparat eller inläst val.
  - Händelserna:
    - PageView via PageViewTracker i __root, en gång per adress.
    - ViewContent på produktsidan.
    - AddToCart i cart.tsx efter lyckad läggning, med variant-id som siffror och event-id.
    - Inga kassahändelser och ingen gravyrtext.
  - Serverrutter ger 301 för /products/<handle> (Stjärntecknet publikt → /smycken), /collections, /cart, /password, /pages, /account och /policies/*. Query-parametrarna följer med, enligt Lovables test på localhost.
  - Cookiepolicyn har en lista över kakorna.
- **Två brister rättas i runda 7:**
  - ViewContent tappas för landningssidan när samtycket ges först där.
  - Nytt samtycke efter återkallat samtycke anropade inte grant igen.

<details><summary>Prompten för runda 6</summary>

```text
Spårning för annonser (TikTok och Meta) och samtycke till Shopify-kassan. Genomför direkt utan planrunda och publicera inte. Ändra inte PRELAUNCH (false), produkterna, bilderna, priserna eller andra texter än de som står här.

BAKGRUND
- TikTok är kopplat i Shopify med pixel-id DAVPCUBC77UD1K9H6HKG. Meta kopplas inom kort, och id:t kommer senare.
- Shopifys TikTok- och Meta-appar rapporterar redan kassa, betalning och köp från kassan på shop.vermo.se.
  - Sajten ska därför INTE skicka InitiateCheckout, AddPaymentInfo, CompletePayment eller Purchase, eftersom det skulle dubbelräkna.
- Shopify kräver samtycke för svenska besökare. Kassan skickar köphändelser bara om besökarens samtycke från vermo.se förs över till Shopify (punkt 3).

1. PIXEL-ID (tracking i src/config/campaign.ts)
- tiktokPixelId = "DAVPCUBC77UD1K9H6HKG"
- metaPixelId och googleTagId är kvar som platshållare.
- Ett id som börjar med "PLACEHOLDER" betyder att pixeln är avstängd, och inget skript laddas för den.

2. SAMTYCKET STYR PIXLARNA
- Meta- och TikTok-skripten laddas först när besökaren har samtyckt till Marknadsföring i cookierutan, dvs. befintliga CookieConsent och händelsen sitora:consent-updated.
- Läs också det sparade samtycket när sidan startar.
- Före samtycke får det inte finnas något skript, någon kaka eller något anrop till Meta eller TikTok.
- Om besökaren återkallar samtycket:
  - Skicka inga fler händelser (Meta: fbq('consent', 'revoke'), TikTok: ttq.revokeConsent()).
  - Ladda inte skripten vid nästa sidvisning.
- Pixlarna skickar bara på vermo.se och www.vermo.se. På andra adresser, t.ex. Lovables förhandsvisning, laddas inga pixlar, och varje händelse loggas i stället i konsolen med sina parametrar (för test).

3. SAMTYCKET TILL SHOPIFY-KASSAN (viktigast)
- Ladda Shopifys Customer Privacy API: https://cdn.shopify.com/shopifycloud/consent-tracking-api/v0.1/consent-tracking-api.js
  - Det är en nödvändig funktion, eftersom det bara sparar besökarens val. Därför får det laddas oavsett val.
  - Bara på vermo.se och www.vermo.se. På andra adresser loggas anropet i konsolen.
- Varje gång samtycket sparas, eller läses in vid start (även "Endast nödvändiga"), anropa:
  window.Shopify.customerPrivacy.setTrackingConsent({
    analytics: <Statistik>,
    marketing: <Marknadsföring>,
    preferences: <Statistik>,
    sale_of_data: <Marknadsföring>,
    headlessStorefront: true,
    checkoutRootDomain: "shop.vermo.se",
    storefrontRootDomain: "vermo.se",
    storefrontAccessToken: <den befintliga publika Storefront-token>
  }, callback)
- Vänta tills skriptet har laddats. Ett fel här får aldrig stoppa sidan, cookierutan eller köpet.

4. HÄNDELSER FRÅN SAJTEN (bara efter samtycke)
- PageView: vid varje sidvisning, även vid sidbyte i appen. Den första laddningen räknas bara en gång.
- ViewContent: på produktsidan, en gång per produkt och sidvisning (inte vid färgbyte).
- AddToCart: när varan faktiskt ligger i varukorgen, samtidigt som plinget, inte vid klick.
- Parametrar:
  - Meta: content_ids [variant-id], content_type "product", content_name (produktens namn, t.ex. "Hjärtat"), value (pris i kronor inkl. moms × antal), currency "SEK".
  - TikTok: contents [{ content_id: variant-id, content_type: "product", content_name, quantity, price }], value, currency "SEK".
  - Variant-id är siffrorna i Shopifys gid (gid://shopify/ProductVariant/123 → "123"). Lägg formateringen i en enda funktion, så att den lätt kan ändras.
  - Varje händelse får ett unikt event-id (Meta: { eventID }, TikTok: { event_id }).
- Skicka aldrig gravyrtexter, stjärntecken, e-post eller andra personuppgifter till Meta eller TikTok.
- previewOnly-produkter skickar inga händelser.

5. PRODUKTLÄNKAR FRÅN SHOPIFY
Meta- och TikTok-katalogerna länkar till shop.vermo.se/products/<handle>. Den adressen ska skickas vidare till vermo.se med samma sökväg. Lägg till permanenta omdirigeringar (301) på sajten. Query-parametrar, t.ex. fbclid, ttclid och utm_*, ska alltid följa med.
- /products/<handle> → /smycken/<slug> för den produktgrupp som har det handle:t, t.ex. hjartat-snabb-leverans → /smycken/hjartat.
  - Okänt handle eller previewOnly-produkt (publikt) → /smycken.
- /collections och /collections/<allt> → /smycken
- /cart → /varukorg
- /password, /pages/<allt>, /account och /account/<allt> → /
- /policies/refund-policy och /policies/shipping-policy → /leverans-och-reklamation
- /policies/privacy-policy → /integritetspolicy
- /policies/terms-of-service och /policies/legal-notice → /kopvillkor
- /policies/contact-information → /kontakt
- Lägg inte till dem i sitemap.xml.

6. COOKIEPOLICYN
Komplettera med en kort lista över kakor, med namn, syfte och lagringstid:
- Nödvändiga:
  - Shopify _tracking_consent: sparar ditt samtyckesval så att kassan respekterar det, 1 år.
  - Vermos cookieval i webbläsaren.
- Marknadsföring:
  - Meta _fbp och _fbc: mäter annonser och visar relevanta annonser, 90 dagar.
  - TikTok _ttp och _tt_enable_cookie: samma syfte, upp till 13 månader.
Övrig text ändras inte.

KONTROLL
- I förhandsvisningen:
  - Inga anrop till facebook.net, facebook.com eller tiktok.com, varken före eller efter samtycke.
  - Efter "Acceptera alla" loggas PageView, ViewContent och AddToCart med rätt parametrar i konsolen.
  - setTrackingConsent loggas med rätt värden.
- /products/hjartat-snabb-leverans?fbclid=test ska ge 301 till /smycken/hjartat?fbclid=test.
- /products/stjarntecknet-snabb-leverans ska publikt ge 301 till /smycken.
- Svara med en kort lista över ändrade filer.
```

</details>

**2 okt kl. 14.25: runda 7, Meta-pixeln och villkoren från Shopify (umsg_01m3y96gnmf1pbemzfw0yg050r)**
- **Meta är kopplat av ägaren.** Shopifys pixellista visar facebook_pixel 1042319362191805 (appen Facebook & Instagram), datadelningen "optimized" och facebookCapiEnabled true.
- **Ägarens önskemål:** "Lägg även in alla villkor till Lovable". Sajtens villkorssidor ska visa exakt Shopifys policytexter, dvs. samma som kassan länkar till.
  - Sidorna hämtar texterna via Storefront API (shop.termsOfService, shippingPolicy, refundPolicy och privacyPolicy fungerar med den publika token; testat 2 okt).
  - Då behöver texterna bara ändras på ett ställe: i Shopify.
  - Legal notice och kontaktinformation finns inte i Storefront API. De finns redan på sajten via company-config, under Kontakt och Företagsuppgifter.
- **Beställt:**
  - metaPixelId.
  - ViewContent när samtycket ges på produktsidan.
  - grant igen efter återkallat samtycke.
  - /kopvillkor, /leverans-och-reklamation och /integritetspolicy renderar Shopify-texterna: rubrikrader som h2, "– " som punktlista, bara säkra taggar, 10 minuters cache och reservlänkar till Shopifys policysidor.
- **Ägaren:** klistra in integritetspolicyn igen i Shopify. Där står fortfarande "Gravyr- och korttexter". Rätt text finns i SHOPIFY-POLICYER.md.
- **Klart (0b4149f, 4,6 krediter), granskat i Lovables logg:**
  - metaPixelId är satt.
  - ViewContent lyssnar på sitora:consent-updated och skickas en gång per produktvisning. trackEvent returnerar om händelsen skickades.
  - loadMeta och loadTiktok anropar grant igen efter återkallat samtycke.
  - Ny src/lib/policies.functions.ts:
    - En serverfunktion med 10 minuters cache. Vid fel används senaste cachen.
    - Sanering med tillåtna taggar och säkra länkar. Webbadresser görs klickbara, och externa länkar öppnas i ny flik.
    - Rubrikrader blir h2 och "– " blir punktlista.
  - Ny src/components/site/ShopifyPolicy.tsx med reservlänkar.
  - /kopvillkor visar ToS, med Företagsuppgifter (#foretagsuppgifter) sist. /leverans-och-reklamation visar frakt och ångerrätt/reklamation. /integritetspolicy visar integritetstexten och en länk till cookiepolicyn.
  - Testat: inga anrop till facebook eller tiktok i förhandsvisningen, en PageView och en ViewContent efter samtycke, grant efter nytt samtycke, och rubriker och listor syns.
- **Publicerat av ägaren den 2 okt, ca 14.40. Live-verifiering i Chromium via proxyn:**
  - Shopify-vägarna /products/hjartat-snabb-leverans?fbclid=test, /collections/all, /cart, /password och /policies/refund-policy ger 301 till rätt sida, och /presentkort ger 307.
  - Startsidan visar "Våra favoriter" och Nyhetsbrev.
  - Villkorssidorna visar Shopify-texterna, inklusive Reklamation, Tvist och Gravyrtexter.
  - Pixlarna och samtycket (se LANSERING.md, punkt 6):
    - Inget anrop före samtycke.
    - Efter samtycke: PageView, ViewContent och AddToCart till Meta och TikTok, samt Shopifys consentManagement.
    - _tracking_consent och _fbc sätts på .vermo.se.
  - Mitt testbesök (fbclid=CLAUDETEST123, amerikansk IP) syns som några händelser hos Meta och TikTok.
- **Temat:** Shopify-kopplingen får inte skriva till det publicerade temat. Därför finns en kopia, "External Redirect – vermo.se" (gid://shopify/OnlineStoreTheme/210954158470), med storefront_hostname "vermo.se" och custom_redirects "/>/".
  - Den förhandsvisas korrekt: canonical https://vermo.se/products/…, och den simulerade omdirigeringen går till vermo.se med samma sökväg och query.
  - Ägaren publicerar den.
- **Lovables notering:** ägarens namn, adress och telefon syns nu i villkoren, eftersom de står i Shopify-texterna.
  - De fanns redan på sajten under Kontakt, Ångra köp, Produktsäkerhet och Integritetspolicy.
  - Säljarens namn, adress och kontaktuppgifter ska enligt e-handelslagen vara lätt åtkomliga. Ingen ändring behövs.

<details><summary>Prompten för runda 7</summary>

```text
Meta-pixeln, två rättelser i spårningen och villkoren från Shopify. Genomför direkt utan planrunda och publicera inte. Ändra inte PRELAUNCH (false), produkterna, bilderna eller priserna.

1. META-PIXELN
- I tracking i src/config/campaign.ts: metaPixelId = "1042319362191805".
- Allt annat gäller som för TikTok: laddas bara efter samtycke till marknadsföring, bara på vermo.se och www.vermo.se, och inga kassa- eller köphändelser från sajten.

2. RÄTTELSER I src/lib/tracking.ts OCH PRODUKTSIDAN
a) ViewContent på landningssidan
- I dag tappas ViewContent för produktsidan besökaren landar på, om samtycket ges först när hen redan är på sidan. Det gäller de flesta som kommer från annonser.
- Om samtycket till marknadsföring ges medan besökaren är kvar på en produktsida, skicka ViewContent för den produkten en gång, på samma sätt som PageView redan gör.
- Ingen dubbel ViewContent för samma produktvisning.

b) Nytt samtycke efter återkallat samtycke
- Om besökaren återkallar och sedan ger samtycke igen under samma besök, anropa fbq('consent', 'grant') och ttq.grantConsent() igen.
- I dag görs det bara vid första laddningen.

3. VILLKOREN DIREKT FRÅN SHOPIFY (en enda källa)
Shopifys policyer är de som visas i kassan. Sajten ska visa exakt samma texter, så att de aldrig skiljer sig. Hämta dem via Storefront API på servern (SSR):
shop { termsOfService { title body url } shippingPolicy { title body url } refundPolicy { title body url } privacyPolicy { title body url } }
- Använd @inContext(country: SE, language: SV).
- Cacha på servern i högst 10 minuter.

Sidor (adresser, rubriker och sidfotens länkar är oförändrade):
- /kopvillkor: termsOfService.
  - Behåll avsnittet Företagsuppgifter med id "foretagsuppgifter", hämtat från company-config, sist på sidan. Sidfotens länk dit ska fungera.
- /leverans-och-reklamation: shippingPolicy, med underrubriken "Frakt och leverans". Därefter refundPolicy, med underrubriken "Ångerrätt, reklamation och återbetalning".
- /integritetspolicy: privacyPolicy. Sist kommer raden "Om kakor och pixlar: se vår cookiepolicy." med en länk till /cookiepolicy.
- /angra-kop, /cookiepolicy, /produktsakerhet och /kontakt behåller sitt nuvarande innehåll.

Visning av Shopify-texten:
- Shopifys body är HTML där varje stycke börjar med en kort rubrikrad följd av <br>, t.ex. "<p>Ångerrätt<br>Personligt graverade …</p>".
  - Visa rubrikraden som en h2 i samma stil som i dag, och resten som brödtext.
  - Rader som börjar med "– " visas som punktlista.
- Tillåt bara enkla taggar: p, br, a, strong, em, ul, ol, li, h2 och h3. Ta bort allt annat. Länkar till andra webbplatser öppnas i ny flik med rel="noopener noreferrer".
- Webbadresser i texten som inte redan är länkar (t.ex. www.arn.se, www.imy.se, https://privacy.shopify.com) görs klickbara.
- Om hämtningen misslyckas visas texten: "Villkoren kunde inte laddas just nu. De finns också här:" med en länk till Shopifys sida för respektive policy:
  - Köpvillkor: https://checkout.shopify.com/110903558534/policies/69404524934.html?locale=sv
  - Frakt: https://checkout.shopify.com/110903558534/policies/69403312518.html?locale=sv
  - Ångerrätt och reklamation: https://checkout.shopify.com/110903558534/policies/69403246982.html?locale=sv
  - Integritet: https://checkout.shopify.com/110903558534/policies/69319131526.html?locale=sv
- Metatitlar och metabeskrivningar på sidorna ändras inte.

KONTROLL
- I förhandsvisningen:
  - Inga anrop till facebook eller tiktok.
  - Efter "Acceptera alla" på en produktsida loggas PageView och ViewContent en gång var.
  - Återkalla och ge samtycke igen: grant loggas.
- De tre villkorssidorna visar Shopifys texter med rubriker och punktlistor. Kontrollera t.ex. att "Reklamation" och "Tvist" finns på /leverans-och-reklamation.
- Länken till /kopvillkor#foretagsuppgifter fungerar.
- Svara med en kort lista över ändrade filer.
```

</details>

**4 okt kl. 13.54: runda 8, julklappsraden vid köpknappen (umsg_01m43c82gjf64vb4h363b86amc)**
- **Varför:** annonserna och filmerna säger "Beställ senast 7 december för leverans före jul", men produktsidan nämnde inte datumet. Claude Desktop upptäckte det vid granskningen i Ads Manager.
- **Klart (4d3cb1d, 2,1 krediter), granskat i diffen:**
  - delivery.ts har två nya funktioner:
    - christmasDeadlineLabel(profile) ger "7 december", hämtat från christmasDeadline i supplier.ts.
    - showChristmasDeadlineNote(profile, now) avgör om raden visas.
  - Raden visas bara om tre villkor gäller:
    - Leveransprofilen är aktiv.
    - Deadline har inte passerat.
    - Sajtens egen beräkning, estimateDelivery().latest, blir senast 23 december.
  - Villkoren kontrolleras när sidan visas, så raden försvinner utan ny publicering.
  - Placering och utseende:
    - På dator ligger raden under pris och köpknapp. På mobil ligger den i den fasta köpraden.
    - Texten är text-xs med en presentikon i accent-strong.
    - Den ryms på en rad vid 360 px: ca 282 av 296 px.
  - Lovable testade i Playwright vid 1280, 390 och 360 px.
- **Rättelse (0dd1d8f, 1,5 krediter):**
  - Problemet: den högre köpraden dolde sidfotens Företagsuppgifter och copyright-rad på mobil. Den gamla h-20 i Personalizer hjälpte inte, eftersom sidfoten kommer efter den.
  - Lösningen: köpraden har nu attributet data-mobile-buy-bar, och body får padding-bottom 6rem under lg när köpraden finns. Den gamla h-20 är borttagen.
  - Verifierat vid 390 och 360 px.
- **Obs:** med nuvarande ledtid (högst 15 arbetsdagar) döljs raden från 3 december. Se "Bekräfta julklappsdeadline" i LANSERING.md.
- **Ägaren publicerar.**

<details><summary>Prompterna för runda 8</summary>

```text
Julklappsraden vid köpknappen. Genomför direkt utan planrunda och publicera inte. Ändra inte PRELAUNCH (false), produkterna, bilderna, priserna, värdena i src/config/supplier.ts eller kampanjfasen.

BAKGRUND
Annonserna säger "Beställ senast 7 december för leverans före jul". Produktsidan ska säga samma sak vid köpknappen, så att besökaren känner igen löftet.

1. RADEN
- Text: "Beställ senast 7 december för leverans före jul."
- Datumet hämtas från christmasDeadline i den valda leveransprofilen i src/config/supplier.ts. Formatera det som i DeliveryOptionsInfo (sv-SE, dag och månad, Europe/Stockholm). Skriv inget datum i koden.
- Lägg logiken i src/lib/delivery.ts, t.ex. christmasDeadlineLabel(profile) och showChristmasDeadlineNote(profile, now).

2. NÄR RADEN VISAS (alla villkor måste gälla)
- Den valda leveransprofilen är aktiverad (enabled).
- Deadline har inte passerat (samma kontroll som isPastChristmasDeadline).
- Sajtens egen leveransberäkning för en beställning i dag, estimateDelivery(profile).latest, blir senast 23 december samma år. Annars skulle raden motsäga "beräknad leverans" på samma sida.
- Kontrollen görs när sidan visas, inte vid bygget, så att raden försvinner av sig själv utan ny publicering.

3. PLACERING OCH STIL (Personalizer.tsx)
- Dator: direkt under raden med pris och köpknapp.
- Mobil: i den fasta bottenraden, som en egen rad ovanför pris och köpknapp. Den ska rymmas på en rad vid 360 px bredd. Höj utfyllnaden under innehållet (h-20) så att den högre bottenraden inte döljer något.
- Liten text (text-xs) med en liten presentikon (lucide Gift, aria-hidden) i samma guldbruna färg som övriga guldtexter (accent-strong).
- Ingen nedräkning, ingen animation och ingen ny banner.

KONTROLL
- I förhandsvisningen på /smycken/hjartat syns raden under köpknappen på dator och i bottenraden vid 390 px bredd, utan att något döljs.
- Svara med en kort lista över ändrade filer.
```

```text
Rättelse till förra ändringen. Publicera inte.

PROBLEMET
På mobil täcker den fasta köpraden på produktsidan nu nedersta delen av sidfoten när man har scrollat längst ner: länken Företagsuppgifter och copyright-raden syns inte. Utfyllnaden h-20 i Personalizer hjälper inte, eftersom sidfoten kommer efter den. Felet fanns delvis innan, men den högre köpraden gör det värre.

GÖR SÅ HÄR
- Ge sidan en nedre utfyllnad som är minst lika hög som den fasta köpraden med julraden. Gäller bara under lg och bara när köpraden visas. Till exempel ett data-attribut på köpraden och body:has([data-mobile-buy-bar]) { padding-bottom: … } i styles.css, eller något motsvarande.
- Ta bort den gamla utfyllnaden h-20 om den inte längre behövs.
- Ändra inget på dator och inget annat på sidan.

KONTROLL
- Vid 390 och 360 px på /smycken/hjartat syns hela sidfoten, inklusive Företagsuppgifter, ovanför köpraden när man har scrollat längst ner.
- Svara med en kort lista över ändrade filer.
```

</details>

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
