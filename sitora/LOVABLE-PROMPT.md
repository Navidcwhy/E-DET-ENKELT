# Lovable-prompt – Sitora-butiken

**Innan du klistrar in prompten**

1. Låt Lovable skapa (eller koppla) Shopify-butiken med **samma e-post** som ditt Lovable-konto.
2. Installera **Ownprint** i Shopify och publicera produkterna därifrån. Då är de kopplade till fabriken.
3. Kör prompten nedan.
4. Gör testordern i PLAN.md avsnitt 5. Byt sedan platshållarnycklarna i `attributeKeys` till Ownprints exakta nycklar.

---

```text
Bygg e-handelsbutiken för Sitora: personliga, graverade smycken för den svenska marknaden. All text på svenska. Nästan all trafik kommer från Instagram- och TikTok-annonser på mobil, så bygg mobil först.

## 1. Teknik (viktigt)
- Använd Lovables Shopify-integration: en headless butik där Shopify sköter checkout, betalning (Klarna, kort, Apple Pay), moms och order.
- Produkterna publiceras från leverantörens Shopify-app (Ownprint). Skapa, ändra eller radera ALDRIG produkter, varianter eller SKU:er i Shopify, eftersom ordrarna då slutar gå automatiskt till fabriken. Läs produkterna via Storefront API. Finns inga produkter än: använd tydligt markerad mockdata.
- Använd Lovable Cloud (databas, edge functions, e-post) för nyhetsbrev, ångerformulär och prislogg.

## 2. Sortiment (priser sätts i Shopify, inte i koden)
- Hjärtat: graverat hjärthalsband med meddelandekort, 599 kr
- Familjen: mynt eller bar med barnens namn (+ födelsesten), 699 kr
- Vår dag: bar med datum eller koordinater, 599 kr
- Pappa: graverat armband eller nyckelring, 549 kr
- Tillval baksidesgravyr +99 kr. Digitala presentkort 300/500/700 kr.
Material: 18K guldpläterat rostfritt stål (även silver- och roséguldfärg).

## 3. Varumärke och design
- Känsla: premium, skandinavisk, varm och personlig. Absolut inte en "billig dropshipping-butik".
- Färger: bakgrund #FAF7F2, text #1C1B19, guld #B8925A, rosé #E9D9D0.
- Typsnitt: Cormorant Garamond (rubriker) och Inter (brödtext). För förhandsvisning av gravyr: Great Vibes (skrivstil) och Cormorant Garamond (rak).
- Stora bilder, mycket luft, tydliga knappar ("Skapa ditt smycke") och en sticky köpknapp på mobil. Mål: LCP under 2,5 s på mobil.

## 4. Sidor
1. Startsida:
   - Hero (bild eller video) med rubriken "Smycket hon aldrig tar av sig" (platshållare).
   - USP-rad: "Graverat efter din text · Presentask och meddelandekort ingår · Fri frakt · Graveras och skickas från EU".
   - Kampanjbanner som styrs av config.
   - "Handla efter mottagare": Mamma, Dotter, Partner, Syster/Vän, Pappa.
   - Bästsäljare, "Så funkar det" i tre steg, recensioner (endast verifierade köp), FAQ-utdrag och nyhetsbrev.
2. Kollektionssidor med filter för mottagare, färg och pris.
3. Produktsida med personaliserare (avsnitt 5).
4. Presentkort (Shopify gift card): "Låt mottagaren välja sin egen gravyr". Levereras direkt via e-post.
5. Om Sitora, FAQ och Kontakt.
6. Juridiska sidor: Köpvillkor, Leverans & reklamation, Integritetspolicy, Cookiepolicy, Produktsäkerhet och Ångra köp.

## 5. Personaliseraren (viktigast på hela sajten)
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

## 6. Kampanjer och leveranslöfte (bara sanna uppgifter)
- src/config/campaign.ts styr aktuell fas (lansering, early-black-week, black-week, julklappsdeadline, presentkort), bannertexter och datum.
- Leveransberäkning från config: produktionsdagar + fraktdagar räknat i arbetsdagar, med svenska helgdagar. Exempel: "Beställ idag – beräknad leverans 12–19 okt".
- Julklappsdeadline: nedräkning ENDAST till det verkliga datumet i config (startvärde 2026-12-07 23:59). Efter deadline byter bannern automatiskt till presentkort.
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

## 7. Förtroende och konvertering
- Vid köpknappen: Klarna, Fri frakt, Presentask + kort ingår, Fri omgravering om vi gör fel, Graveras i EU – inga tullavgifter.
- Plats för Klarnas meddelande om att betala senare.
- Recensioner: endast verifierade köp.
- Pop-up efter 15 sekunder eller vid exit intent, högst en gång per 7 dagar: "Få tidig tillgång till Black Week".
  - E-post, samtycke och tidsstämpel sparas i databasen.
  - Bekräftelse via e-post (dubbel opt-in).

## 8. Juridik (Sverige/EU)
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

## 9. SEO
Svenska titlar och metabeskrivningar, structured data (Product, Offer, Organization), sitemap, OG-bilder och snygga URL:er (/smycken/hjartat).

## Bygg i den här ordningen
1. Design, startsida och produktsida med personaliserare.
2. Varukorg och checkout mot Shopify med attributes.
3. Juridiska sidor, cookie-banner och ångerformulär.
4. Kampanj-config, leveransberäkning, nyhetsbrev och prislogg.
Stanna efter varje steg och sammanfatta vad som är klart och vad jag behöver fylla i.
```
