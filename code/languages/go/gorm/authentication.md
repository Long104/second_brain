---
date: 2024-10-31T00:00:00.000Z
tags:
  - go
  - auth
  - authentication
  - gorm
hubs:
  - '[[]]'
urls:
  - 'https://docs.mikelopster.dev/c/goapi-essential/chapter-5/fiber'
  - 'https://dev.to/siddheshk02/oauth-20-implementation-in-golang-3mj1'
---
# authentication

## install

```go

go get golang.org/x/crypto/bcrypt
go get github.com/golang-jwt/jwt/v4
go get golang.org/x/crypto/bcrypt
go get gorm.io/gorm

```

## signup in model

```go
import (
  "github.com/gofiber/fiber/v2"
  "github.com/golang-jwt/jwt/v4"
  "golang.org/x/crypto/bcrypt"
  "gorm.io/gorm"
  "time"
)

type User struct {
  gorm.Model
  Email    string `gorm:"unique"`
  Password string
}


// createUser handles user registration
func createUser(db *gorm.DB, c *fiber.Ctx) error {
  user := new(User)
  if err := c.BodyParser(user); err != nil {
    return err
  }

  // Encrypt the password
  hashedPassword, err := bcrypt.GenerateFromPassword([]byte(user.Password), bcrypt.DefaultCost)
  if err != nil {
    return err
  }
  user.Password = string(hashedPassword)

  // Create user
  db.Create(user)
  return c.JSON(user)
}
```

## signin in model

```go

func LoginUser(db *gorm.DB, c *fiber.Ctx, jwtSecretKey []byte) error {
 var input User
 var user User

 if err := c.BodyParser(&input); err != nil {
  return err
 }

 // Find user by email
 db.Where("email = ?", input.Email).First(&user)

 // Check password
 if err := bcrypt.CompareHashAndPassword([]byte(user.Password), []byte(input.Password)); err != nil {
  return c.SendStatus(fiber.StatusUnauthorized)
 }

 // TODO: Add custom claims
 // registeredClaims := jwt.RegisteredClaims{
 //  Issuer:    "YourIssuerName",                                   // Set your custom issuer here
 //  ExpiresAt: jwt.NewNumericDate(time.Now().Add(time.Hour * 72)), // Expiration time
 // }

 // Create JWT token
 token := jwt.New(jwt.SigningMethodHS256)
 claims := token.Claims.(jwt.MapClaims)
 claims["user_id"] = user.ID
 claims["exp"] = time.Now().Add(time.Hour * 72).Unix()
  claims["role"] = "admin"
  // claims["role"] = "memeber"
 // claims["exp"] = registeredClaims.ExpiresAt.Unix()
 // claims["iss"] = registeredClaims.Issuer

 t, err := token.SignedString(jwtSecretKey)
 if err != nil {
  return c.SendStatus(fiber.StatusInternalServerError)
 }

 // Set cookie
 c.Cookie(&fiber.Cookie{
  Name:     "jwt",
  Value:    t,
  Expires:  time.Now().Add(time.Hour * 72),
  HTTPOnly: true,
 })

 return c.JSON(fiber.Map{"message": "success"})
}

```

## check middleware

```go


 "github.com/gofiber/fiber/v2"
 "github.com/gofiber/fiber/v2/middleware/cors"
 jwtware "github.com/gofiber/jwt/v3"
 "github.com/golang-jwt/jwt/v4"
 "github.com/joho/godotenv"

func checkMiddleware(c *fiber.Ctx) error {
 data := c.Locals("user").(*jwt.Token)
 dataClaim := data.Claims.(jwt.MapClaims)
 fmt.Println(dataClaim)
 if dataClaim["role"] != "admin" {
  return fiber.ErrUnauthorized
 }
 return c.Next()
}

func AuthRequired(c *fiber.Ctx) error {
 err := godotenv.Load(".env")
 if err != nil {
  log.Fatalf("Some error occured. Err: %s", err)
 }

 // claims := CustomClaims{
 //  UserID: "yourUserID", // set your user ID here
 //  RegisteredClaims: jwt.RegisteredClaims{
 //   Issuer:    "CashWise",
 //   ExpiresAt: jwt.NewNumericDate(time.Now().Add(72 * time.Hour)), // Token expires in 72 hours
 //  },
 // }
 //

 // type CustomClaims struct {
 //     UserID string `json:"user_id"`
 //     *jwt.RegisteredClaims // Embed the RegisteredClaims struct
 // }

 cookie := c.Cookies("jwt")
 // token, err := jwt.ParseWithClaims(cookie, &jwt.RegisteredClaims{Issuer: "CashWise", ExpiresAt: jwt.NewNumericDate(time.Now().Add(1 * time.Hour))}, func(token *jwt.Token) (interface{}, error) {
 token, err := jwt.ParseWithClaims(cookie, &jwt.RegisteredClaims{Issuer: "CashWise"}, func(token *jwt.Token) (interface{}, error) {
  // token, err := jwt.ParseWithClaims(cookie, jwt.MapClaims{}, func(token *jwt.Token) (interface{}, error) {
  // token, err := jwt.ParseWithClaims(cookie, jwt.MapClaims{}, func(token *jwt.Token) (interface{}, error) {
  // return []byte("secret"), nil
  return []byte(os.Getenv("jwtSecretKey")), nil
 })

 // if err != nil || !token.Valid {
 //  return c.SendStatus(fiber.StatusUnauthorized)
 // }

 if claims, ok := token.Claims.(*jwt.RegisteredClaims); ok && token.Valid {
  fmt.Println("Issuer:", claims.Issuer)
  fmt.Println("user_id:", token.Claims)

  // If you want to perform additional checks or return an unauthorized status:
  // if claims.ExpiresAt.Time.Before(time.Now()) {
  //  return c.SendStatus(fiber.StatusUnauthorized) // Token is expired
  // }
    // don't need cause cookie already have expire time
 } else {
  return c.SendStatus(fiber.StatusUnauthorized)
 }


 return c.Next()
}
```

## oauth2

- https://dev.to/siddheshk02/oauth-20-implementation-in-golang-3mj1


```
