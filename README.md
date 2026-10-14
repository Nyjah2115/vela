# Vela® — strona do nagrania rolki

Wersja słuchawkowa stron Solen® i Halden®. Otwórz `index.html` w Chrome lub Safari, włącz pełny ekran i scrolluj
(albo z folderu `vizita-rolki`: `python3 -m http.server 8766`, potem http://localhost:8766/vela/).

## Skróty
- **A**: auto-scroll przez całą stronę (ok. 16 s, równe tempo, najlepszy do nagrywania). Ponowne A zatrzymuje, kółko myszy też.
- **C**: ukryj / pokaż kursor.
- **0**: powrót na górę.

## Co jest czym
- `frames/hero/`: klatki wideo hero, kamera okrąża kobietę na wydmach i kończy na muszli słuchawek (Kling 3.0, OpenArt).
- `frames/product/`: klatki obrotu słuchawek na czerni (Veo 3.1, OpenArt, bez dźwięku).
- `frames/product-mask.png`: wycięte słuchawki z pierwszej klatki obrotu (Vision na Macu), maska na czas przejścia.
- `frames/manifest.js`: liczba klatek + krzywa ruchu obrotu (równe tempo przy scrollu).
- `source/`: oryginały z OpenArt (obrazy GPT Image 2 + oba wideo .mp4).

## Przejście (jak w Solen i Halden)
1. Hero kończy się zbliżeniem na muszlę, niebieski pierścień prawie na środku kadru.
2. Kobieta się rozmywa, tło zostaje jasne.
3. Ostre słuchawki produktowe pojawiają się dokładnie na jej słuchawkach (maska `product-mask.png`, wyrównanie w `MATCH`,
   zmierzone po niebieskim pierścieniu: `narzedzia-stron/pierscien.py`).
4. Tło gaśnie do czerni, maska znika, słuchawki rosną i zaczynają się obracać.

## Różnice względem Haldena
- Tło hero jest jasne (wydmy), więc menu u góry ma `mix-blend-mode: difference` jak wielki napis: na jasnym ciemne, na czerni białe.

## Strojenie (w `index.html`)
- `.track { height: 900vh }`: długość scrolla (więcej = wolniej).
- `T = { ... }`: kiedy gra hero, kiedy jest „fade”, kiedy obraca się produkt.
- `data-in` / `data-out` na `.callout`: kiedy pojawiają się teksty.
- `AUTO_SECONDS`: czas auto-scrolla.
