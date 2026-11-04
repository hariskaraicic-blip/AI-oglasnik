# AI-Oglasnik — plan i primopredaja

## Smjer projekta

AI-Oglasnik je prototip alata koji korisniku olakšava sastavljanje oglasa. Prvi cilj nije izgraditi veliki oglasnik niti odmah konkurirati OLX-u. Prvi cilj je provjeriti može li alat brzo i kvalitetno pretvoriti korisnikov opis proizvoda u uređiv oglas na lokalnim jezicima.

**Osnovna vrijednost:** korisnik unese nekoliko rečenica, AI pripremi naslov i opis, korisnik pregleda/uredi rezultat, a aplikacija ga spremi.

## Trenutačna dokumentirana osnova

- Python + FastAPI
- SQLite baza
- Google Gemini SDK (`google-genai`)
- Pydantic modeli
- Uvicorn za lokalno pokretanje
- Početni API: `POST /oglasi` i `GET /oglasi`
- Postojeći dokumenti: `README.md` i `docs/AI-Oglasnik-Dokumentacija.md`

Ovaj dokument je plan, a ne potvrda da su sve stavke implementirane ili testirane. Prije izmjena pregledati stvarni kod, konfiguraciju i Git povijest.

## Sljedeći koraci — redoslijed

### 1. Upoznati i stabilizirati postojeći prototip
- Pregledati `app.py`, modele, bazu i konfiguraciju.
- Potvrditi kako se Gemini poziva i što se događa ako API ključ nedostaje ili je servis nedostupan.
- Potvrditi stvarni oblik zahtjeva/odgovora za postojeće endpointove.
- Dodati ili provjeriti minimalne testove za kreiranje i čitanje oglasa.
- Ne mijenjati shemu baze bez migracijskog plana i sigurnosne kopije.

**Kriterij završetka:** aplikacija se može pokrenuti, osnovni API radi, testovi prolaze, a greške su razumljive.

### 2. Poboljšati kvalitetu AI-generiranog oglasa
- AI smije koristiti samo informacije koje je korisnik dao.
- Ne smije izmišljati stanje, specifikacije, garanciju, cijenu, lokaciju ni druge činjenice.
- Ako podaci nedostaju, ostaviti ih praznima ili postaviti kratko pitanje.
- Rezultat treba biti prirodan na bosanskom/hrvatskom/srpskom jeziku.
- Korisnik mora moći urediti tekst prije spremanja/objave.

**Kriterij završetka:** nekoliko testnih opisa daje čitljive oglase bez izmišljenih tvrdnji.

### 3. Jednostavno korisničko sučelje
- Jedan obrazac za unos opisa.
- Prikaz generiranog naslova i opisa.
- Uređivanje prije spremanja.
- Jasna stanja učitavanja i pogreške.
- Mobilno upotrebljiv raspored.

Ne graditi još sustav korisničkih računa, plaćanja, poruka, napredne pretrage ili veliki marketplace dok osnovna vrijednost nije potvrđena.

### 4. Mali pilot
- Testirati s 10–20 ljudi koji povremeno objavljuju oglase.
- Zabilježiti koliko vremena alat štedi, što korisnici ispravljaju i bi li ga opet koristili.
- Na temelju povratnih informacija odabrati sljedeću funkciju.

## Pravila rada za asistente (ChatGPT, Grok i drugi)

1. GitHub repozitorij je izvor istine: `https://github.com/hariskaraicic-blip/AI-oglasnik`.
2. Prije predlaganja izmjena pregledati postojeće datoteke i aktualni branch.
3. Raditi male, provjerljive korake; ne prepisivati cijeli projekt bez potrebe.
4. Ne dodavati nove funkcije izvan dogovorenog opsega bez obrazloženja.
5. Ne izlagati API ključeve, `.env` datoteke ni osobne podatke.
6. Ne spremati tajne u GitHub. Koristiti lokalne environment varijable.
7. Prije promjena baze napraviti kopiju i opisati utjecaj.
8. Nakon izmjena pokrenuti dostupne testove i navesti točne rezultate. Ako testovi nisu pokrenuti, jasno to reći.
9. Za rad na GitHubu koristiti zaseban branch i PR; ne spajati bez Harisove potvrde.
10. Ne tvrditi da je aplikacija produkcijski spremna bez sigurnosne i funkcionalne provjere.

## Preuzimanje u Termuxu (Android)

Ove naredbe preuzimaju GitHub projekt u Termux. Ako Git nije instaliran:

```bash
pkg update
pkg install git python
```

Kloniranje:

```bash
git clone https://github.com/hariskaraicic-blip/AI-oglasnik.git
cd AI-oglasnik
```

Kasnije dohvaćanje novih izmjena:

```bash
cd ~/AI-oglasnik
git pull origin main
```

Pregled stanja i trenutnog commita:

```bash
git status
git log -1 --oneline
```

**Napomena:** Python paketi i način pokretanja na Androidu mogu zahtijevati prilagodbe. Prije instalacije ovisnosti pregledati `requirements.txt` (ako postoji) i README. Nemojte kopirati `.env` ili API ključeve u repozitorij. Ovaj dokument ne potvrđuje da je aplikacija već testirana u Termuxu.

## Trenutačni fokus

**Prvo stabilizirati prototip i provjeriti kvalitetu generiranja oglasa.** Tek nakon toga odlučiti što je sljedeća funkcija.