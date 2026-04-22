# 1. Wprowadzenie i cel analizy
Niniejszy raport stanowi szczegółowe porównanie dwóch fundamentalnie różnych podejść do inwestowania na rynku akcji: pasywnej strategii Buy & Hold (Kup i Trzymaj) oraz aktywnej strategii Momentum 12–1. Analiza bazuje na historycznych notowaniach komponentów indeksu S&P 500.
W raporcie przeanalizowano wyniki dwóch strategii inwestycyjnych na rynku akcji USA (S&P 500) w okresie 2018–2021. Celem analizy było sprawdzenie, czy prosta strategia podążania za trendem (Momentum 12-1) pozwala na osiągnięcie wyższych stóp zwrotu lub lepszą ochronę kapitału w porównaniu do pasywnego podejścia „Kup i Trzymaj” (Buy & Hold). Wyniki wskazują na dominację strategii pasywnej w badanym okresie hossy, przy jednoczesnym braku skutecznej ochrony momentum przed gwałtownymi szokami rynkowymi (np. krach COVID-19).


# 2. Opis danych
Analizę przeprowadzono na podstawie danych historycznych dla 500 spółek wchodzących w skład indeksu S&P 500, pobranych z serwisu Kaggle.
Szereg czasowy: Dane miesięczne (stopy zwrotu).
Konstrukcja indeksu: Zastosowano podejście Equal-Weighted (równowagowe). Oznacza to, że każda spółka ma identyczny wpływ na wynik portfela, co pozwala na lepszą ocenę ogólnej kondycji rynku niż indeksy ważone kapitalizacją, gdzie dominują najwięksi gracze (np. Big Tech).
W badaniu wykorzystano środowisko R oraz biblioteki dplyr, readr, ggplot2, tidyr do przetwarzania danych. 

## 2.1. Konstrukcja Benchmarku (S&P 500 Proxy)
Zamiast korzystać z gotowego indeksu wagowego, model oblicza miesięczny zwrot rynku jako średnią arytmetyczną zwrotów wszystkich spółek wchodzących w skład portfela (Equal-Weighted). Pozwala to na uniknięcie dominacji największych korporacji w wynikach.

# 3. Opis strategii i metodologii
W badaniu porównano dwie metody alokacji kapitału:
Buy & Hold (B&H): Strategia pasywna Buy & Hold polega na utrzymywaniu pełnej ekspozycji na rynek przez cały okres badawczy. Inwestor nie podejmuje żadnych decyzji timingowych, a miesięczna stopa zwrotu strategii jest równa stopie zwrotu rynku.
Momentum 12-1: Strategia aktywna Momentum 12–1 opiera się na koncepcji time-series momentum. Sygnał inwestycyjny definiowany jest jako:
Wskaźnik (M): Mt = (Pt-1/Pt-12) - 1, gdzie Pt-1 oznacza cenę z poprzedniego miesiąca, a Pt-12 cenę sprzed roku
Decyzja: Jeśli Mt > 0, portfel inwestuje 100% w akcje 
Jeśli Mt ≤ 0, portfel przechodzi w 100% na gotówkę (zwrot 0%)
Rebalancing: Odbywa się wyłącznie na koniec każdego miesiąca
Zastosowanie miesięcznego opóźnienia (skip-1-month) ogranicza wpływ krótkoterminowych odwróceń trendu i jest standardem w literaturze empirycznej.


# 4. Wyniki ilościowe
W niniejszej sekcji dokonano szczegółowej analizy wyników ilościowych strategii Buy & Hold oraz Momentum 12–1, koncentrując się na czterech kluczowych miarach efektywności inwestycyjnej: rocznej stopie zwrotu (annual_return), zmienności rocznej (annual_volatility), wskaźniku Sharpe’a (sharpe_ratio) oraz maksymalnym obsunięciu kapitału (max_drawdown).



## 4.1. Roczna stopa zwrotu
Strategia Buy & Hold osiągnęła średnią roczną stopę zwrotu na poziomie 16.4%, co odzwierciedla silny trend wzrostowy na rynku akcji USA w badanym okresie. Wysoka roczna stopa zwrotu jest konsekwencją ciągłej ekspozycji na rynek oraz braku decyzji timingowych, które mogłyby ograniczyć udział w hossie.
Strategia Momentum 12–1 uzyskała istotnie niższą roczną stopę zwrotu (~8.0%). Niższa stopa wynika z okresowego pozostawania poza rynkiem w miesiącach, w których sygnał momentum był nieaktywny. W warunkach dominującej hossy takie podejście prowadzi do utraty części dodatnich stóp zwrotu, co negatywnie wpływa na wynik końcowy.

