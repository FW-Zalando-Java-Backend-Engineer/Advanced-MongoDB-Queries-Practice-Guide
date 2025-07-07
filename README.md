# 📚 Advanced MongoDB Queries Practice Guide

## Theme: Library Management System

**Welcome!**
In this project, you'll create a MongoDB database to manage a **Library** with 4 rich collections:

* 📖 `books`
* 👩‍🎓 `members`
* 📦 `borrowRecords`
* 👥 `staff`

You’ll **insert real sample data** and **practice advanced querying operators**.

Each section:

* ✅ Plain English question
* ✅ The exact query to copy
* ✅ Explanation of the result

This is a *complete guided exercise*.

---

## 🟣 1️⃣ DATABASE SETUP

### ✅ Switch / Create Database

```javascript
use libraryDB
```

---

## 🟣 2️⃣ INSERT SAMPLE DATA

### ✅ A. books Collection

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

### ✅ B. members Collection

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

### ✅ C. borrowRecords Collection

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

### ✅ D. staff Collection

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

## 🟣 3️⃣ PRACTICE: ADVANCED QUERIES

Each question below:

* ✅ Plain English question for the student
* ✅ Copy-paste-ready query
* ✅ Explanation of what it does

---

### ✅ (1) Comparison Operators

**❓ Q1. Find all books cheaper than \$40.**

```javascript
db.books.find({ price: { $lt: 40 } })
```

🗒️ *Explanation:* Finds books with price less than 40.

---

**❓ Q2. Find books priced between \$30 and \$60 inclusive.**

```javascript
db.books.find({ price: { $gte: 30, $lte: 60 } })
```

🗒️ *Explanation:* `$gte` (≥) and `$lte` (≤) combined to define a price range.

---

### ✅ (2) \$in and \$nin

**❓ Q3. Find books in categories Programming or AI.**

```javascript
db.books.find({ category: { $in: ["Programming", "AI"] } })
```

🗒️ *Explanation:* `$in` matches any value in the given array.

---

**❓ Q4. Exclude books in Fantasy category.**

```javascript
db.books.find({ category: { $nin: ["Fantasy"] } })
```

🗒️ *Explanation:* `$nin` excludes any of these categories.

---

### ✅ (3) Logical Operators

**❓ Q5. Find active members or those younger than 25.**

```javascript
db.members.find({
  $or: [
    { status: "active" },
    { age: { $lt: 25 } }
  ]
})
```

🗒️ *Explanation:* `$or` lets either condition match.

---

**❓ Q6. Find active members older than 30.**

```javascript
db.members.find({
  $and: [
    { status: "active" },
    { age: { $gt: 30 } }
  ]
})
```

🗒️ *Explanation:* `$and` requires *both* conditions.

---

**❓ Q7. Find members who are NOT (active OR younger than 25).**

```javascript
db.members.find({
  $nor: [
    { status: "active" },
    { age: { $lt: 25 } }
  ]
})
```

🗒️ *Explanation:* `$nor` returns docs that match *neither* condition.

---

### ✅ (4) \$exists

**❓ Q8. Find members that have an addresses field.**

```javascript
db.members.find({ addresses: { $exists: true } })
```

🗒️ *Explanation:* Checks if the field is present.

---

### ✅ (5) \$type

**❓ Q9. Find staff with age stored as int.**

```javascript
db.staff.find({ age: { $type: "int" } })
```

🗒️ *Explanation:* Verifies field data type.

---

### ✅ (6) \$regex

**❓ Q10. Find books with 'JavaScript' in title (case-insensitive).**

```javascript
db.books.find({ title: { $regex: "javascript", $options: "i" } })
```

🗒️ *Explanation:* Pattern match ignoring case.

---

**❓ Q11. Find staff whose name starts with 'M'.**

```javascript
db.staff.find({ name: { $regex: "^M" } })
```

🗒️ *Explanation:* `^` anchors to the start.

---

### ✅ (7) \$all

**❓ Q12. Find books with BOTH 'epic' and 'adventure' tags.**

```javascript
db.books.find({ tags: { $all: ["epic", "adventure"] } })
```

🗒️ *Explanation:* `$all` requires *all* values in array.

---

### ✅ (8) \$elemMatch

**❓ Q13. Find members with an address in New York.**

```javascript
db.members.find({
  addresses: { $elemMatch: { city: "New York" } }
})
```

🗒️ *Explanation:* Matches documents where any element in `addresses` array matches.

---

### ✅ (9) \$size

**❓ Q14. Find members with exactly 2 addresses.**

```javascript
db.members.find({ addresses: { $size: 2 } })
```

