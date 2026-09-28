# Console-calculator-OOP


### Программа

```python
import math
class Fraction():
    numerator = 1
    denominator = 1
    def __init__(self, numerator, denominator):
        if denominator == 0:
            raise ValueError("Знаменатель не может быть равен 0")
        denominator = abs(denominator)

        g = math.gcd(numerator, denominator)
        self.numerator = numerator // g
        self.denominator = denominator // g

    def __add__(self, other):
        return Fraction(self.numerator*other.denominator + self.denominator*other.numerator, self.denominator*other.denominator)

    def __sub__(self, other):
        return Fraction(self.numerator * other.denominator - self.denominator * other.numerator, self.denominator * other.denominator)

    def __mul__(self, other):
        if isinstance(other, Fraction):
            return Fraction(self.numerator * other.numerator, self.denominator * other.denominator)
        elif isinstance(other, int):
            return Fraction(self.numerator * other, self.denominator)
        raise TypeError ("Неподдерживаемый тип")

    def __truediv__(self, other):
        if isinstance(other, Fraction):
            if other.numerator == 0:
                raise ValueError("Числитель второй дроби не может быть равен 0")
            return Fraction(self.numerator * other.denominator, self.denominator * other.numerator)
        elif isinstance(other, int):
            if other != 0:
                return Fraction(self.numerator, self.denominator * other)
            raise ZeroDivisionError("Деление на ноль запрещено")
        raise TypeError("Неподдерживаемый тип")

    def __pow__(self, other):
        if other.denominator != 1:
            raise TypeError("Введите валидную степень")
        if other.numerator < 0:
            if self.numerator == 0:
                raise ValueError("Числитель дроби не может быть равен 0")
            return Fraction(self.denominator ** abs(other.numerator), self.numerator ** abs(other.numerator))
        return Fraction(self.numerator ** other.numerator, self.denominator ** other.numerator)

    def __str__ (self):
        if self.numerator == 0:
            return "0"
        if self.denominator == 1:
            return str(self.numerator)
        if abs(self.numerator) > self.denominator:
            digit = abs(self.numerator)//self.denominator
            remainder = abs(self.numerator)%self.denominator
            if self.numerator < 0:
                return f"-{digit} {remainder}/{self.denominator}"
            return f"{digit} {remainder}/{self.denominator}"
        else:
            return f"{self.numerator}/{self.denominator}"


def parse(fraction):
    s = fraction.strip()
    num, den = s.split("/")
    return Fraction(int(num), int(den))

try:
    frac1 = input("Введите первую дробь в формате a/b: ")
    frac1 = parse(frac1)
    sign = input("Введите знак операции: ")
    frac2 = input("Введите вторую дробь в формате a/b: ")
    frac2 = parse(frac2)
    if sign == "+":
        result = frac1 + frac2
    elif sign == "-":
        result = frac1 - frac2
    elif sign == "*":
        result = frac1 * frac2
    elif sign == "/":
        result = frac1 / frac2
    elif sign == "**":
        result = frac1 ** frac2
    else:
        raise ValueError ("Операция не поддерживается")
    print(f"Результат: {result}")
except ValueError as e:
    print(f"Ошибка ввода: {e}")


```