## 4.2. Zmienność roczna jako miara ryzyka
Zmienność roczna strategii Buy & Hold wyniosła 19.5%, co jest typowym poziomem dla rynku akcji USA. Strategia Momentum cechowała się nieco niższą zmiennością (17.6%), co wskazuje, że okresowe przejścia do gotówki ograniczyły amplitudę wahań portfela.
Należy jednak podkreślić, że redukcja zmienności miała charakter umiarkowany. Wynika to z faktu, iż strategia Momentum pozostawała zainwestowana przez ponad 90% badanego okresu, co znacząco ograniczyło jej potencjał defensywny.

## 4.3. Efektywność ryzykowna - Sharpe ratio
Wskaźnik Sharpe’a dla strategii Buy & Hold wyniósł 0.88, przewyższając wartość uzyskaną przez strategię Momentum (0.53). Oznacza to, że każda jednostka ryzyka podejmowana w strategii pasywnej była lepiej wynagradzana niż w przypadku strategii momentum.
Niższy Sharpe Momentum wskazuje, że redukcja zmienności nie była wystarczająca, aby zrekompensować utratę stóp zwrotu. W badanym okresie strategia Buy & Hold oferowała korzystniejszą relację zysku do ryzyka.

## 4.4. Maksymalne obsunięcie kapitału (Max Drawdown)
Maksymalne obsunięcie kapitału dla obu strategii wyniosło −25.8%, co oznacza, że strategia Momentum nie zapewniła istotnej ochrony przed najgłębszym spadkiem rynkowym w analizowanym okresie.
Kluczowym czynnikiem był gwałtowny charakter krachu związanego z pandemią COVID-19, który nastąpił szybciej niż pozwalała na to miesięczna definicja sygnału momentum. W rezultacie strategia nie zdążyła opuścić rynku przed wystąpieniem największego obsunięcia.



## 4.5. Podsumowanie wyników ilościowych
Analiza ilościowa wskazuje, że strategia Buy & Hold była korzystniejsza w analizowanym okresie zarówno pod względem stóp zwrotu, jak i efektywności ryzykownej. Strategia Momentum 12–1 nie wykazała przewagi ilościowej i nie spełniła roli skutecznego narzędzia redukcji ryzyka w warunkach silnej hossy oraz nagłych szoków rynkowych.


# 5. Weryfikacja statystyczna wyników- test t-Studenta
W celu formalnej oceny różnic pomiędzy wynikami strategii Buy & Hold oraz Momentum 12–1 zastosowano sparowany test t-Studenta dla średnich miesięcznych stóp zwrotu obu strategii. 

## 5.1. Uzasadnienie wyboru testu
Zastosowanie testu sparowanego jest uzasadnione faktem, że obie strategie generują stopy zwrotu w tych samych okresach czasowych, a obserwacje są ze sobą bezpośrednio powiązane. Różnica pomiędzy stopami zwrotu w danym miesiącu wynika wyłącznie z decyzji inwestycyjnej strategii momentum (pozostanie w rynku lub przejście do gotówki), a nie z odmiennych warunków rynkowych. Takie podejście pozwala na eliminację wpływu wspólnych czynników rynkowych i koncentruje analizę na rzeczywistej przewadze (lub jej braku) strategii aktywnej.

## 5.2. Hipotezy statystyczne
Sformułowano następujące hipotezy:
Hipoteza zerowa H0: Średnia miesięczna stopa zwrotu strategii Momentum 12–1 jest równa średniej stopie zwrotu strategii Buy & Hold.
Hipoteza alternatywna H1​: Średnie miesięczne stopy zwrotu obu strategii różnią się istotnie.

## 5.3. Wyniki testu
Wyniki testu t-Studenta przedstawiają się następująco:

t = -1.73
df = 47
p-value = 0.091

```{r}
t_test <- t.test(
  df3$r_mom,
  df3$r_bh,
  paired = TRUE
)


t_test
```

Ujemna wartość statystyki t oraz ujemna średnia różnica wskazują, że strategia Momentum generowała niższe średnie miesięczne stopy zwrotu niż strategia Buy & Hold w analizowanym okresie.

