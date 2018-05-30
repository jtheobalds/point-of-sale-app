# shopping_cart.py
import datetime
products = [
    {"id":1, "name": "Chocolate Sandwich Cookies", "department": "snacks", "aisle": "cookies cakes", "price": 3.50},
    {"id":2, "name": "All-Seasons Salt", "department": "pantry", "aisle": "spices seasonings", "price": 4.99},
    {"id":3, "name": "Robust Golden Unsweetened Oolong Tea", "department": "beverages", "aisle": "tea", "price": 2.49},
    {"id":4, "name": "Smart Ones Classic Favorites Mini Rigatoni With Vodka Cream Sauce", "department": "frozen", "aisle": "frozen meals", "price": 6.99},
    {"id":5, "name": "Green Chile Anytime Sauce", "department": "pantry", "aisle": "marinades meat preparation", "price": 7.99},
    {"id":6, "name": "Dry Nose Oil", "department": "personal care", "aisle": "cold flu allergy", "price": 21.99},
    {"id":7, "name": "Pure Coconut Water With Orange", "department": "beverages", "aisle": "juice nectars", "price": 3.50},
    {"id":8, "name": "Cut Russet Potatoes Steam N' Mash", "department": "frozen", "aisle": "frozen produce", "price": 4.25},
    {"id":9, "name": "Light Strawberry Blueberry Yogurt", "department": "dairy eggs", "aisle": "yogurt", "price": 6.50},
    {"id":10, "name": "Sparkling Orange Juice & Prickly Pear Beverage", "department": "beverages", "aisle": "water seltzer sparkling water", "price": 2.99},
    {"id":11, "name": "Peach Mango Juice", "department": "beverages", "aisle": "refrigerated", "price": 1.99},
    {"id":12, "name": "Chocolate Fudge Layer Cake", "department": "frozen", "aisle": "frozen dessert", "price": 18.50},
    {"id":13, "name": "Saline Nasal Mist", "department": "personal care", "aisle": "cold flu allergy", "price": 16.00},
    {"id":14, "name": "Fresh Scent Dishwasher Cleaner", "department": "household", "aisle": "dish detergents", "price": 4.99},
    {"id":15, "name": "Overnight Diapers Size 6", "department": "babies", "aisle": "diapers wipes", "price": 25.50},
    {"id":16, "name": "Mint Chocolate Flavored Syrup", "department": "snacks", "aisle": "ice cream toppings", "price": 4.50},
    {"id":17, "name": "Rendered Duck Fat", "department": "meat seafood", "aisle": "poultry counter", "price": 9.99},
    {"id":18, "name": "Pizza for One Suprema Frozen Pizza", "department": "frozen", "aisle": "frozen pizza", "price": 12.50},
    {"id":19, "name": "Gluten Free Quinoa Three Cheese & Mushroom Blend", "department": "dry goods pasta", "aisle": "grains rice dried goods", "price": 3.99},
    {"id":20, "name": "Pomegranate Cranberry & Aloe Vera Enrich Drink", "department": "beverages", "aisle": "juice nectars", "price": 4.25}
] # based on data from Instacart: https://www.instacart.com/datasets/grocery-shopping-2017

seq = [x["id"] for x in products]
min_id = min(seq)
max_id = max(seq)

product_ids = []

while True: #infinite loop
   try:
      product_id = input("Please input a product identifier: ")
      if product_id == "DONE":
         break
      if int(product_id) < min_id or int(product_id) > max_id:
         print("Are you sure that product identifier is correct? Please try again: ")
      else:
         product_ids.append(int(product_id))
   except ValueError:
      print("Are you sure that product identifier is correct? Please try again: ")




# outfile.write("-----------------")
# outfile.write(product_ids)
# outfile.write("-----------------")

#product_ids = [3, 12, 10, 3, 5, 11]
store_receipt = "store_receipt.txt"
with open(store_receipt, "w") as outfile:
    outfile.write("----------------------------------------------------")
    outfile.write("\n")
    outfile.write("JAE'S GROCERY")
    outfile.write("\n")
    outfile.write("----------------------------------------------------")
    outfile.write("\n")
    outfile.write("Location: 1013 Honey Street, New York, NY 10543")
    outfile.write("\n")
    outfile.write("Phone: 212-555-0000")
    outfile.write("\n")
    outfile.write("Web: jaesgrocery.com")
    outfile.write("\n")
    outfile.write("Date: " + datetime.date.today().strftime('%m/%d/%Y'))
    outfile.write("\n")
    outfile.write("Time: " + datetime.datetime.now().strftime('%I:%M %p'))
    outfile.write("\n")
    outfile.write("----------------------------------------------------")
    outfile.write("\n")

    outfile.write("Items:")
    outfile.write("\n")

    def matching_product(product_identifier):
      products_list = [p for p in products if p["id"] == product_identifier]
      return products_list[0]

    raw_total = 0

    for pid in product_ids:
       product = matching_product(pid)
       raw_total = raw_total + product["price"]
       pre_total = "${0:.2f}".format(raw_total)
       prod_price = "(${0:.2f})".format(product["price"])
       outfile.write(str(product["id"]) + " " + product["name"] + " " + prod_price)
       outfile.write("\n")

       outfile.write ("--------------------------------------------")
       outfile.write("\n")
       outfile.write("Subtotal: " + str(pre_total))
       outfile.write("\n")
       nyc_tax = raw_total*0.08875
       sales_tax = "${0:.2f}".format(nyc_tax)
       outfile.write("Sales tax: " + str(sales_tax))
       outfile.write("\n")
       outfile.write ("--------------------------------------------")
       outfile.write("\n")
       totwtax = raw_total + nyc_tax
       fin_total = "${0:.2f}".format(totwtax)
       outfile.write("Total: " + fin_total)
       outfile.write("\n")
       outfile.write ("--------------------------------------------")
       outfile.write("\n")
       outfile.write("Thank you for shopping with us! Please come again soon!")
       outfile.write("\n")
outfile.close()
#very close. still trying to figure out how to print without multiple subtotals and exit lines