🗒️ *Explanation:* Matches arrays of given length.

---

### ✅ (10) \$not

**❓ Q15. Find staff who are NOT employed.**

```javascript
db.staff.find({ employed: { $not: { $eq: true } } })
```

🗒️ *Explanation:* Negates the condition.

---

### ✅ (11) Sorting

**❓ Q16. List all books by price descending.**

```javascript
db.books.find().sort({ price: -1 })
```

🗒️ *Explanation:* `-1` = descending order.

---

### ✅ (12) Projection

**❓ Q17. Show only title and price of books.**

```javascript
db.books.find({}, { title: 1, price: 1, _id: 0 })
```

🗒️ *Explanation:* Includes only specified fields.

---

### ✅ (13) Aggregation: Group

**❓ Q18. Count borrowRecords by status.**

```javascript
db.borrowRecords.aggregate([
  { $group: { _id: "$status", count: { $sum: 1 } } }
])
```

🗒️ *Explanation:* Groups by status, counts.

---

### ✅ (14) Aggregation: Match + Project

**❓ Q19. Show only Fantasy books with their title and price.**

```javascript
db.books.aggregate([
  { $match: { category: "Fantasy" } },
  { $project: { title: 1, price: 1, _id: 0 } }
])
```

🗒️ *Explanation:* Filters, then reshapes fields.

---

### ✅ (15) Aggregation: Sort

**❓ Q20. Sort staff by age ascending.**

```javascript
db.staff.aggregate([
  { $sort: { age: 1 } }
])
```

🗒️ *Explanation:* 1 = ascending order.

---

### ✅ (16) Aggregation: Complex Example

**❓ Q21. For Programming books, show average price.**

```javascript
db.books.aggregate([
  { $match: { category: "Programming" } },
  { $group: { _id: "$category", avgPrice: { $avg: "$price" } } }
])
```

🗒️ *Explanation:* Filters to category, then groups and averages.

---

## 🟣 4️⃣ COMBO / ADVANCED CHALLENGES

✅ These encourage students to *mix* operators.

---

**✅ Challenge 1**
**❓ Find active members older than 25 with at least 1 address.**

```javascript
db.members.find({
  $and: [
    { status: "active" },
    { age: { $gt: 25 } },
    { addresses: { $exists: true, $ne: [] } }
  ]
})
```

💡 *Explanation:* Combines `$and`, `$gt`, `$exists`, `$ne`.

---

**✅ Challenge 2**
**❓ Find books in Programming or AI categories priced below \$50.**

```javascript
db.books.find({
  $and: [
    { category: { $in: ["Programming", "AI"] } },
    { price: { $lt: 50 } }
  ]
})
```

---

**✅ Challenge 3**
**❓ Count number of active vs inactive members.**

```javascript
db.members.aggregate([
  { $group: { _id: "$status", count: { $sum: 1 } } }
])
```

---

**✅ Challenge 4**
**❓ Find borrowRecords with null returnDate (currently borrowed).**

```javascript
db.borrowRecords.find({ returnDate: null })
```

---

**✅ Challenge 5**
**❓ Find books that are available and have both 'classic' and 'architecture' tags.**

```javascript
db.books.find({
  $and: [
    { available: true },
    { tags: { $all: ["classic", "architecture"] } }
  ]
})
```

---

## 🟣 5️⃣ BONUS STUDENT QUESTIONS

✅ *Q: How do you exclude unavailable books?*

```javascript
db.books.find({ available: { $eq: true } })
```

---

✅ *Q: How would you find staff whose name contains "an" anywhere?*

```javascript
db.staff.find({ name: { $regex: "an", $options: "i" } })
```

---

✅ *Q: How do you find borrowRecords for a given member? (e.g., Alice)*

```javascript
db.borrowRecords.find({ memberId: "Alice" })
```

---

✅ *Q: How do you get the highest priced book?*

```javascript
db.books.find().sort({ price: -1 }).limit(1)
```

---

✅ *Q: How to list members who don't have addresses field at all?*

```javascript
db.members.find({ addresses: { $exists: false } })
```

---

## 🟣 6️⃣ TIPS FOR SUCCESS

* ✅ Use Compass for visual building of filters.
* ✅ Always check data with:

```javascript
db.collection.find().pretty()
```

* ✅ Break complex queries into parts first.
* ✅ Try adding, updating, deleting documents to test.

---

## ✅ 🎯 GOAL

> By completing this guide, you'll know **all** the advanced querying operators from the tutorial, and be able to apply them confidently to real-world MongoDB schemas.

---

**📌 Happy querying!**

✅ *Share your favorite query with the class when you finish!*

