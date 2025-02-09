class Product:
    def __init__(self, name, quantity, price):
        self.name = name
        self.quantity = quantity
        self.price = price

    def __str__(self):
        return f"{self.name} - Quantity: {self.quantity}, Price: {self.price}"


class RationShop:
    def __init__(self):
        self.inventory = {}

    def add_product(self, name, quantity, price):
        if name in self.inventory:
            self.inventory[name].quantity += quantity
        else:
            self.inventory[name] = Product(name, quantity, price)
        print(f"Added {quantity} of {name} to inventory.")

    def sell_product(self, name, quantity):
        if name in self.inventory:
            product = self.inventory[name]
            if product.quantity >= quantity:
                product.quantity -= quantity
                total_price = quantity * product.price
                print(f"Sold {quantity} of {name}. Total price: {total_price}")
            else:
                print(f"Insufficient quantity of {name}. Available: {product.quantity}")
        else:
            print(f"Product {name} not found in inventory.")

    def display_inventory(self):
        print("Current Inventory:")
        for product in self.inventory.values():
            print(product)


def main():
    shop = RationShop()

    while True:
        print("\nRation Shop Management System")
        print("1. Add Product")
        print("2. Sell Product")
        print("3. Display Inventory")
        print("4. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            name = input("Enter product name: ")
            quantity = int(input("Enter quantity: "))
            price = float(input("Enter price: "))
            shop.add_product(name, quantity, price)

        elif choice == '2':
            name = input("Enter product name to sell: ")
            quantity = int(input("Enter quantity to sell: "))
            shop.sell_product(name, quantity)

        elif choice == '3':
            shop.display_inventory()

        elif choice == '4':
            print("Exiting the system.")
            break

        else:
            print("Invalid choice. Please try again.")


if __name__ == "__main__":
    main()