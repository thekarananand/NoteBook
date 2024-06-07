
- Clear Screen
```
cls
```

---

- Show Database
```
show dbs
```

- Create/Switch to another Database
```
use <DB NAME>
```

- Drop (Delete) Database```
```
db.dropDatabase()
```

> You should be Switched into the database you want to delete 
---

- Create Collection 
```
db.createCollection("<COLLECTION NAME>")
```

- To insert a single document
```
db.<COLLECTION NAME>.insertOne(
	{
		name: "Karan Anand",
		age: 30.
		subjects: ['PDC', 'MCS', 'AI', 'SC']	
	}
)
```

> If the Collection do not exists, it will be created

- To insert many document, in one go
```
db.<COLLECTION NAME>.insertMany(
	[
		{name: "Vansh"}, {name: "Kartikey"}, {name: "Nitish"}
	]
)
```

- To display all documents 
```
db.<COLLECTION NAME>.find()
```

---
Data Types in MongoDB
![[Pasted image 20240215141350.png]]

---
