# Prompt till Claude Desktop: slutför, granska och publicera Meta-kampanjen (4 okt 2026)

**Så används den:**
1. Spara de tre filmerna från chatten i mappen Hämtade filer på datorn.
2. Öppna Claude Desktop med tillägget Claude in Chrome påslaget, i den Chrome där du är inloggad på Facebook.
3. Klistra in prompten nedan.
4. Claude stannar före Publicera. Klistra in sammanfattningen här i projektchatten, så granskar jag den innan du publicerar.

```text
Hjälp mig att slutföra, granska och publicera en Meta-annonskampanj för min webbutik Vermo (vermo.se, graverade smycken, säljer bara i Sverige). Använd tillägget Claude in Chrome i min Chrome, där jag är inloggad på Facebook/Meta Business. Ads Manager är en webbtjänst, så styr den via Chrome-tillägget och inte med skärmklick.

REGLER
- Ändra inga betalningsuppgifter och lägg inte till kort. Om betalmetod saknas: stanna och säg till.
- Publicera inte förrän jag har skrivit "Publicera" i chatten. Visa först sammanfattningen i steg 6. Om du inte får trycka på Publicera själv, säg till så trycker jag.
- Rätta den befintliga kampanjen. Skapa ingen ny och rör inga andra kampanjer eller kontoinställningar.
- Ta inte bort något (annons, annonsgrupp, kampanj eller media) utan att fråga mig.
- Ändra så lite som möjligt i annonser som redan är aktiva eller under granskning, eftersom ändringar kan starta om granskningen. Namnbyten går bra.
- Är en inställning låst efter publiceringen: gå inte runt det, t.ex. med en ny kampanj. Skriv det i sammanfattningen.
- Godkänn inga automatiska rekommendationer eller förslag från Meta (t.ex. Opportunity score, Advantage+-förslag) utan att fråga mig.
- Om något i Ads Manager ser annorlunda ut än jag beskriver: välj närmaste motsvarighet och skriv det i sammanfattningen. Gissa aldrig när det gäller pengar eller målgrupp. Fråga.

STEG 1: LÄGET
Öppna https://adsmanager.facebook.com och välj annonskontot 3439617542952505 (Vermo).
- Notera kontots valuta och tidszon. Valutan ska vara SEK. Om den inte är det: stanna och fråga.
- Leta upp kampanjen "Vermo | Försäljning | Kreativtest okt". Notera status (Utkast, Under granskning, Aktiv eller Fel) och belopp spenderat hittills för kampanjen, annonsgruppen och varje annons.
- Om något redan är aktivt och kampanjen saknar beloppsgräns: sätt först beloppsgränsen till 1 050 kr (se steg 2). Fortsätt sedan.

STEG 2: KAMPANJEN SKA VARA
- Mål: Försäljning. Köptyp: Auktion.
- Advantage+-katalogannonser: AV.
- Kampanjbudget (Advantage+): 150 kr per dag. Budstrategi: Högsta volym.
- Kampanjens beloppsgräns: 1 050 kr.
- A/B-test: av. Speciella annonskategorier: inga.

STEG 3: ANNONSGRUPPEN (EN ENDA) SKA VARA
- Namn: SE | Advantage+ | 150 kr
- Konverteringsplats: Webbplats (inte "Webbplats och app").
- Resultatmål: Maximera antalet konverteringar. Dataset/pixel: Vermo (1042319362191805). Händelse: Köp.
- Attributionsmodell: Standard. Inget mål för kostnad per resultat. Inga värderegler.
- Schema: start vid publicering. Har annonsgruppen redan startat: behåll startdatumet. Slutdatum: 10 oktober 2026 kl. 23:59 svensk tid.
- Målgrupp: Advantage+-målgrupp, plats Sverige, lägsta ålder 25 (under målgruppskontrollerna). Inga andra begränsningar.
- Placeringar: Advantage+-placeringar.
- EU-uppgifter: annonsören är Vermo, och annonsören och betalaren är samma.

STEG 4: ANNONSERNA
Det finns tre stående filmer (1080×1920, med svensk text i bilden, utan ljud). Leta först i annonskontots mediebibliotek. Ladda annars upp dem från mappen Hämtade filer. Om du inte kan styra filväljaren: säg till, så väljer jag filerna.
- vermo_mamma_kroken_10s.mp4
- vermo_julberattelsen_12s.mp4
- vermo_familjen_rose_8s.mp4

Gäller alla annonser:
- Identitet: Facebook-sidan Vermo och Instagram-kontot Vermo. Välj Instagram-profilen, inte "Använd Facebook-sidan".
- Annonskonfiguration: Skapa annons, Manuell uppladdning (inte Product media), format En bild eller video.
- Avmarkera "Annonser från flera annonsörer".
- Destination: Webbplats. Kryssa i "Använd en visningslänk": vermo.se. Anpassade destinationer: inaktiverade.
- Uppmaning (knapp): Handla nu.
- Musik: lägg till musik, eftersom filerna är tysta. Använd musikvalet i annonsen eller Advantage+-förbättringen Musik.
- Advantage+-förbättringar: stäng av textförbättringar, genererade bakgrunder, bildexpansion och allt annat som ändrar bild eller text. Musik får vara på.
- AI-märkning: finns ett val för att märka annonsen som AI-genererad, slå på det. Filmerna visar AI-genererade personer.
- Spårning: Webbplatshändelser = datasetet Vermo. Webbadressparametrar (exakt):
  utm_source=meta&utm_medium=paid&utm_campaign=jul_test&utm_content={{ad.name}}
- Språk: av. Evenemangsinformation: ingen.

Annons A: namn mamma_kroken (produkten Hjärtat)
- Video: vermo_mamma_kroken_10s.mp4
- Webbadress: https://vermo.se/smycken/hjartat
- Primär text: Ett hjärta med hennes namn, graverat med dina ord. Fri frakt. Beställ senast 7 december för leverans före jul.
- Rubrik: Hjärtat – graverat halsband
- Beskrivning: Fri frakt · 599 kr
- Test av innehåll: lägg till vermo_julberattelsen_12s.mp4 som version 2, med samma texter och länk. Ge den namnet julberattelsen om det går. Frågar testet efter budget eller längd: välj 7 dagar, och testet får inte höja den totala budgeten. Är du osäker: fråga.
- Går innehållstestet inte att använda: skapa i stället en separat annons, julberattelsen, i samma annonsgrupp med samma texter och länk.

Annons B: namn familjen_rose (produkten Familjen)
- Video: vermo_familjen_rose_8s.mp4
- Webbadress: https://vermo.se/smycken/familjen
- Primär text: Barnens namn och födelsesten, nära hjärtat varje dag. Fri frakt. Beställ senast 7 december för leverans före jul.
- Rubrik: Familjen – namn och födelsesten
- Beskrivning: Fri frakt · 699 kr

Känt från i går:
- "Ny Försäljning-annons" har en miniatyrbild och ett lås. Den är troligen Hjärtat-testet.
- "Ny Försäljning-annons – kopia" saknar miniatyrbild.
Döp om annonserna enligt ovan och ge kopian Familjen-innehållet. När du är klar ska annonsgruppen innehålla mamma_kroken (med julberattelsen som version 2 eller som egen annons) och familjen_rose, inget annat. Finns det fler annonser: fråga mig vad som ska hända med dem.

STEG 5: GRANSKNING
Öppna förhandsvisningen för Instagram Reels, Instagram Stories och Facebook-flödet för varje annons och kontrollera:
- Texterna i filmen syns och kapas inte av Metas knappar eller beskärning.
- Knappen är Handla nu, och länken går till rätt produktsida.
- Meta har inte lagt till genererade texter, bilder eller bakgrunder.
- Webbadressen laddar rätt produktsida på vermo.se.

STEG 6: SAMMANFATTNING INNAN PUBLICERING
Svara med exakt följande:
1. Status för kampanj, annonsgrupp och varje annons, och spenderat hittills.
2. Varje inställning från steg 2–4, markerad OK eller ÄNDRAD (vad och varför).
3. Avvikelser, låsta inställningar, varningar från Ads Manager och frågor.
4. Maxbelopp (beloppsgräns) och slutdatum.
5. Det jag behöver göra själv, t.ex. välja filer eller trycka på Publicera.
Vänta sedan på mitt "Publicera".

STEG 7: EFTER PUBLICERING
Kontrollera att leveransstatus blir "Under granskning" eller "Aktiv" och att ingen annons står på "Fel" eller "Avvisad". Rapportera kort.
```
