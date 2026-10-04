# Vermo: kvar före lansering och annonser (2 okt 2026)

## Läget nu
- **Sajten:** vermo.se är publicerad med hela butiken. Förlanseringsläget är borttaget för gott.
- **Kassan:** fungerar på vermo.se. Ägaren testade och fick upp kort, Klarna och Google Pay. Shopify har också Apple Pay och Shop Pay. Planen är Basic (betald).
- **Funktioner:**
  - tio produkter, varav nio publika. Stjärntecknet är dolt tills Ownprint har svarat, se OWNPRINT-FRAGA.md.
  - alla 124 variantkombinationer och sex testvarukorgar testade (2 okt)
  - bilder i varje vald färg. Pappa finns bara i guld och silver.
  - gravyrillustration i vald färg
  - köpknapp med animation och pling på varukorgen
  - tillverkare (Print-on-Demand B.V.) i produktsäkerhetsraden
  - ångerformulär med mejl
  - cookiebanner
  - policyer
- **shop.vermo.se:** skickas vidare till www.vermo.se via Shopify-temat "External Redirect". Kunder som klickar "Fortsätt handla" efter köpet hamnar alltså rätt.
- **Förpackning:** asken kommer i praktiken (ägarens prov), men den lovas inte i text, enligt ägarens beslut.
- **Tackkort:** €0,35 per order, betalas av Vermo.

## Måste göras innan annonserna startar
**Läget 2 okt kl. 15.20:**
- Klart:
  - 4, tackkortet.
  - 5, fraktpolicyn: kontrollerad via API och den lovar ingen ask.
  - 3, faktureringen: momsnumret är giltigt i VIES och väntar på Ownprints nya kontroll.
  - Runda 4–7 är publicerade av ägaren: nya produkter, rensningen, spårningen och villkoren från Shopify.
  - Privat läge (butikslösenordet) är av. Integritetspolicyn i Shopify säger "Gravyrtexter".
  - **6, spårningen, är verifierad live i Chromium den 2 okt:**
    - Före samtycke: inga anrop till Meta eller TikTok.
    - Efter "Acceptera alla":
      - Meta: PageView och ViewContent (pixel 1042319362191805).
      - TikTok: Pageview och ViewContent (DAVPCUBC77UD1K9H6HKG).
      - Shopifys consentManagement-anrop.
    - Lägg i varukorg: AddToCart till båda.
    - Kakor på .vermo.se: _tracking_consent (kassan på shop.vermo.se kan läsa den), _fbc med fbclid, _fbp, _ttp och _tt_enable_cookie.
    - Köp och kassa rapporteras av Shopifys Meta- och TikTok-appar, och Meta även via Conversions API.
