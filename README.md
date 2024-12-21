# Leapcell Neon Example

Neon combines all the features developers love about Postgres (reliability, performance, scalability) and offers it as a serverless product, helping you deliver reliable and scalable applications faster than ever.

## Getting Started

1. Create a Neon account.
2. Go to the [Neon Dashboard](https://console.neon.tech/app/projects) and click `New Project`.
3. Once the project is created, open it.

You will see a `Connection string` similar to the following:

```
postgresql://neondb_owner:***@******ep-gentle-math-***********.us-east-1.aws.neon.tech/neondb?sslmode=require
```

You can use this connection string with popular ORMs or directly in your code.

---

## Example Usage

### Using Node.js (Prisma ORM)

1. Install Prisma:
   ```bash
   npm install prisma @prisma/client
   ```
2. Initialize Prisma:
   ```bash
   npx prisma init
   ```
3. Update your `prisma/schema.prisma` file:

   ```prisma
   datasource db {
     provider = "postgresql"
     url      = "postgresql://neondb_owner:***@******ep-gentle-math-***********.us-east-1.aws.neon.tech/neondb?sslmode=require"
   }

   generator client {
     provider = "prisma-client-js"
   }

   model User {
     id    Int    @id @default(autoincrement())
     name  String
     email String @unique
   }
   ```

4. Run migrations and use the database:
   ```bash
   npx prisma migrate dev
   ```

---

### Using Python (Django ORM)

1. Install dependencies:
   ```bash
   pip install django psycopg2-binary
   ```
2. Update your `settings.py` in the Django project:
   ```python
   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.postgresql',
           'NAME': 'neondb',
           'USER': 'neondb_owner',
           'PASSWORD': 'your_password',
           'HOST': '******ep-gentle-math-***********.us-east-1.aws.neon.tech',
           'PORT': '5432',
           'OPTIONS': {
               'sslmode': 'require',
           },
       }
   }
   ```

---

### Using Node.js Without an ORM

1. Install the `pg` library:
   ```bash
   npm install pg
   ```
2. Connect to Neon:

   ```javascript
   const { Client } = require("pg");

   const client = new Client({
     connectionString:
       "postgresql://neondb_owner:***@******ep-gentle-math-*********.us-east-1.aws.neon.tech/neondb?sslmode=require",
   });

   client
     .connect()
     .then(() => console.log("Connected to Neon"))
     .catch((err) => console.error("Connection error", err.stack));
   ```

---

### Using Python Without an ORM

1. Install `psycopg2`:
   ```bash
   pip install psycopg2
   ```
2. Connect to Neon:

   ```python
   import psycopg2

   connection = psycopg2.connect(
       dbname="neondb",
       user="neondb_owner",
       password="your_password",
       host="******ep-gentle-math-***********.us-east-1.aws.neon.tech",
       port="5432",
       options="-c sslmode=require"
   )

   print("Connected to Neon")
   ```

Now you're ready to use Neon for your application with Node.js or Python! 🎉
