# Vermo: kvar före lansering och annonser (2 okt 2026)

## Läget nu
- **Sajten:** vermo.se är publicerad med hela butiken. Förlanseringsläget är borttaget för gott.
- **Kassan:** fungerar på vermo.se. Ägaren testade och fick upp kort, Klarna och Google Pay. Shopify har också Apple Pay och Shop Pay. Planen är Basic (betald).
- **Funktioner:**
  - fyra produkter med alla varianter testade
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
| # | Vad | Vem | Tid |
|---|---|---|---|
| 1 | **En riktig testorder på vermo.se**, t.ex. Hjärtat med text på fram- och baksidan och å/ä/ö. Kontrollera i Ownprint-appen att `Front engraving text` och `Back engraving text` kom fram exakt. Låt den produceras, eller avbryt i Ownprint och återbetala i Shopify. *Det enda som inte är bevisat är att Ownprint läser texten från sajtens ordrar.* | Ägaren, sedan Claude kontrollerar | 15 min |
| 2 | **Ownprint: betala varje order.** Ownprint har inget sparat kort med automatisk dragning. Varje ny order hamnar under **Orders**, där du granskar den och betalar (kort eller OwnPrint Points). Därefter går den automatiskt till produktion. Leveranstiden räknas från betalningen, så betala samma dag. Slå på e-post under **Notifications** för nya ordrar och ordrar som stoppas (on hold). Klicka **inte** på "Enable Personalization": den lägger till Ownprints ruta i Shopify-temat, som bara skickar vidare till vermo.se. Sajten skickar redan gravyrtexten. | Ägaren | 2 min per order |
| 3 | **Ownprint → Settings → Billing:** fyll i faktureringsuppgifterna och lägg in och verifiera momsnumret SE020130615601. Enligt Ownprint tar de inte ut moms av säljare i EU med verifierat momsnummer. Annars tillkommer 21 % holländsk moms, cirka 40 kr per order. | Ägaren | **Ifyllt 2 okt.** VIES visar numret som giltigt (2 okt 11.49: "Chowdhury, Navid Ahmed"). Ownprint visade "VIES temporarily unavailable – VAT is charged until validated" och kontrollerar igen automatiskt. |
| 4 | **Ownprint:** ladda upp Vermos tackkort, med texten nedan. Annars följer Ownprints standardkort med. | Ägaren | 10 min |
| 5 | **Shopify-fraktpolicyn:** klistra in texten från SHOPIFY-POLICYER.md. Den nuvarande lovar "Presentask och meddelandekort ingår." | Ägaren | 2 min |
| 6 | **Spårning för annonser:** skapa en Meta-pixel (dataset) och en TikTok-pixel och skicka id:na. Installera apparna "Facebook & Instagram" och "TikTok" i Shopify, som rapporterar köpen i kassan. Claude lägger in sidvisning, lägg i varukorg och till kassan på sajten, och de körs bara efter samtycke. | Ägaren och Claude | 30 min |
| 7 | **Annonsmaterial:** filma provet, 5–10 korta klipp: uppackning, närbild på gravyren och smycket på. Riktiga klipp säljer bättre än mockups och är sanna. | Ägaren | 1 tim |

## Bör göras de första två veckorna
- **Bilder i silver och roséguld** för de fyra produkterna, via Ownprints steg Mockups. Se DESKTOP-PROMPT-2.md.
- **Fler produkter:** se nedan och DESKTOP-PROMPT-2.md.
- **Svenska rubriker i orderbekräftelsen:** se nedan.
- **Betalikoner på sajten** (Klarna, Apple Pay, Google Pay, kort). Alla är nu bekräftat aktiva.
- **Pappa:** €16,50 i inköp ger bara cirka 200 kr i täckningsbidrag vid 599 kr. Med 649 kr blir det cirka 240 kr.

## Kan vänta
- Standardleverans (CJ).
- Varumärkesskydd för "Vermo" (PRV/EUIPO).
- Google Search Console.
- Erbjudandet "Köp två, spara 100 kr" till Black Week. Två Hjärtat ger då cirka 480 kr i täckningsbidrag, mot cirka 255 kr för ett.

## Sortimentet: räcker fyra produkter?
- **Ja, för att starta.** Annonser bör ändå bara driva trafik till 1–2 vinnare (Hjärtat, Familjen), och en fokuserad butik konverterar bra.
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
