# One.com: DNS för vermo.se (uppdaterad 1 okt 2026, kl. 15)

**Hitta rätt sida:** logga in på one.com → Kontrollpanelen → välj **vermo.se** → **Avancerade inställningar** → **DNS-inställningar** → fliken **DNS-poster**. One.com stöder A-, CNAME-, MX-, TXT- och NS-poster.

## Läget (kontrollerat via DNS)

| Namn | Post | Värde | Status |
|---|---|---|---|
| `vermo.se` | A | 185.158.133.1 (Lovable) | Klart |
| `www.vermo.se` | A | 185.158.133.1 | Klart. www skickas vidare till vermo.se. |
| `shop.vermo.se` | CNAME | shops.myshopify.com | Klart. Shopifys primära domän, SSL fungerar. |
| `vermo.se` | MX | mx1–mx4.mailpod16-cph3.g1i.one.com | Klart. info@vermo.se tar emot e-post. |
| `vermo.se` | TXT (SPF) | `v=spf1 include:_custspf.one.com ~all` | Klart |
| `_dmarc.vermo.se` | TXT | `v=DMARC1; p=none` | Klart |
| `_lovable-email.vermo.se` | TXT | `lovable_email_verify=ecef…c9db` | Klart |
| `info.vermo.se` | NS | ns3.lovable.cloud och ns4.lovable.cloud | **Saknas.** Lovable kan inte skicka e-post förrän posterna finns. |
| `_lovable.vermo.se` | TXT | två `lovable_verify=…` | Klart, rör inte |

## Kvar att göra

### 1. Lovables e-post: info.vermo.se (5 min)
Skapa två NS-poster:

| Typ | Värdnamn | Pekar på |
|---|---|---|
| NS | `info` | `ns3.lovable.cloud` |
| NS | `info` | `ns4.lovable.cloud` |

- Ändra inte domänens egna namnservrar (ns01/ns02.one.com). De här posterna gäller bara underdomänen `info`.
- Brevlådan info@vermo.se påverkas inte. Den använder MX-posterna för vermo.se.
- Om Lovable ber om en `_dmarc`-post: ändra den befintliga `_dmarc`-posten i stället för att skapa en ny. En domän får bara ha en DMARC-post.
- Klicka sedan **Verify Domain** under Cloud → Emails i Lovable och säg till mig, så kontrollerar jag.

### 2. Shopify-mejl från info@vermo.se
1. Gå till Shopify → Settings → Notifications → Sender email och klicka **Authenticate** för vermo.se.
2. Shopify visar några CNAME-poster. Lägg in dem exakt som de står i One.com.

Utan det skickas orderbekräftelser från en Shopify-adress och oftare till skräpposten.

## Rör inte
- A-posterna för `vermo.se` och `www`
- CNAME-posten för `shop`
- MX- och SPF-posterna
- `_lovable`-posterna
- domänens namnservrar

**Koppla aldrig vermo.se eller www till Shopify.** Då slutar sajten på Lovable att fungera.
