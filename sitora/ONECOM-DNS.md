# One.com: DNS för vermo.se (1 okt 2026)

**Läget nu:**

| Namn | Post | Pekar på | Status |
|---|---|---|---|
| `vermo.se` | A | 185.158.133.1 (Lovable) | Rätt |
| `www.vermo.se` | A | 46.30.211.38 (One.com webbhotell) | **Fel:** SSL-fel och 503 |
| `vermo.se` | MX | `0 .` (null-MX: tar inte emot e-post) | **Fel:** kundservice@vermo.se fungerar inte |
| `_lovable.vermo.se` | TXT | två `lovable_verify=…` | Rätt, rör inte |
| `_dmarc.vermo.se` | TXT | `v=DMARC1; p=none;` | Rätt |
| `shop.vermo.se` | finns inte | | Ska skapas (kassan) |

**Hitta rätt sida:** logga in på one.com → Kontrollpanelen → välj **vermo.se** → **Avancerade inställningar** → **DNS-inställningar** → fliken **DNS-poster**. Där kan du skapa egna poster. En egen post med samma namn ersätter One.coms standardpost.

## 1. www.vermo.se → sajten (5 min)
- Skapa en A-post: värdnamn `www`, värde `185.158.133.1`, och låt TTL stå kvar på standardvärdet.
- Om det redan finns en egen post för `www` med 46.30.211.38: ändra den, eller ta bort den och skapa en ny.
- Om www bara finns som One.com-standardpost (webbhotell): skapa den egna posten ovan, eller stäng av standardposterna för webbplatsen.
- Skapa ingen AAAA-post.
- Lovable: kontrollera under Project Settings → Domains att `www.vermo.se` finns med. Lägg annars till den. Lovable skickar www vidare till vermo.se.

## 2. E-post: kundservice@vermo.se
- Skapa brevlådan `kundservice@vermo.se` i One.com under E-post. Det kan kräva ett e-postpaket hos One.com.
- Brevlådan fungerar först när MX pekar på One.coms e-postservrar.
- Om MX fortfarande är `0 .` efter att brevlådan skapats: ta bort den MX-posten och aktivera One.coms standardposter för e-post. Då läggs MX och SPF in automatiskt.
- Annan e-postleverantör, till exempel Google Workspace eller Zoho: lägg in exakt de MX- och TXT-poster som leverantören visar.

## 3. shop.vermo.se → Shopify-kassan (5 min + Shopify)
**Varför:** kassan visar i dag adressen `sitora-s-sentiments-m92xh-0dypfzx1.myshopify.com`. Med egen domän visas `shop.vermo.se` i stället, och det ger mer förtroende i kassan.

**I One.com:** skapa en CNAME-post med värdnamn `shop` och värde `shops.myshopify.com`.

**I Shopify:**
1. Gå till Inställningar → Domäner → Anslut befintlig domän.
2. Skriv `shop.vermo.se` och verifiera.
3. Välj Ändra primär domän och välj `shop.vermo.se`.

**Gör inte:** koppla inte `vermo.se` eller `www.vermo.se` till Shopify. Då slutar sajten på Lovable att fungera.

## 4. notify.vermo.se → mejl från sajten (Lovable)
1. Klicka **Konfigurera notify.vermo.se** i Lovable-editorn.
2. Lägg in exakt de poster som Lovable visar under värdnamnet `notify`.

## 5. Senare: Shopify-mejl från kundservice@vermo.se
1. Gå till Shopify → Inställningar → Aviseringar → Avsändarens e-post och ange `kundservice@vermo.se`.
2. Shopify visar då ett antal CNAME-poster som ska läggas in i One.com. De gör att orderbekräftelser kommer från er egen domän och inte hamnar i skräpposten.

## Rör inte
- A-posten för `vermo.se` (185.158.133.1)
- `_lovable`-posterna
- NS-posterna (ns01/ns02.one.com)

## Kontroll
Säg till efter varje steg, så kontrollerar jag DNS-svaret. Ändringar slår oftast igenom inom några minuter. Ibland tar det upp till 24 timmar.
