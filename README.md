# Modeling-the-shopping-process-in-a-store
class Item:
    def __init__(self, name, price, description, dimensions):
        self.name = name
        self.price = price
        self.description = description
        self.dimensions = dimensions

    def __str__(self):
        return f"{self.name}, ціна: {self.price}, опис: {self.description}, розміри: {self.dimensions}"


class User:
    def __init__(self, name, surname, numberphone):
        self.name = name
        self.surname = surname
        self.numberphone = numberphone

    def __str__(self):
        return f"{self.name} {self.surname}, телефон: {self.numberphone}"


class Purchase:
    def __init__(self, user):
        self.user = user
        self.products = {}

    def add_item(self, item, cnt):
        self.products[item] = cnt

    def get_total(self):
        total = sum(item.price * quantity for item, quantity in self.products.items())
        return total

    def __str__(self):
        items_str = "\n".join([f"{item.name}: {quantity} шт." for item, quantity in self.products.items()])
        return f"Користувач: {self.user}\nТовари:\n{items_str}\nСумарна вартість: {self.get_total()} грн"


lemon = Item('Лимон', 5, "жовтий", "маленький")
apple = Item('Яблуко', 2, "червоне", "середній")
print(lemon)

buyer = User("Іван", "Іванов", "02628162")
print(buyer)

cart = Purchase(buyer)
cart.add_item(lemon, 4)
cart.add_item(apple, 20)
print(cart)
"""
Користувач: Іван Іванов
Товари:
Лимон: 4 шт.
Яблуко: 20 шт.
Сумарна вартість: 60 грн
"""

assert isinstance(cart.user, User) is True, 'Екземпляр класу User'
assert cart.get_total() == 60, "Всього 60"
cart.add_item(apple, 10)
print(cart)
"""
Користувач: Іван Іванов
Товари:
Лимон: 4 шт.
Яблуко: 10 шт.
Сумарна вартість: 40 грн
"""

assert cart.get_total() == 40
