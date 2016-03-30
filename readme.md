How many users are there? 50
`User.count`

What are the 5 most expensive items?
`Item.order(price: :desc).limit(5)`

What's the cheapest book?
id: 76, title: "Ergonomic Granite Chair", price: 1496
`Item.order(:price).where(category:"Books").limit(1)`

Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
`Address.where("street = '6439 Zetta Hills'")`
`Address.where("user_id = '40'")`

Correct Virginie Mitchell's address to "New York, NY, 10108".
`user = Address.joins('JOIN "users" ON "users".id = "addresses".user_id').where("first_name LIKE 'Virginie'")`

returns ```[#<Address:0x007fa57e6f87b0 id: 41, user_id: 39, street: "12263 Jake Crossing", city: "New York", state: "NY", zip: 10108>,
 #<Address:0x007fa57e6f85a8 id: 42, user_id: 39, street: "83221 Mafalda Canyon", city: "Bahringerland", state: "WY", zip: 24028>]```


How much would it cost to buy one of each tool? 46477
`Item.where("category like '%tool%'").sum(:price)`


How many total items did we sell? 2125
`SELECT SUM("orders"."quantity") FROM "orders"`


How much was spent on books? 1081352
`Item.joins('JOIN "orders" ON "orders".item_id = "items".id').where('category like "%books%"').sum('"items".price * "orders".quantity')`

Simulate buying an item by inserting a User for yourself and an Order for that User.
`User.create(first_name: "Dane", last_name: "Carmichael", email: "me@me.com")`
`Order.create(user_id: 51, item_id: 66, quantity: 6)`