- Punkt 1 ersätts: Shopify har ännu ingen order. Eftersom varje order betalas för hand i Ownprint kontrolleras gravyrtexten på första riktiga ordern, innan du betalar.
- **Temat "External Redirect – vermo.se" är publicerat av ägaren (2 okt, ca 15.15).** Hela kedjan testad i Chromium:
  - Kataloglänken shop.vermo.se/products/hjartat-snabb-leverans?fbclid=E2ETEST går till vermo.se/smycken/hjartat?fbclid=E2ETEST.
  - shop.vermo.se/ går till vermo.se/, /collections/all till /smycken och /cart till /varukorg.
  - /policies/* visar Shopifys egna policysidor med samma text som sajten.
  - Samtycke på sajten, lägg i varukorg och sedan Till kassan:
    - Kassan laddar ("Utcheckningskassa - Vermo"), och _tracking_consent på .vermo.se följer med.
    - Meta-appen skickar PageView och InitiateCheckout från kassan. Samtycket når alltså kassan.
    - TikTok-appen skickar Pageview från kassan. TikToks kassa- och köphändelser bekräftas vid första riktiga köpet i Events Manager.
  - Produkterna har nu onlineStoreUrl, så katalogerna hos Meta och TikTok får produktlänkar.
  - Det gamla temat "External Redirect" ligger kvar opublicerat som reserv.
- Kvar: 7, filmerna.
- Blockerar inte: skicka Ownprint-frågan om Stjärntecknet (OWNPRINT-FRAGA.md).

| # | Vad | Vem | Tid |
|---|---|---|---|
| 1 | **En riktig testorder på vermo.se**, t.ex. Hjärtat med text på fram- och baksidan och å/ä/ö. Kontrollera i Ownprint-appen att `Front engraving text` och `Back engraving text` kom fram exakt. Låt den produceras, eller avbryt i Ownprint och återbetala i Shopify. *Det enda som inte är bevisat är att Ownprint läser texten från sajtens ordrar.* | Ägaren, sedan Claude kontrollerar | 15 min |
| 2 | **Ownprint: betala varje order.** Ownprint har inget sparat kort med automatisk dragning. Varje ny order hamnar under **Orders**, där du granskar den och betalar (kort eller OwnPrint Points). Därefter går den automatiskt till produktion. Leveranstiden räknas från betalningen, så betala samma dag. Slå på e-post under **Notifications** för nya ordrar och ordrar som stoppas (on hold). Klicka **inte** på "Enable Personalization": den lägger till Ownprints ruta i Shopify-temat, som bara skickar vidare till vermo.se. Sajten skickar redan gravyrtexten. | Ägaren | 2 min per order |
| 3 | **Ownprint → Settings → Billing:** fyll i faktureringsuppgifterna och lägg in och verifiera momsnumret SE020130615601. Enligt Ownprint tar de inte ut moms av säljare i EU med verifierat momsnummer. Annars tillkommer 21 % holländsk moms, cirka 40 kr per order. | Ägaren | **Ifyllt 2 okt.** VIES visar numret som giltigt (2 okt 11.49: "Chowdhury, Navid Ahmed"). Ownprint visade "VIES temporarily unavailable – VAT is charged until validated" och kontrollerar igen automatiskt. |
| 4 | **Ownprint:** ladda upp Vermos tackkort, med texten nedan. Annars följer Ownprints standardkort med. | Ägaren | 10 min |
| 5 | **Shopify-fraktpolicyn:** klistra in texten från SHOPIFY-POLICYER.md. Den nuvarande lovar "Presentask och meddelandekort ingår." | Ägaren | 2 min |
| 6 | **Spårning för annonser.** Klart och verifierat live den 2 okt, se ovan. Meta och TikTok är kopplade i Shopify. Pixlarna laddas på sajten efter samtycke, och samtycket förs över till kassan. Kvar: publicera temakopian. | Ägaren och Claude | Klart |
| 7 | **Annonsmaterial:** filma provet, 5–10 korta klipp: uppackning, närbild på gravyren och smycket på. Riktiga klipp säljer bättre än mockups och är sanna. | Ägaren | 1 tim |

## Bör göras de första två veckorna
- ~~**Bilder i silver och roséguld** för de fyra produkterna.~~ Klart 2 okt (runda 4).
- ~~**Fler produkter.**~~ Klart 2 okt: sex nya, se tabellen nedan.
- **Bekräfta julklappsdeadline 7 december före 1 november.** Annonserna, filmerna och sajten lovar leverans före jul vid beställning senast 7 december.
  - Sajtens egen ledtid är 2–5 arbetsdagar produktion och 1–10 arbetsdagar frakt, alltså högst 15 arbetsdagar. En beställning 7 december kan då komma först 30 december.
  - Raden vid köpknappen (Lovable runda 8) döljs därför automatiskt från 3 december med nuvarande ledtid, så att sajten aldrig motsäger sig själv. Bannern och filmerna säger fortfarande 7 december.
  - **Snabbast att validera:** provbeställningens faktiska frakttid (PROVBESTALLNING.md) och Ownprints svar om frakttid och julstopp för Sverige (fråga 3 i LEVERANTORSMEJL.md).
  - **Sedan:** 7 december håller om produktion plus frakt är högst 12 arbetsdagar, t.ex. 5 + 7. Då sänks maxvärdena i supplier.ts. Annars flyttas deadline till 2 december, och decemberfilmerna klipps om.
- **Presentkort före jul:**
  - Skapa ett presentkort i Shopify (300, 500 och 700 kr) och koppla sidan /presentkort.
  - Det kostar inget extra på Basic.
  - Det är det enda som går att sälja efter sista beställningsdag för jul (7 december).
  - Gör det i november, inte nu: köpflödet för en vara utan gravyr behöver testas.
- **Nyhetsbrevet:** anmälningarna sparas i Lovable Cloud (tabellen newsletter_signups) med samtycke och tid. Före Black Week:
  - Importera dem som Shopify-kunder med samtycke till marknadsföring.
  - Skicka med Shopify Email.
- **Recensioner:** sektionen på startsidan är dold tills det finns riktiga recensioner. Välj en recensionsapp som fungerar med en fristående sajt, t.ex. Judge.me, och be om omdöme cirka 10 dagar efter leverans.
- **Svenska rubriker i orderbekräftelsen:** se nedan.
- **Betalikoner på sajten** (Klarna, Apple Pay, Google Pay, kort). Alla är nu bekräftat aktiva.
- **Pappa:** €16,50 i inköp ger bara cirka 200 kr i täckningsbidrag vid 599 kr. Med 649 kr blir det cirka 240 kr.

## Kan vänta
- Standardleverans (CJ).
- Varumärkesskydd för "Vermo" (PRV/EUIPO).
- Google Search Console.
- Erbjudandet "Köp två, spara 100 kr" till Black Week. Två Hjärtat ger då cirka 480 kr i täckningsbidrag, mot cirka 255 kr för ett.

## Sortimentet (tio produkter sedan 2 okt)
- **Fyra hade räckt för att starta.** Annonser bör ändå bara driva trafik till 1–2 vinnare (Hjärtat, Familjen), och en fokuserad butik konverterar bra.
- **Lägg till 4–6 produkter före Black Week och julen.** Ett billigare instegspris ger fler presenttillfällen och höjer ordervärdet. Sista beställningsdag för jul är 7 december.
- **Inköpspriserna hos Ownprint är nästan desamma för alla produkter.** Ett lägre pris ger därför direkt lägre marginal.
- **Antagande:** en annonserad försäljning kostar 150–300 kr i början. Det ska valideras med en testbudget på 2 000–3 000 kr.
- **Slutsats:** annonsera inte produkter för 399 kr. Använd dem som extravara, där den andra varans frakt bara kostar €3.

| Produkt | Ownprint-bas | Inköp | Pris | Täckningsbidrag före annons | Som andra vara |
|---|---|---|---|---|---|
| Hjärtat, Vår dag (finns) | Heart, Horizontal Bar | €11–11,5 | 599 | ≈ 255 kr | ≈ 300 kr |
| Familjen (finns) | Coin + Birthstone | €13,5 | 699 | ≈ 310 kr | ≈ 355 kr |
| Pappa (finns) | Men's Leather | €16,5 | 599 | ≈ 200 kr | ≈ 245 kr |
| **Namnet** (namnhalsband) | Vertical Bar Necklace | €11 | 499 | ≈ 180 kr | ≈ 230 kr |
| **Stjärntecknet** | Coin Necklace med stjärntecken (färdig nisch) | €11 | 499 | ≈ 180 kr | ≈ 230 kr |
| **Armringen** (initialer) | Bangle Bracelet | €11 | 499 | ≈ 180 kr | ≈ 230 kr |
| **Initialen** | Tag Necklace | €11 | 449 | ≈ 145 kr | ≈ 190 kr |
| **Nyckelringen** (pappa, partner) | Heart/Tag Keychain | €11 | 399 | ≈ 105 kr | ≈ 150 kr |
| **Pärlan** (premium) | Premium Pearl & Gold Coin Bracelet | €17 | 699 | ≈ 270 kr | ≈ 320 kr |

Kalkylen räknar med 11,2 kr/€, frakt €6,95 för första varan och €3 per extra vara, tackkort €0,35, kortavgift cirka 2,5 % och 25 % moms. Gravyr på baksidan drar ytterligare cirka 39 kr.

- **Mäta:** kostnad per köp under täckningsbidraget.
- **Break-even ROAS:** pris delat med täckningsbidrag, till exempel cirka 2,4 för Hjärtat.
- **Mål:** ordervärde över 650 kr.

## Text till tackkortet (förslag)
> Tack för att du valde Vermo.
> Ditt smycke är graverat just för dig, med dina ord.
> Frågor? info@vermo.se · vermo.se

## Svenska rubriker i orderbekräftelsen
1. Gå till Shopify → Settings → Notifications → Order confirmation → Edit code.
2. Sök efter `{{ property.first }}` och ersätt varje förekomst med:
```liquid
{% case property.first %}{% when 'Front engraving text' %}Gravyr framsida{% when 'Back engraving text' %}Gravyr baksida{% else %}{{ property.first }}{% endcase %}
```
3. Gör samma sak i Shipping confirmation.

Nycklarna som Ownprint läser ändras inte, bara rubrikerna i mejlet.
