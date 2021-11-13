### class Money

Напишите класс для работы с денежными суммами.

Реализовать:



*   сложение
*   вычитание
*   умножение на целое число
*   сравнение (больше, меньше, равно, не равно)

денежной суммы. При всех операциях, сумма должна преобразовываться к сумме с минимальным количеством копеек.

Примеры:


```
# Создаем сумму из 20 рублей и 120 копеек
money_sum1 = Money(20, 120)
# Выводим сумму, с учетом минимального кол-ва копеек
print(money_sum1) # 21руб 20коп
```



```
# Создаем две денежные суммы
money_sum1 = Money(20, 60)
money_sum2 = Money(10, 45)

# Складываем суммы
money_result = money_sum1 + money_sum2
print(money_result)  # 31руб 5коп
```


**Примечание**: список всех методов для перегрузки операций [тут](https://pythonworld.ru/osnovy/peregruzka-operatorov.html).


#### Доп.задание

Добавьте операцию - вычисление <span style="text-decoration:underline;">процент </span>от суммы.

**Пример**:


```
# Создаем две денежные суммы
money_sum1 = Money(20, 60)

# Находим 21% от суммы
percent_sum = money_sum1 % 21

print(percent_sum)  # 4руб 33коп
```


**Пояснение**: % (процет от суммы) - должна являться новая денежная сумма. После вычисления процента, используем округление (функция round())


### Конвертация валют

Доработайте класс Money, добавив ему метод .convert(), для конвертации суммы в рублях в евро и доллары. Актуальные значения можно взять, сделав запрос на: [https://www.cbr-xml-daily.ru/daily_json.js](https://www.cbr-xml-daily.ru/daily_json.js)

#### Отправка запроса на url-адрес


```
import urllib.request

data = urllib.request.urlopen(url).read()
```


, где **url** - адрес сайта, на который отправляете запрос.

В переменную **data** получите ответ сайта.

Для преобразования ответа из json-формата используйте функцию:
```
data_dict = json.loads(data)
```
Модуля json
class Money:
    def __init__(self, ruble, kopek):
        self.kopek = ruble * 100 + kopek
        self.ruble = 0

    def __add__(self, other):
        return Money(self.ruble, self.kopek + other.kopek)

    def __sub__(self, other):
        return Money(self.ruble, self.kopek - other.kopek)

    def __mul__(self, num):
        return Money(self.ruble, self.kopek * num)

    def __mod__(self, pers):
        return Money(self.ruble, self.kopek * pers / 100)

    def __gt__(self, other):
        return self.kopek > other.kopek

    def __lt__(self, other):
        return self.kopek < other.kopek

    def __eq__(self, other):
        return self.kopek == other.kopek

    def __repr__(self):
         return f" {round(self.kopek // 100)} руб. {round(self.kopek % 100)} коп."

n = 2
money_sum1 = Money(20, 60)
money_sum2 = Money(10, 45)
money_result = money_sum1 + money_sum2
money_result_sub = money_sum1 - money_sum2
money_result_mul = money_sum1 * n
percent_sum = money_sum1 % 21


print (money_sum1)
print (money_sum2)
print(f"сложение: {money_result}")
print(f"вычитание: {money_result_sub}")
print(f"умножение на {n} :{money_result_mul}")
print(f"21 %: {percent_sum}")
print(money_sum1 > money_sum2)
print(money_sum1 < money_sum2)
print(money_sum1 == money_sum2)
