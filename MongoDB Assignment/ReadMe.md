##Documentation:
Step 1: Install MongoDB
Locally:

1. Download MongoDB from the official website.
2. Follow the installation instructions for your operating system.
3. Verify the installation by running mongo --version in your terminal or command prompt.

Step 2: Start the MongoDB Server
Locally:

1 Open your terminal or command prompt.

2 Start the MongoDB server by running:
    mongod
3. Open another terminal or command prompt and start the MongoDB shell by running:  
     mongo

Step 3: Create a Database and Collection
Switch to the library database:
    use library 

Create the books collection:
    db.createCollection("books")

Step 4: Insert Data
db.books.insertMany([
  { title: "To Kill a Mockingbird", author: "Harper Lee", publishedYear: 1960, genre: "Fiction", ISBN: "9780061120084" },
  { title: "1984", author: "George Orwell", publishedYear: 1949, genre: "Dystopian", ISBN: "9780451524935" },
  { title: "The Great Gatsby", author: "F. Scott Fitzgerald", publishedYear: 1925, genre: "Classic", ISBN: "9780743273565" },
  { title: "The Catcher in the Rye", author: "J.D. Salinger", publishedYear: 1951, genre: "Classic", ISBN: "9780316769488" },
  { title: "The Hobbit", author: "J.R.R. Tolkien", publishedYear: 1937, genre: "Fantasy", ISBN: "9780547928227" }
])

Step 5: Retrieve Data
db.books.find().pretty()

Query books based on a specific author:
db.books.find({ author: "George Orwell" }).pretty()

Find books published after the year 2000:
db.books.find({ publishedYear: { $gt: 2000 } }).pretty()

Step 6: Update Data
Update the publishedYear of a specific book:
db.books.updateOne(
  { ISBN: "9780316769488" },
  { $set: { publishedYear: 1952 } }
)

Add a new field called rating to all books and set a default value
db.books.updateMany(
  {},
  { $set: { rating: 0 } }
)

Step 7: Delete Data
Delete a specific book:
db.books.deleteOne({ ISBN: "9780451524935" })

Remove all books of a particular genre:
db.books.deleteMany({ genre: "Classic" })

Step 8: Data Modeling for E-commerce Platform
{
  _id: ObjectId,
  name: String,
  email: String,
  password: String,
  address: String,
  orders: [ObjectId] // Reference to Orders
}

{
  _id: ObjectId,
  userId: ObjectId, // Reference to Users
  products: [ObjectId], // Reference to Products
  orderDate: Date,
  status: String
}

{
  _id: ObjectId,
  name: String,
  description: String,
  price: Number,
  category: String,
  stock: Number
}

Step 9: Aggregation Pipeline
db.books.aggregate([
  { $group: { _id: "$genre", totalBooks: { $sum: 1 } } }
])

Calculate the average published year of all books:
db.books.aggregate([
  { $group: { _id: null, avgPublishedYear: { $avg: "$publishedYear" } } }
])

db.books.aggregate([
  { $sort: { rating: -1 } },
  { $limit: 1 }
])

Step 10: Indexing
Create an index on the author field:
   db.books.createIndex({ author: 1 })


Benefits of indexing in MongoDB:

Improved Query Performance

Efficient Sorting

Reduced Resource Usage



