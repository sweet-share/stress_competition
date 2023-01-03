## Решение [соревнования](https://www.kaggle.com/competitions/silero-stress-predictor/discussion/367804) по расстановке ударений в русском языке с применением нейронных сетей и классических методов.

Суть решения - попытка предсказать ударение на основе морфологических свойств слова, расположения букв в нем и характеристик слогов.
Полученные признаки можно разделить на 6 признаков / групп признаков:

1. Морфемы слова - часть речи, падеж, род, время, число, лицо, переходность/непереходность. Ударение в русском языке может зависеть от каждой из этих морфем.

2. Учет количества каждой буквы в слове (one-hot вектор из 33 элементов). Комбинация этих фич в модели позволяет увидеть разницу и связи между разными словами.

3. Расстояние Левенштейна между словом и его леммой. Показывает, насколько далеко словоформа ушла от первоначального слова.

4. Первая и последняя буквы слова. Может быть важным признаком (например, если существительное начинается на "а", есть высокий шанс того, что оно иностранного происхождения; это влияет на ударение).

5. Порядок гласных в слове (т.е. на каком по счету слоге стоит гласная). Может влиять на ударение (пример - если буква "ё" стоит на 3 слоге, то ударение падает на 3 слог).

6. Количетсво слогов. Тоже оказывает влияние на ударание, тривиальный пример - если есть всего один слог, то и ударение стоит на позиции 1.

Группы 1, 2, 4, 5 являются категориальными и представлены через one-hot encoding, а группы 2 и 6 представлены в числовом виде. 

Кроме того, предпринята попытка создать embedding для букв с помощью 1-D сверточной нейросети, а также провести классификацию с помощью LSTM. 

В финальном решении ударение предсказывается с помощью классификатора LightGBM (GBDT).

Точность решения на приватной выборке соревнования составила 0.78 (при точности 0.86 на публичной), итог - 14 место в соревновании.
