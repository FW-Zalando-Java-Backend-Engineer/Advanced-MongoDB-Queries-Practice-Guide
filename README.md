# 📚 Advanced MongoDB Queries Practice Guide

## Theme: Library Management System

Welcome! In this exercise, you'll **build and query** a MongoDB database for a *Library Management System*.

You’ll learn to use **advanced query operators** by exploring collections of:

* 📖 Books
* 👩‍🎓 Members
* 📦 Borrow Records
* 👥 Staff

This guide includes:

✅ Step-by-step setup
✅ Sample data for all collections (lots of records!)
✅ Practice queries covering *ALL* advanced operators from the tutorial
✅ Explanations and hints

---

## 🟣 1️⃣ Create Database

Open your **mongosh** and run:

```javascript
use libraryDB
```

✅ This will switch to (or create) your database called `libraryDB`.

---

## 🟣 2️⃣ Create Collections and Insert Sample Data

You'll create **4 collections**:

* `books`
* `members`
* `borrowRecords`
* `staff`

Each with **rich sample data**.

---

### 📖 A. books Collection

✅ Insert \~14 books:

```javascript
db.books.insertMany([
  { title: "Clean Code", author: "Robert C. Martin", category: "Programming", price: 45, tags: ["code", "best-practice"], available: true },
  { title: "Design Patterns", author: "GoF", category: "Programming", price: 55, tags: ["architecture", "classic"], available: true },
  { title: "Harry Potter", author: "J.K. Rowling", category: "Fantasy", price: 30, tags: ["magic", "bestseller"], available: false },
  { title: "The Hobbit", author: "J.R.R. Tolkien", category: "Fantasy", price: 28, tags: ["classic", "adventure"], available: true },
  { title: "Data Science Handbook", author: "Jake VanderPlas", category: "Data", price: 60, tags: ["data", "science"], available: true },
  { title: "Eloquent JavaScript", author: "Marijn Haverbeke", category: "Programming", price: 35, tags: ["javascript", "web"], available: false },
  { title: "Algorithms", author: "Sedgewick", category: "Programming", price: 70, tags: ["algorithms", "classic"], available: true },
  { title: "Lord of the Rings", author: "J.R.R. Tolkien", category: "Fantasy", price: 50, tags: ["epic", "adventure"], available: false },
  { title: "Python Crash Course", author: "Eric Matthes", category: "Programming", price: 40, tags: ["python", "beginner"], available: true },
  { title: "Deep Learning", author: "Goodfellow", category: "AI", price: 80, tags: ["ai", "ml"], available: true },
  { title: "The Silmarillion", author: "J.R.R. Tolkien", category: "Fantasy", price: 35, tags: ["epic", "lore"], available: true },
  { title: "AI Superpowers", author: "Kai-Fu Lee", category: "AI", price: 45, tags: ["ai", "china"], available: true },
  { title: "The Pragmatic Programmer", author: "Andrew Hunt", category: "Programming", price: 50, tags: ["best-practice", "career"], available: true },
  { title: "Kafka on the Shore", author: "Haruki Murakami", category: "Fiction", price: 25, tags: ["magic", "modern"], available: true }
])
```

---

### 👩‍🎓 B. members Collection

✅ Insert \~10 members:

```javascript
db.members.insertMany([
  { name: "Alice", email: "alice@example.com", age: 24, status: "active", addresses: [ { city: "New York", zip: "10001" } ] },
  { name: "Bob", email: "bob@example.com", age: 35, status: "inactive", addresses: [ { city: "Chicago", zip: "60601" } ] },
  { name: "Carol", email: "carol@example.com", age: 28, status: "active", addresses: [ { city: "Boston", zip: "02101" } ] },
  { name: "Dave", email: "dave@example.com", age: 40, status: "active", addresses: [ { city: "San Francisco", zip: "94101" }, { city: "Seattle", zip: "98101" } ] },
  { name: "Eve", email: "eve@example.com", age: 22, status: "active", addresses: [] },
  { name: "Frank", email: "frank@example.com", age: 30, status: "inactive", addresses: [ { city: "Los Angeles", zip: "90001" } ] },
  { name: "Grace", email: "grace@example.com", age: 27, status: "active", addresses: [ { city: "Austin", zip: "73301" } ] },
  { name: "Heidi", email: "heidi@example.com", age: 32, status: "active", addresses: [ { city: "Denver", zip: "80201" } ] },
  { name: "Ivan", email: "ivan@example.com", age: 45, status: "inactive", addresses: [ { city: "Miami", zip: "33101" } ] },
  { name: "Judy", email: "judy@example.com", age: 29, status: "active", addresses: [ { city: "Philadelphia", zip: "19101" } ] }
])
```

---

### 📦 C. borrowRecords Collection

✅ Insert \~10 borrow records:

```javascript
db.borrowRecords.insertMany([
  { memberId: "Alice", bookTitle: "Clean Code", borrowDate: ISODate("2024-06-01"), returnDate: null, status: "borrowed" },
  { memberId: "Bob", bookTitle: "Harry Potter", borrowDate: ISODate("2024-05-15"), returnDate: ISODate("2024-06-10"), status: "returned" },
  { memberId: "Carol", bookTitle: "Design Patterns", borrowDate: ISODate("2024-06-05"), returnDate: null, status: "borrowed" },
  { memberId: "Dave", bookTitle: "Lord of the Rings", borrowDate: ISODate("2024-05-20"), returnDate: ISODate("2024-06-15"), status: "returned" },
  { memberId: "Eve", bookTitle: "Deep Learning", borrowDate: ISODate("2024-06-10"), returnDate: null, status: "borrowed" },
  { memberId: "Frank", bookTitle: "Harry Potter", borrowDate: ISODate("2024-06-01"), returnDate: null, status: "borrowed" },
  { memberId: "Grace", bookTitle: "The Hobbit", borrowDate: ISODate("2024-06-12"), returnDate: null, status: "borrowed" },
  { memberId: "Heidi", bookTitle: "Algorithms", borrowDate: ISODate("2024-06-02"), returnDate: ISODate("2024-06-20"), status: "returned" },
  { memberId: "Ivan", bookTitle: "AI Superpowers", borrowDate: ISODate("2024-06-15"), returnDate: null, status: "borrowed" },
  { memberId: "Judy", bookTitle: "Eloquent JavaScript", borrowDate: ISODate("2024-06-05"), returnDate: null, status: "borrowed" }
])
```

---

### 👥 D. staff Collection

✅ Insert \~6 staff records:

```javascript
db.staff.insertMany([
  { name: "Manager Mike", role: "Manager", age: 45, employed: true },
  { name: "Librarian Laura", role: "Librarian", age: 32, employed: true },
  { name: "Assistant Alex", role: "Assistant", age: 24, employed: true },
  { name: "Technician Tom", role: "Technician", age: 38, employed: false },
  { name: "Clerk Cathy", role: "Clerk", age: 29, employed: true },
  { name: "Intern Ian", role: "Intern", age: 21, employed: true }
])
```

---

## ✅ ✅ ✅ Now you have:

✔️ 4 collections
✔️ \~40 realistic records to practice with

---

## 🟣 3️⃣ Practice Advanced Queries

### ⚡ Comparison Operators

✅ *Find books cheaper than \$40*

```javascript
db.books.find({ price: { $lt: 40 } })
```

💡 *Hint: Use `$lt`, `$gt`, `$lte`, `$gte` to filter numeric fields.*

---

### ⚡ Logical Operators

✅ *Find active members OR those younger than 25*

```javascript
db.members.find({
  $or: [
    { status: "active" },
    { age: { $lt: 25 } }
  ]
})
```

💡 *Combine conditions with `$or`, `$and`, `$nor`.*

---

### ⚡ \$in and \$nin

✅ *Find books in Programming or AI categories*

```javascript
db.books.find({
  category: { $in: ["Programming", "AI"] }
})
```

✅ *Exclude Fantasy category*

```javascript
db.books.find({
  category: { $nin: ["Fantasy"] }
})
```

---

### ⚡ \$exists

✅ *Find members with addresses*

```javascript
db.members.find({
  addresses: { $exists: true }
})
```

💡 *Check if a field exists.*

---

### ⚡ \$type

✅ *Find staff with age stored as int*

```javascript
db.staff.find({
  age: { $type: "int" }
})
```

💡 *Validate data types.*

---

### ⚡ \$regex

✅ *Find books with 'JavaScript' in title (case-insensitive)*

```javascript
db.books.find({
  title: { $regex: "javascript", $options: "i" }
})
```

💡 *Search patterns in strings.*

---

### ⚡ \$all

✅ *Find books with both 'epic' and 'adventure' tags*

```javascript
db.books.find({
  tags: { $all: ["epic", "adventure"] }
})
```

---

### ⚡ \$elemMatch

✅ *Find members with a New York address*

```javascript
db.members.find({
  addresses: { $elemMatch: { city: "New York" } }
})
```

💡 *Match embedded array elements.*

---

### ⚡ \$size

✅ *Find members with exactly 2 addresses*

```javascript
db.members.find({
  addresses: { $size: 2 }
})
```

---

### ⚡ \$not

✅ *Find staff not employed*

```javascript
db.staff.find({
  employed: { $not: { $eq: true } }
})
```

---

### ⚡ Aggregation Example

✅ *Count borrow records per status*

```javascript
db.borrowRecords.aggregate([
  { $group: { _id: "$status", count: { $sum: 1 } } }
])
```

💡 *Summarize data.*

---

### ⚡ Sorting

✅ *List books by price descending*

```javascript
db.books.find().sort({ price: -1 })
```

---

### ⚡ Projection

✅ *Show only title and price of books*

```javascript
db.books.find({}, { title: 1, price: 1, _id: 0 })
```

---

## 🟣 4️⃣ 📝 Suggested Student Challenges

✅ "Find books priced between \$30 and \$60."
✅ "List active members older than 30."
✅ "Find borrowRecords with null returnDate (currently borrowed)."
✅ "Aggregate staff by role and count them."
✅ "Regex search staff whose name starts with 'M'."

---

## ✅ 5️⃣ 📌 Tips

✅ Use **MongoDB Compass** for visual filtering and aggregation!
✅ Use **mongosh** for scripting.
✅ Always verify inserts with:

```javascript
db.collection.find().pretty()
```

---

## 🎯 Goal

> Practice **ALL** advanced query operators in MongoDB, understand their **real-life use** in a **Library Management System**.

---

✅ **Happy querying!**