## 5.4. Interpretacja wyników
Na podstawie przeprowadzonego testu t-Studenta nie ma podstaw do stwierdzenia, że którakolwiek z analizowanych strategii jest statystycznie gorsza lub lepsza od drugiej (p>0.05). Brak istotności statystycznej różnicy średnich miesięcznych stóp zwrotu oznacza, że zaobserwowane niższe wyniki strategii Momentum 12–1 nie mogą zostać jednoznacznie przypisane samej konstrukcji strategii. Przedział ufności obejmuje wartość zero, co dodatkowo potwierdza brak jednoznacznej przewagi którejkolwiek ze strategii w sensie statystycznym.
Niższe średnie stopy zwrotu Momentum w badanym okresie mogą wynikać z czynników zewnętrznych, takich jak specyfika analizowanego rynku, struktura okresu próby (dominująca hossa), ograniczona liczba obserwacji czy brak uwzględnienia kosztów transakcyjnych i alternatywnych klas aktywów. W konsekwencji, analiza statystyczna nie dostarcza wystarczających dowodów na trwałą nieefektywność strategii momentum względem podejścia Buy & Hold. 
Wynik testu wskazuje, że strategia Momentum 12–1 w analizowanym horyzoncie nie wykazała statystycznie potwierdzonej przewagi, jednak może pełnić rolę narzędzia dywersyfikującego w innych realiach rynkowych.
Wizualizacja krzywych kapitału (Equity Curves)
Krzywe kapitału przedstawiają ewolucję wartości jednostki kapitału zainwestowanej w obie strategie w analizowanym okresie. Oś pozioma reprezentuje czas, natomiast oś pionowa skumulowaną wartość portfela.


W analizowanym okresie strategia Momentum 12–1 pozostawała zainwestowana przez większość czasu, co sprawia, że jej krzywa kapitału początkowo pokrywa się z krzywą strategii Buy & Hold. Krótkie epizody braku ekspozycji rynkowej miały ograniczony wpływ na kształt krzywej kapitału i nie prowadziły do wyraźnych okresów stabilizacji wartości portfela.
Linia strategii Buy & Hold charakteryzuje się ciągłą ekspozycją na rynek, co skutkuje pełnym udziałem zarówno w okresach wzrostów, jak i spadków cen akcji. Strategia Momentum 12–1 może wykazywać krótkie epizody stabilizacji wartości portfela, odpowiadające miesiącom, w których sygnał momentum był nieaktywny (pos = 0), a portfel pozostawał w gotówce, generując zerową stopę zwrotu.
W analizowanym okresie liczba takich epizodów była ograniczona, co wynika z dominującego trendu wzrostowego na rynku akcji. Brak długotrwałych okresów wypłaszczenia ograniczył potencjał strategii momentum do istotnej redukcji obsunięć kapitału.


# 6. Interpretacja wyników i wnioski końcowe
Badany okres charakteryzował się dominującym trendem wzrostowym na rynku akcji USA, co w naturalny sposób sprzyjało strategii pasywnej Buy & Hold, utrzymującej nieprzerwaną ekspozycję na rynek. Strategia Momentum 12–1, mimo okresowego wychodzenia z rynku, pozostawała zainwestowana przez ponad 90% czasu, co istotnie ograniczyło jej potencjał do redukcji ryzyka i obsunięć kapitału.
Istotnym wnioskiem płynącym z analizy wizualnej oraz wyników ilościowych jest wpływ opóźnienia reakcji na turbulentnym rynku, charakterystycznego dla strategii opartych na długim horyzoncie momentum. W marcu 2020 r., podczas gwałtownego załamania rynku wywołanego pandemią COVID-19, sygnał momentum pozostawał dodatni, opierając się na silnych wynikach rynku z 2019 r. W konsekwencji strategia nie opuściła rynku przed wystąpieniem największych spadków, co naraziło portfel na pełne obsunięcie kapitału.
Analiza ilościowa potwierdza, że w latach 2018–2021 strategia Buy & Hold była skuteczniejsza zarówno pod względem osiąganych stóp zwrotu, jak i efektywności ryzykownej mierzonej wskaźnikiem Sharpe’a. Strategia Momentum 12–1 nie wykazała statystycznie istotnej przewagi nad benchmarkiem i nie zapewniła wyraźnej ochrony kapitału w okresach gwałtownych spadków rynkowych.
Uzyskane wyniki podkreślają silną zależność skuteczności strategii momentum od panujących warunków rynkowych oraz znaczenie odpowiedniego doboru horyzontu analizy. W okresach długotrwałej hossy strategie pasywne mogą dominować, natomiast potencjalne korzyści z podejścia momentum ujawniają się częściej w środowiskach charakteryzujących się długimi i uporządkowanymi trendami spadkowymi.
