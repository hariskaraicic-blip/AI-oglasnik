# AI-oglasnik — projektna dokumentacija

## 1. Svrha projekta

AI-oglasnik je prototip marketplace aplikacije koja korisniku omogućuje da napiše opis proizvoda običnim jezikom, a umjetna inteligencija pretvara taj tekst u strukturirani oglas.

Cilj je smanjiti ručni unos podataka pri objavljivanju oglasa.

## 2. Primjer korisničkog unosa

> Prodajem Samsung S23, 256 GB, očuvan, 450 EUR.

AI iz teksta treba prepoznati podatke poput naslova, opisa, cijene i kategorije. Primjer je ilustrativan, a stvarni izlaz ovisi o implementaciji i AI odgovoru.

## 3. Tehnološki stack

| Dio | Tehnologija |
|---|---|
| Backend | Python + FastAPI |
| Server | Uvicorn |
| AI integracija | Google GenAI SDK / Gemini |
| Validacija podataka | Pydantic |
| Baza podataka | SQLite |
| Web sučelje | FastAPI aplikacija i HTML |

## 4. Opis toka aplikacije

1. Korisnik unosi tekst oglasa.
2. Backend šalje tekst Gemini modelu radi izdvajanja strukturiranih polja.
3. Rezultat se validira i priprema za spremanje.
4. Oglas se sprema u SQLite bazu.
5. Web sučelje prikazuje oglase.

Ovaj opis predstavlja projektni pregled; pojedinosti implementacije treba provjeriti u izvornom kodu.

## 5. API

| Metoda | Endpoint | Namjena |
|---|---|---|
| `POST` | `/oglasi` | Kreiranje oglasa |
| `GET` | `/oglasi` | Dohvat oglasa |

## 6. Lokalno pokretanje

Primjer naredbe za pokretanje FastAPI aplikacije:

```bash
python -m uvicorn app:app --host 127.0.0.1 --port 8000 --reload
```

Aplikacija se zatim može otvoriti na `http://127.0.0.1:8000`.

Naredba pretpostavlja da je aplikacijski modul `app.py`, a FastAPI instanca nazvana `app`. Potrebno je instalirati ovisnosti iz `requirements.txt` i konfigurirati Gemini API ključ prema zahtjevima koda. Točne nazive varijabli okruženja treba potvrditi u izvornoj implementaciji.

## 7. Trenutni opseg prototipa

Dokumentirani osnovni opseg obuhvaća AI strukturiranje oglasa, spremanje u SQLite i prikaz oglasa u web sučelju.

Ovaj dokument ne potvrđuje da su sve navedene funkcionalnosti testirane ili dostupne u produkciji.

## 8. Mogući sljedeći koraci

- Korisnički računi i autentikacija
- Uređivanje i brisanje oglasa
- Učitavanje fotografija
- Pretraga, sortiranje i filteri
- Moderacija oglasa i zaštita od prijevara
- Javno hosting okruženje
- Promovirani oglasi i poslovni model

Ove stavke su prijedlozi za razvoj, a ne postojeće funkcionalnosti.