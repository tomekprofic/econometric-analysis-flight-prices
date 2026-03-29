# Analiza Ekonometryczna Cen Biletów Lotniczych

## Opis projektu
Celem projektu jest budowa modelu ekonometrycznego służącego do prognozowania cen biletów lotniczych (klasa Economy) na podstawie danych z rynku indyjskiego. Analiza skupia się na identyfikacji kluczowych czynników cenotwórczych oraz optymalizacji modelu pod kątem dokładności predykcji.

**Główne pytanie badawcze:** Jak parametry lotu (liczba dni do wylotu, liczba przesiadek, linia lotnicza) wpływają na końcową cenę biletu?

## Wykorzystane Technologie & Biblioteki
* **Język:** R
* **Środowisko:** RStudio
* **Biblioteki:** `tidyverse`, `caret`, `lmtest`, `car`, `mgcv` (modele GAM), `ggplot2`.

## Metodologia i Etapy Prac
1. **Eksploracyjna Analiza Danych (EDA):** Analiza statystyk opisowych oraz wizualizacja rozkładów (wykrycie silnej prawostronnej skośności cen).
2. **Weryfikacja Strukturalna:** Wykorzystanie **testu Chowa**, który wykazał konieczność budowy osobnego modelu dla klasy Economy.
3. **Specyfikacja Modelu:** - Zastosowanie transformacji logarytmicznej zmiennej zależnej.
   - Wprowadzenie interakcji (`airline * stops`).
   - Testowanie nieliniowości zmiennych `duration` oraz `days_left`.
4. **Diagnostyka Statystyczna:** - Testy: **RESET** (nieliniowość), **Breuscha-Pagana** (heteroskedastyczność), **Jarque-Bera** (normalność reszt).
   - Analiza współliniowości (**VIF**).
   - Zastosowanie estymacji odpornej na heteroskedastyczność (korekta White’a).
5. **Modelowanie Zaawansowane:** Porównanie klasycznego modelu regresji z uogólnionym modelem addytywnym (**GAM**).

## Wyniki i Wnioski
* **Dobór modelu:** Finalny model log-liniowy osiągnął skorygowany współczynnik $R^2 \approx 0.55$.
* **Kluczowe spostrzeżenia:**
    - **Reguła wyprzedzenia:** Każde 10% wzrostu czasu do wylotu przekłada się na średni spadek ceny o ok. 3%.
    - **Wpływ linii lotniczych:** Przesiadki najmocniej obniżają ceny w tanich liniach (np. AirAsia).
    - **Pora przylotu:** Loty kończące się rano są statystycznie najtańsze.
* **Predykcja:** Średni błąd absolutny (MAE) na zbiorze testowym wyniósł ok. 1695 zł.

## Struktura plików
* `model_analysis.html` – Pełny raport z analizą i wykresami.
* `model_analysis.Rmd` – Kod źródłowy analizy w R Markdown.
* `Clean_Dataset/` – Katalog z próbką danych (30 000 obserwacji).

---
*Projekt zrealizowany w ramach przedmiotu Ekonometria.*
