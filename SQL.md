**Problem 1:**

- **Prerequisite**: Understand creating tables in SQL / collections in MongoDB
- **Problem**: Create a **`Customers`** table / collection with the following fields: **`id`** (unique identifier), **`name`**, **`email`**, **`address`**, and **`phone_number`**.

SQL ==> 

CREATE TABLE Customers (
    id INT PRIMARY KEY,
    name VARCHAR(255),
    email VARCHAR(255),
    address VARCHAR(255),
    phone_number VARCHAR(20)
);

mongoDB ==> 

db.createCollection("Customers")

// Add indexes for faster querying (optional but recommended)
db.Customers.createIndex({ "id": 1 }, { unique: true })

// Insert validation rules (optional but recommended)
db.runCommand({
  collMod: "Customers",
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["id", "name", "email", "address", "phone_number"],
      properties: {
        id: { bsonType: "int", description: "must be an integer and unique" },
        name: { bsonType: "string", description: "must be a string" },
        email: { bsonType: "string", description: "must be a string" },
        address: { bsonType: "string", description: "must be a string" },
        phone_number: { bsonType: "string", description: "must be a string" }
      }
    }
  }
})




**Problem 2:**

- **Prerequisite**: Understand inserting data into SQL tables / MongoDB collections
- **Problem**: Insert five rows / documents into the **`Customers`** table / collection with data of your choice.

SQL ==> 

INSERT INTO Customers (id, name, email, address, phone_number)
VALUES (1, 'John Doe', 'john.doe@example.com', '123 Main St', '555-1234'),
       (2, 'Jane Smith', 'jane.smith@example.com', '456 Elm St', '555-5678'),
       (3, 'David Johnson', 'david.johnson@example.com', '789 Oak St', '555-9012'),
       (4, 'Emily Brown', 'emily.brown@example.com', '321 Pine St', '555-3456'),
       (5, 'Michael Davis', 'michael.davis@example.com', '654 Maple St', '555-7890');


mongoDB ==> 

db.Customers.insertMany([
  { id: 1, name: 'John Doe', email: 'john.doe@example.com', address: '123 Main St', phone_number: '555-1234' },
  { id: 2, name: 'Jane Smith', email: 'jane.smith@example.com', address: '456 Elm St', phone_number: '555-5678' },
  { id: 3, name: 'David Johnson', email: 'david.johnson@example.com', address: '789 Oak St', phone_number: '555-9012' },
  { id: 4, name: 'Emily Brown', email: 'emily.brown@example.com', address: '321 Pine St', phone_number: '555-3456' },
  { id: 5, name: 'Michael Davis', email: 'michael.davis@example.com', address: '654 Maple St', phone_number: '555-7890' }
]);



**Problem 3:**

- **Prerequisite**: Understand basic data fetching in SQL / MongoDB
- **Problem**: Write a query to fetch all data from the **`Customers`** table / collection.

SQL ==> 

SELECT * FROM Customers;


mongoDB ==> 

db.Customers.find({});



**Problem 4:**

- **Prerequisite**: Understand how to select specific fields in SQL / MongoDB
- **Problem**: Write a query to select only the **`name`** and **`email`** fields for all customers.

SQL ==>

SELECT name, email FROM Customers;

mongoDB ==> 

db.Customers.find({}, { name: 1, email: 1, _id: 0 });




**Problem 5:**

- **Prerequisite**: Understand basic WHERE clause in SQL / MongoDB's find method
- **Problem**: Write a query to fetch the customer with the **`id`** of 3.

SQL ==>

SELECT * FROM Customers WHERE id = 3;

mongoDB ==> 

db.Customers.findOne({ id: 3 });



**Problem 6:**

- **Prerequisite**: Understand using string patterns in SQL (LIKE clause) / using regex in MongoDB
- **Problem**: Write a query to fetch all customers whose **`name`** starts with 'A'.


SQL ==> 

SELECT * FROM Customers WHERE name LIKE 'A%';


mongoDB ==> 

db.Customers.find({ name: /^A/ });




**Problem 7:**

- **Prerequisite**: Understand how to order data in SQL / MongoDB
- **Problem**: Write a query to fetch all customers, ordered by **`name`** in descending order.

SQL ==> 

SELECT * FROM Customers ORDER BY name DESC;


mongoDB ==> 

db.Customers.find({}).sort({ name: -1 });




**Problem 8:**

- **Prerequisite**: Understand data updating in SQL / MongoDB
- **Problem**: Write a query to update the **`address`** of the customer with **`id`** 4.

SQL ==> 

UPDATE Customers SET address = 'New Address' WHERE id = 4;


mongoDB ==> 

db.Customers.updateOne({ id: 4 }, { $set: { address: 'New Address' } });



**Problem 9:**

- **Prerequisite**: Understand how to limit results in SQL / MongoDB
- **Problem**: Write a query to fetch the top 3 customers when ordered by **`id`** in ascending order.

SQL ==> 

SELECT * FROM Customers ORDER BY id ASC LIMIT 3;


mongoDB ==> 

db.Customers.find({}).sort({ id: 1 }).limit(3);




**Problem 10:**

- **Prerequisite**: Understand data deletion in SQL / MongoDB
- **Problem**: Write a query to delete the customer with **`id`** 2.

SQL ==> 

DELETE FROM Customers WHERE id = 2;

mongoDB ==> 

db.Customers.deleteOne({ id: 2 });



**Problem 11:**

- **Prerequisite**: Understand how to count rows / documents in SQL / MongoDB
- **Problem**: Write a query to count the number of customers.


SQL ==> 

SELECT COUNT(*) FROM Customers;


mongoDB ==> 

db.Customers.countDocuments();




**Problem 12:**

- **Prerequisite**: Understand how to skip rows / documents in SQL / MongoDB
- **Problem**: Write a query to fetch all customers except the first two when ordered by **`id`** in ascending order.

s ==>

SELECT * FROM Customers ORDER BY id ASC OFFSET 2;


mongoDB ==> 

db.Customers.find({}).sort({ id: 1 }).skip(2);



**Problem 13:**

- **Prerequisite**: Understand filtering with multiple conditions in SQL / MongoDB
- **Problem**: Write a query to fetch all customers whose **`id`** is greater than 2 and **`name`** starts with 'B'.

SQL ==> 

SELECT * FROM Customers WHERE id > 2 AND name LIKE 'B%';


mongoDB ==> 

db.Customers.find({ id: { $gt: 2 }, name: /^B/ });



**Problem 14:**

- **Prerequisite**: Understand how to use OR conditions in SQL / MongoDB
- **Problem**: Write a query to fetch all customers whose **`id`** is less than 3 or **`name`** ends with 's'.

SQL ==> 

SELECT * FROM Customers WHERE id < 3 OR name LIKE '%s';


mongoDB ==> 

db.Customers.find({ $or: [{ id: { $lt: 3 } }, { name: /s$/ }] });



**Problem 15:**

- **Prerequisite**: Understand how to use NULL checks in SQL / MongoDB
- **Problem**: Write a query to fetch all customers where the **`phone_number`** field is not set or is null.


SQL ==> 

SELECT * FROM Customers WHERE phone_number IS NULL OR phone_number = '';


mongoDB ==> 

db.Customers.find({ $or: [{phone_number: null }, { phone_number: "" }] });
