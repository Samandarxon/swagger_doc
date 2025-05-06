
# 📘 Swagger (`swaggo/swag`) `@` Direktivalari To‘liq Qo‘llanma

Ushbu qo‘llanmada Go tilida `swaggo/swag` paketidan foydalanib Swagger hujjatlarini yaratish uchun ishlatiladigan barcha `@` direktivalar (kommentariyalar) jadval ko‘rinishida tushuntirilgan. Har bir direktiva **nima uchun kerak**, **qanday yoziladi**, va **amaliy misollar** bilan berilgan.

---

## 📊 Jadval: Swagger Direktivalar

| Direktiva            | Maqsadi                                                                                   | Format / Foydalanish                                                               | Misol                                                                                      |
|----------------------|--------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| `@title`             | API nomini belgilaydi                                                                      | `@title API nomi`                                                                  | `@title Electron Navbat API`                                                               |
| `@version`           | API versiyasini belgilaydi                                                                 | `@version 1.0`                                                                      | `@version 1.0`                                                                              |
| `@description`       | Umumiy API haqida ma'lumot                                                                 | `@description Matn`                                                                | `@description Bu navbat boshqaruv tizimi uchun API.`                                       |
| `@termsOfService`    | Xizmat shartlari havolasi                                                                   | `@termsOfService http://example.com/terms/`                                        | `@termsOfService http://navbat.uz/terms/`                                                  |
| `@contact.name`      | Kontakt ismi                                                                                | `@contact.name Ism`                                                                | `@contact.name Ali Akbarov`                                                                |
| `@contact.email`     | Kontakt email manzili                                                                      | `@contact.email user@example.com`                                                  | `@contact.email admin@navbat.uz`                                                           |
| `@license.name`      | Litsenziya nomi                                                                             | `@license.name MIT`                                                                | `@license.name Apache 2.0`                                                                 |
| `@license.url`       | Litsenziya URL manzili                                                                      | `@license.url http://opensource.org/licenses/MIT`                                  | `@license.url https://opensource.org/licenses/Apache-2.0`                                  |
| `@host`              | API host (Swagger UI uchun)                                                                | `@host localhost:8080`                                                              | `@host api.navbat.uz`                                                                      |
| `@BasePath`          | Asosiy API yo‘li                                                                            | `@BasePath /api/v1`                                                                 | `@BasePath /api`                                                                           |
| `@schemes`           | Qo‘llab-quvvatlanadigan protokollar                                                         | `@schemes http https`                                                              | `@schemes https`                                                                           |
| `@Tags`              | Endpointni guruhlash uchun                                                                  | `@Tags users`                                                                      | `@Tags admin`                                                                              |
| `@Accept`            | Qaysi formatdagi ma’lumotlarni qabul qilishini belgilaydi                                  | `@Accept json`                                                                     | `@Accept json`                                                                             |
| `@Produce`           | Qanday javob formatida qaytarilishini belgilaydi                                           | `@Produce json`                                                                    | `@Produce json`                                                                            |
| `@Param`             | Endpoint parametrlari haqida ma’lumot (query, path, body, header)                          | `@Param name in type required "description"`                                       | `@Param id path int true "Foydalanuvchi ID"`                                               |
| `@Success`           | Muvaffaqiyatli javob kodi va modeli                                                         | `@Success 200 {object} models.User`                                                | `@Success 200 {object} User`                                                               |
| `@Failure`           | Xato holatlari kodi va modeli                                                               | `@Failure 400 {object} ErrorResponse`                                              | `@Failure 404 {object} ErrorResponse`                                                      |
| `@Router`            | Endpoint yo‘li va HTTP metodi                                                               | `@Router /users/{id} [get]`                                                        | `@Router /login [post]`                                                                    |
| `@Summary`           | Endpoint mazmunining qisqacha tavsifi                                                       | `@Summary Get user by ID`                                                          | `@Summary Foydalanuvchini ID orqali olish`                                                 |
| `@Description`       | Endpoint haqida batafsil ma’lumot                                                           | `@Description Ushbu endpoint foydalanuvchini ID orqali olib keladi`               | `@Description Tizimga kirish endpointi`                                                    |
| `@Security`          | Endpointga autentifikatsiya kerakligini ko‘rsatadi                                          | `@Security ApiKeyAuth`                                                             | `@Security BearerAuth`                                                                     |

---

## 🧪 Amaliyot 1: `main.go` faylida umumiy Swagger konfiguratsiyasi

```go
// @title Electron Navbat API
// @version 1.0
// @description Bu API navbat tizimi uchun mo‘ljallangan.
// @termsOfService http://navbat.uz/terms/

// @contact.name Admin
// @contact.email admin@navbat.uz

// @license.name MIT
// @license.url https://opensource.org/licenses/MIT

// @host localhost:8080
// @BasePath /api/v1

package main
```

---

## 🧪 Amaliyot 2: Foydalanuvchini olish endpointi uchun kommentariyalar

```go
// GetUserByID godoc
// @Summary Foydalanuvchini ID orqali olish
// @Description Ushbu endpoint foydalanuvchini ID orqali olib keladi
// @Tags users
// @Accept json
// @Produce json
// @Param id path int true "Foydalanuvchi ID"
// @Success 200 {object} models.User
// @Failure 404 {object} models.ErrorResponse
// @Router /users/{id} [get]
func (h *Handler) GetUserByID(c echo.Context) error {
    // implementation
}
```

---

## 🛠 Amaliyot 3: Swagger hujjatlarini generatsiya qilish

1. Terminalda quyidagilarni bajaring:

```bash
go install github.com/swaggo/swag/cmd/swag@latest
```

2. Swagger fayllarini yaratish:

```bash
swag init -g api/api.go -o api/docs
```

> `-g` buyrug‘i bilan asosiy fayl ko‘rsatiladi (`main.go` yoki `api.go`).
> `-o` buyrug‘i bilan generatsiya natijasi qayerga yozilishini ko‘rsatiladi.

---

## ✅ Eslatma

- Har bir endpointning tepasida `@Router`, `@Summary`, `@Param`, `@Success`, va `@Failure` yozilishi kerak.
- Modellar (`models.User`, `models.ErrorResponse`) to‘liq aniqlangan bo‘lishi kerak.
- Swagger fayllarini `http://localhost:8080/swagger/index.html` da ko‘rishingiz mumkin (Echo yoki Gin bilan).

---

## 📚 Foydali havolalar

- [Swaggo GitHub sahifasi](https://github.com/swaggo/swag)
- [Swaggo Echo Integration](https://github.com/swaggo/echo-swagger)
- [OpenAPI Specification](https://swagger.io/specification/)
