# Vermo: produkter och två leveransval (2 okt 2026)

Kunden ser en produkt och väljer **Snabb leverans** (EU-partnern Ownprint) eller **Standardleverans** (CN-partnern CJdropshipping). Partnernas namn syns aldrig på sajten. Varje val är en egen Shopify-produkt från respektive app, så ordern går automatiskt till rätt partner.

## Läget 1 okt (kontrollerat via Shopify-kopplingen)
| Område | Läge |
|---|---|
| Produkter | 1 produkt totalt, oavsett status: testprodukten. Inga produkter från Ownprint eller CJ finns, inte ens som utkast. |
| Ownprint | Kopplad. Leveransplatsen "Ownprint Fulfillment" och fraktprofilen "Ownprint" finns. |
| CJ | Syns inte i Shopify. CJ:s koppling märks inte förrän en produkt listas, så kontrollera i CJ-appen att butiken står som auktoriserad. |
| Säljkanal för sajten | "Lovable" (`vibe-ide-app-lovable`). Apparna publicerar normalt bara till Online Store. Jag publicerar därför nya produkter till "Lovable" via API. |
| Shopify-temat (Online Store) | Lösenordsskyddat. Bra. |
| Moms | Priserna anges inklusive moms. Bra. |
| Policyer i kassan | Bara Shopifys engelska integritetsmall finns. Den visar Gmail-adressen och saknar telefonnummer. Övriga policyer saknas. Byts mot SHOPIFY-POLICYER.md. |
| Lovable | Två leveransval är byggda. Testprodukten är platshållare för Hjärtat med snabb leverans. |

**Frakt till Sverige, ändrat 1 okt**
- **Allmän fraktprofil:** "Normal" (65 kr, gratis från 470 kr) och "Express" (99 kr) är ersatta med "Fri frakt" för 0 kr.
  - Annars hade Standardvalet för 449 kr fått 65 kr i frakt, trots att sajten lovar fri frakt.
  - Annars hade Express sålts utan att någon partner kan leverera det.
- **Ownprint-profilen:** Sverige ändrat från €6,95 till "Fri frakt" för 0. Kontrolleras igen när Ownprint har skapat produkterna, ifall appen skriver över värdet.
- **Återställning:** i allmän profil "Normal" 65 kr med gratis frakt från 470 kr och "Express" 99 kr. I Ownprint-profilen Sverige €6,95.
- **Ej ändrat:** EU-zonen och den internationella zonen (299 kr i allmän profil) samt Ownprints övriga länder.
  - Ägaren behöver besluta om försäljningen ska begränsas till Sverige vid lanseringen.
  - Rekommendation: begränsa till Sverige. Villkoren är svenska, och det slipper hantera OSS-moms och tull.

## Produktval
| Vermo | Snabb: Ownprint (exakt namn i appen) | Standard: CJ (sökord i CJ-appen) |
|---|---|---|
| **Hjärtat** | Heart Necklace (Fine Link), €11–12 | "custom engraved heart necklace stainless steel" |
| **Familjen** | Coin Necklace with Birthstone (Fine Link), €13,50 | "custom coin necklace engraved names birthstone" |
| **Vår dag** | Horizontal Bar Necklace (Fine Link), €11–12 | "custom engraved bar necklace stainless steel" |
| **Pappa** | Premium Engraved Men's Leather Bracelet, €16,50 | "engraved leather bracelet men stainless steel" |

Ownprints frakt inom EU kostar €6,95 för första varan och €3 per extra vara. Färgerna är Silver (stål), 18K Guld och 18K Roséguld.

**Krav på CJ-produkterna:**
- 316L rostfritt stål. Inte "alloy", "zinc alloy" eller "copper", där risken för bly och kadmium är högre.
- Tre färger: silver, guld och roséguld, gärna PVD/IP-plätering.
- Kunden ska kunna lägga in egen text (laser). Kontrollera att å, ä och ö fungerar.
- Frakt till Sverige med CJPacket (9–18 dagar).
- Bra betyg och riktiga produktbilder.
- Anteckna inköpspris och frakt till Sverige, så att marginalen kan räknas.

