# financial-time-series-analysis
Projekt w Pythonie dotyczący analizy finansowych szeregów czasowych (S&amp;P 500, Złoto, USD/PLN). Projekt wykorzystuje indeks VIX do kategoryzacji zmienności rynkowej i empirycznie bada zjawisko "Volatility Clustering" za pomocą logarytmicznych stóp zwrotu.

## Zbiory danych
Analiza opiera się na historycznych danych notowań z czterech rynków:
* **S&P 500** (`SP500_data_close.csv`) – główny indeks giełdy amerykańskiej.
* **VIX** (`VIX.csv`) – indeks zmienności.
* **Złoto** (`gold.csv`) – ceny kontraktów terminowych na złoto.
* **USD/PLN** (`usdpln_d.csv`) – historyczny kurs dolara amerykańskiego do polskiego złotego.

## Etapy analizy i inżynieria danych
1. **Preprocessing i czyszczenie danych:**
   - Wczytanie danych jako szeregi czasowe z odpowiednim indeksowaniem dat.
   - Obsługa braków danych (NaN) przy użyciu metody interpolacji liniowej.
   - Integracja wszystkich aktywów w jedną spójną ramkę danych (DataFrame).
2. **Inżynieria cech:**
   - Obliczenie **logarytmicznych stóp zwrotu** dla S&P 500, Złota oraz USD/PLN.
   - Kategoryzacja indeksu VIX na 3 poziomy zmienności rynkowej:
     - `low` (VIX < 12)
     - `high` (VIX > 20)
     - `medium` (wartości pomiędzy).
3. **Eksploracja wizualna:**
   - Utworzenie wykresów liniowych obrazujących historyczne zachowanie badanych aktywów.
   - Generowanie nakładających się histogramów logarytmicznych stóp zwrotu z podziałem na reżimy zmienności (low, medium, high).
4. **Analiza prawdopodobieństwa warunkowego:**
   - Obliczenie odsetka dni, w których po wystąpieniu dużego wahania na S&P 500 (log-zwrot >= 2% lub <= -2%), kolejny dzień również charakteryzował się tak samo dużą zmiennością.

## Główne wnioski
Projekt empirycznie potwierdza rynkową teorię grupowania zmienności. Wyniki jednoznacznie wskazują, że duże wahania cen lubią występować seriami, szczególnie w okresach rynkowej paniki:

* Z perspektywy całego badanego okresu, prawdopodobieństwo wystąpienia "dużego ruchu" na S&P 500 dzień po dniu wynosi **22.24%**.
* **Segmentacja w oparciu o VIX obnaża jednak prawdziwą strukturę rynku:**
  * Przy niskiej zmienności (`low volatility`): **0.00%** (duże wahania po prostu nie występują seriami).
  * Przy średniej zmienności (`medium volatility`): **2.56%**.
  * Przy wysokiej zmienności (`high volatility` / VIX > 20): Prawdopodobieństwo kontynuacji gigantycznych wahań drastycznie rośnie aż do **23.56%**.

## Technologie i Biblioteki
Projekt został przygotowany w języku Python:
* `pandas` – zaawansowane operacje na szeregach czasowych (time series), wyrównywanie indeksów, interpolacja.
* `numpy` – obliczenia matematyczne (m.in. logarytmy naturalne).
* `matplotlib` – kompleksowa wizualizacja danych (wykresy liniowe, subploty, histogramy).

##  Jak uruchomić projekt
1. Sklonuj repozytorium na swój dysk.
2. Upewnij się, że masz zainstalowane środowisko Python z pakietami wymienionymi wyżej.
3. Projekt był tworzony z myślą o środowisku Google Colab. Jeśli chcesz go tam uruchomić, wywołaj pierwszą komórkę z google.colab.files.upload() i wgraj pliki .csv.
4. Aby uruchomić go lokalnie, wystarczy umieścić pliki `SP500_data_close.csv`, `VIX.csv`, `gold.csv`, `usdpln_d.csv` w jednym folderze z notatnikiem i pominąć komórkę odpowiedzialną za upload.
5. Uruchamiaj kolejne komórki kodu.
