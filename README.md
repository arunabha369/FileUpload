---

# 📦 File-Upload-Backend

A Node.js + Express backend service for handling **file uploads (images, videos, local files)** with **Cloudinary integration**, **MongoDB (Mongoose)** for metadata, and **Nodemailer** for email notifications.

---

## 🚀 Features

* 📂 Upload files (local, image, video, reduced image size)
* ☁️ Cloud storage with [Cloudinary](https://cloudinary.com/)
* 🗄️ MongoDB database for file metadata
* 📧 Email notifications using Nodemailer after file upload
* 🛡️ MVC architecture (config, controllers, routes, models)
* 🔐 Environment-based configuration with dotenv

---

## 🏗️ Tech Stack

* [Node.js](https://nodejs.org/) + [Express](https://expressjs.com/)
* [MongoDB](https://www.mongodb.com/) + [Mongoose](https://mongoosejs.com/)
* [Cloudinary](https://cloudinary.com/documentation/node_integration)
* [Nodemailer](https://nodemailer.com/about/)
* [express-fileupload](https://www.npmjs.com/package/express-fileupload)

---

## 📂 Project Structure

```
.
├── config/
│   ├── cloudinary.js     # Cloudinary connection
│   ├── database.js       # MongoDB connection
│   └── nodemailer.js     # Nodemailer SMTP transporter config
├── controllers/
│   └── fileUpload.js     # File upload business logic
├── models/
│   └── File.js           # File schema + email hook
├── routes/
│   └── FileUpload.js     # API routes
├── index.js              # Entry point
├── package.json          # Dependencies & scripts
├── NOTICE.txt            # Example env vars
└── .gitignore

```

---

## ⚙️ Setup & Installation

### 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/File-Upload-Backend.git
cd File-Upload-Backend
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

Create a `.env` file in the root:

```env
PORT=4000

MONGODB_URL=your_mongodb_url

CLOUD_NAME=your_cloudinary_cloud_name
API_KEY=your_cloudinary_api_key
API_SECRET=your_cloudinary_api_secret

MAIL_HOST=smtp.yourmail.com
MAIL_USER=your_email@example.com
MAIL_PASS=your_email_password
```

(Reference `NOTICE.txt` for required variables)

### 4. Run the Server

```bash
# Development (with nodemon)
npm run dev

# Production
npm start
```

Server runs at:
👉 `http://localhost:4000`

---

## 📡 API Endpoints

| Method | Path                             | Description                 | Controller        |
| ------ | -------------------------------- | --------------------------- | ----------------- |
| POST   | `/api/v1/upload/localFileUpload` | Uploads file locally        | `localFileUpload` |
| POST   | `/api/v1/upload/imageUpload`     | Uploads image to Cloudinary | `imageUpload`     |
| POST   | `/api/v1/upload/videoUpload`     | Uploads video to Cloudinary | `videoUpload`     |
| POST   | `/api/v1/upload/imageReducer`    | Uploads reduced-size image  | `imageReducer`    |

---

## 📬 Example Usage

### Upload Image

```bash
curl -X POST http://localhost:4000/api/v1/upload/imageUpload \
  -F "imageFile=@./sample.jpg" \
  -F "name=Test Image" \
  -F "tags=demo,upload" \
  -F "email=user@example.com"
```

### Response

```json
{
  "success": true,
  "message": "Image uploaded successfully",
  "fileUrl": "https://res.cloudinary.com/<cloud>/image/upload/abc123.jpg"
}
```

---

## 🛡️ Security Notes

* Add authentication (JWT/API keys) for protected uploads.
* Limit file size in `express-fileupload`.
* Validate MIME types and sanitize input.
* Use signed Cloudinary URLs for private content.

---

## 🚀 Deployment

### Docker Setup (Optional)

`Dockerfile`:

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install --production
COPY . .
EXPOSE 4000
CMD ["npm", "start"]
```

### Run with Docker Compose

```yaml
version: "3"
services:
  app:
    build: .
    ports:
      - "4000:4000"
    env_file: .env
```

Deploy easily to: **Render, Railway, Heroku, AWS, or DigitalOcean**.

---

## 🧪 Testing

* Suggested framework: Jest + Supertest
* Unit tests: controllers & models
* Integration tests: API endpoints (mock Cloudinary + Nodemailer)
* Coverage target: 80%+

---

## 🤝 Contributing

1. Fork the repo
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit changes (`git commit -m "Added new feature"`)
4. Push to branch (`git push origin feature/new-feature`)
5. Open a Pull Request

---

## 📜 License

This project is licensed under the **ISC License** – see [LICENSE](LICENSE) for details.

---
