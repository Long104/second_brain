---
date: 2024-10-31T00:00:00.000Z
tags:
  - gorm
  - crud
  - go
hubs:
  - '[[]]'
urls:
  - null
---
# crud

## create multiple

```go

 app.Post("/createAlot", func(c *fiber.Ctx) error {
  users := []database.User{} // Change this line

  if err := c.BodyParser(&users); err != nil {
   return c.Status(fiber.StatusBadRequest).SendString(err.Error())
  }

  // Convert to pointers
  userPointers := make([]*database.User, len(users))
  for i := range users {
   var existingUser database.User
   result := db.Where("email = ?", user.Email).First(&existingUser)
   if result.Error == nil {
    // Email already exists
    return c.Status(fiber.StatusConflict).SendString("Email already exists: " + user.Email)
   }
   userPointers[i] = &users[i] // Get the address of each user
  }

  // Call CreateUser
  database.CreateUser(db, userPointers)

  return c.JSON(userPointers)
 })



func CreateUser(db *gorm.DB, user []*User) {
 result := db.Create(user)

 if result.Error != nil {
  log.Fatalf("Error creating user: %v", result.Error)
 }
 fmt.Print("User was create successfully")
}

```

## good practice for crate

```go

func CreateTransaction(db *gorm.DB, c *fiber.Ctx) error {
 transaction := new(models.Transaction)
 if err := c.BodyParser(transaction); err != nil {
  return err
 }
 // Check if the category exists
 var category models.Category
 if err := db.First(&category, transaction.CategoryID).Error; err != nil {
  return c.Status(fiber.StatusBadRequest).JSON(fiber.Map{
   "error": "Invalid category_id",
  })
 }

 // db.Create(&transaction)
 if err := db.Create(&transaction).Error; err != nil {
  return c.Status(500).JSON(fiber.Map{
   "error": "Failed to create transaction",
  })
 }
 return c.JSON(transaction)
}
```

```go
func CreatePlan(db *gorm.DB, c *fiber.Ctx) error {
 plan := new(models.Plan)
 if err := c.BodyParser(&plan); err != nil {
  log.Println("Error parsing request body:", err) // Log parsing error
  return c.Status(fiber.StatusBadRequest).JSON(fiber.Map{"error": "Invalid request"})
 }

 if err := db.Create(plan).Error; err != nil {
  log.Println("Error saving plan to database:", err) // Log database error
  return c.Status(fiber.StatusInternalServerError).JSON(fiber.Map{"error": "Could not save plan"})
 }

 // db.Create(plan)
 return c.JSON(plan)
}

```