## Priser (inkl. moms, samma pris för alla färger)
| Produkt | Snabb leverans | Standardleverans |
|---|---|---|
| Hjärtat | 599 kr | 449 kr |
| Familjen | 699 kr | 529 kr |
| Vår dag | 599 kr | 449 kr |
| Pappa | 599 kr | 449 kr |

- **Täckningsbidrag före annonser** (uppskattat): Hjärtat snabb ≈ 253 kr. Hjärtat standard ≈ 220 kr, men det förutsätter att CJ-kostnaden är ca 120 kr inklusive frakt. Verifiera i appen.
- **Gravyr:** framsidan ingår alltid. Baksidan ingår vid snabb leverans. Vid standard erbjuds den bara om CJ-produkten stöder det.

## Steg för ägaren
1. **Ownprint-appen:** skapa de fyra produkterna med tre färger var, sätt priserna i kolumnen "Snabb leverans" och publicera till Shopify.
2. **CJ-appen:** välj fyra motsvarigheter enligt kraven ovan, sätt priserna i kolumnen "Standardleverans" och skicka dem till Shopify.
3. **Säg till.** Jag publicerar då de åtta produkterna till kanalen "Lovable" via API och kontrollerar priser och frakt.
4. **Lovable:** jag fyller i handles och färgnamn per val i `productGroups.ts`. I samma ändring blir materialtexten per färg:
   - Silver: rostfritt stål.
   - Guld och Roséguld: stål med plätering.

   I dag står "18K guldpläterat" även för Silver.

## Instruktion till Claude i Desktop-appen (klistra in)

> Logga in i Shopify-admin för butiken "Vermo" (sitora-s-sentiments-m92xh) i min webbläsare. Jag sköter inloggningen själv. Gör sedan detta och fråga mig innan du betalar eller beställer något:
>
> **Ownprint-appen**
> 1. Skapa produkterna Heart Necklace (Fine Link), Coin Necklace with Birthstone, Horizontal Bar Necklace och Premium Engraved Men's Leather Bracelet.
> 2. Varje produkt ska ha färgerna Silver, Gold och Rose Gold (där de finns), med kundens egen gravyrtext på framsidan och baksidan.
> 3. Försäljningspris: 599 kr. Coin Necklace with Birthstone: 699 kr.
> 4. Publicera till Shopify.
>
> **CJdropshipping-appen**
> 1. Hitta en motsvarighet till varje produkt. Kraven:
>    - rostfritt stål 316L, inte alloy eller copper
>    - färgerna silver, guld och roséguld
>    - kundens egen gravyrtext
>    - frakt till Sverige med CJPacket
>    - bra betyg
> 2. Anteckna inköpspris och frakt till Sverige.
> 3. Lägg till dem i butiken med försäljningspris 449 kr. Coin/familj: 529 kr.
>
> **Shopify**
> 1. Publicera de åtta produkterna till försäljningskanalen "Lovable".
> 2. Ändra inga befintliga produkter, och radera ingenting.
> 3. Rapportera alla handles, variantnamn, inköpspriser och vad som inte gick.

## Innan standardleveransen öppnas för kunder (ECONOMY_ENABLED)
1. **IOSS:** registrera IOSS hos Skatteverket, eller använd tillfälligt CJ:s, och lägg in numret i CJ. Annars får kunden betala moms och avgift vid leverans.
2. **Prover från CJ godkända:** kvalitet, å/ä/ö och leveranstid uppmätt.
3. **Testrapport för nickel (EN 1811), bly och kadmium.** Vi är importör och har ansvaret.
4. **Materialtext** bekräftad för varje CJ-produkt.
5. **Förpackning:** antingen köps CJ-förpackning och kort, eller så visar sajten tydligt vad som ingår, vilket den redan gör per val.
6. **Ursprung och policyer:**
   - Visa på sajten att Standard skickas från Kina, utan att nämna partnern. Annars kan kunden tro att den skickas från EU som Snabb, vilket kan räknas som vilseledande utelämnande.
   - Lägg till överföringen av personuppgifter till Kina, med skyddsåtgärd, i integritetspolicyn.
   - Lägg till Standardtiderna i Fraktpolicy.

## Sista beställningsdag för jul
- Snabb leverans: 7 december.
- Standardleverans: 27 november. Därefter visas valet som "Hinner inte fram till julafton".
