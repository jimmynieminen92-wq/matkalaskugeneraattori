# Matkalasku

Selaimessa toimiva työkalu kuukausittaisen matkalaskun tekemiseen: kilometrikorvaukset, päivärahat ja kuitit yhdeksi PDF:ksi (yhteenvetosivu + kuitit liitteinä).

Koko sovellus on yksi tiedosto, `index.html`. Se ei tarvitse palvelinta, tiliä eikä API-avainta.

## Julkaisu GitHub Pagesissa

1. Luo GitHubiin uusi repositorio (esim. `matkalasku`). Julkinen repo käy, koska tiedostossa ei ole henkilötietoja.
2. Lataa `index.html` ja `README.md` repositorion juureen (**Add file → Upload files**).
3. Avaa **Settings → Pages**.
4. Valitse **Source: Deploy from a branch**, branchiksi `main` ja kansioksi `/ (root)`. Paina **Save**.
5. Hetken kuluttua sivu avautuu osoitteessa `https://KÄYTTÄJÄNIMI.github.io/matkalasku/`.

Puhelimessa avaa osoite selaimessa ja valitse **Lisää aloitusnäyttöön** (iPhone: jakovalikko, Android: selaimen valikko). Silloin sovellus avautuu omana kuvakkeenaan.

Voit käyttää tiedostoa myös ilman GitHubia: tallenna `index.html` ja avaa se selaimessa. Internet-yhteys tarvitaan kuitenkin, koska PDF-kirjastot ladataan cdnjs.cloudflare.com-palvelusta.

## Tietojen tallennus

- Kaikki tiedot (ajot, kuitit, liitteet, asetukset) tallentuvat **vain siihen selaimeen ja siihen osoitteeseen**, jossa sovellusta käytetään. Mitään ei lähetetä mihinkään.
- Tiedot eivät siirry laitteelta toiselle automaattisesti. Käytä **Lataa varmuuskopio** ja **Avaa varmuuskopio** -painikkeita (varmuuskopio sisältää myös liitteet).
- Selaimen tietojen tyhjennys poistaa tiedot. Lataa varmuuskopio ennen sitä.
- Jos siirrät sivun toiseen osoitteeseen, tiedot eivät siirry mukana. Siirrä ne varmuuskopiolla.

## Kuittien lukeminen

- PDF-laskuista päivä ja summa luetaan PDF:n tekstistä. Päiväksi valitaan ensisijaisesti eräpäivä ja summaksi viimeinen "Yhteensä"-rivi. Luku on arvio, joten tarkista se aina (keltaiset kentät).
- Skannatuista PDF:istä ja kuvista (JPG, PNG) tietoja ei lueta, vaan päivä, summa ja kuvaus täytetään käsin. Kuva liitetään silti PDF:ään.

## Päivärahojen ja km-korvauksen vuosittainen päivitys

Verohallinto vahvistaa uudet määrät yleensä loppuvuodesta. Lisää uusi vuosi `index.html`-tiedostossa olevaan taulukkoon (etsi teksti `const RATES=`):

```js
const RATES={2025:{rOsa:24,rKoko:53,rKm:0.59},2026:{rOsa:25,rKoko:54,rKm:0.55}};
```

Esimerkiksi vuodelle 2027 lisätään pilkun jälkeen `,2027:{rOsa:..,rKoko:..,rKm:..}`. Määrät löytyvät osoitteesta https://www.vero.fi/henkiloasiakkaat/auto/kilometrikorvaus_ja_paivaraha/. Sovellus ilmoittaa itse, jos valitulle vuodelle ei ole tallennettuja määriä.

## Päivärahan säännöt

- alle 6 h: ei päivärahaa
- 6 h – 9,99 h: osapäiväraha
- 10 h tai yli: kokopäiväraha

Rajat on kirjoitettu `calc`-funktioon (`h>=10`, `h>=6`).

## Käytetyt kirjastot (ladataan CDN:stä)

- pdf-lib 1.17.1: PDF:n luonti ja liitteiden yhdistäminen
- pdf.js 3.11.174: tekstin lukeminen PDF-laskuista
