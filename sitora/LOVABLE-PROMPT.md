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
- Små saker till nästa Lovable-runda, som görs ihop med de riktiga gravyrnycklarna:
  - Varukorgen visar de tekniska fältnamnen på engelska ("Front Engraving", "Spelling Approved"). De bör visas med svenska etiketter.
  - FAQ säger "Vi levererar endast inom Sverige" två gånger.

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
