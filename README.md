### Database Design (MySQL)

#### Tables:

1. **users**
   - `id` (Primary Key, Auto Increment)
   - `first_name` (VARCHAR)
   - `last_name` (VARCHAR)
   - `email` (VARCHAR, UNIQUE)
   - `phone_number` (VARCHAR)

2. **properties**
   - `id` (Primary Key, Auto Increment)
   - `title` (VARCHAR)
   - `description` (TEXT)
   - `location` (VARCHAR)
   - `area` (VARCHAR)
   - `bedrooms` (INT)
   - `bathrooms` (INT)
   - `price` (DECIMAL)
   - `near_by` (VARCHAR)
   - `image_url` (VARCHAR)
   - `seller_id` (Foreign Key referencing `users.id`)

3. **likes**
   - `id` (Primary Key, Auto Increment)
   - `property_id` (Foreign Key referencing `properties.id`)
   - `buyer_id` (Foreign Key referencing `users.id`)

4. **interested_buyers**
   - `id` (Primary Key, Auto Increment)
   - `property_id` (Foreign Key referencing `properties.id`)
   - `buyer_id` (Foreign Key referencing `users.id`)

### API Design with MySQL Queries

#### 1. User Registration
- **Path**: `/api/register`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "first_name": "string",
    "last_name": "string",
    "email": "string",
    "phone_number": "string"
  }
  ```
- **MySQL Query**:
  ```sql
  INSERT INTO users (first_name, last_name, email, phone_number)
  VALUES ('first_name_value', 'last_name_value', 'email_value', 'phone_number_value');
  ```

#### 2. User Login
- **Path**: `/api/login`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "email": "string",
    "password": "string"
  }
  ```
- **MySQL Query**:
  ```sql
  SELECT * FROM users WHERE email = 'email_value' AND password = 'password_value';
  ```

#### 3. Add Property (Seller Action)
- **Path**: `/api/properties`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "title": "string",
    "description": "string",
    "location": "string",
    "area": "float",
    "bedrooms": "int",
    "bathrooms": "int",
    "price": "decimal",
    "near_by": "string",
    "image_url": "string",
    "user_id": "int" // Seller ID
  }
  ```
- **MySQL Query**:
  ```sql
  INSERT INTO properties (title, description, location, area, bedrooms, bathrooms, price, near_by, image_url, seller_id)
  VALUES ('title_value', 'description_value', 'location_value', 'area_value', 'bedrooms_value', 'bathrooms_value', 'price_value', 'near_by_value', 'image_url_value', 'user_id_value');
  ```

#### 4. Get All Properties (Buyer)
- **Path**: `/api/properties`
- **Method**: `GET`
- **MySQL Query**:
  ```sql
  SELECT * FROM properties;
  ```

#### 5. Get Property Details
- **Path**: `/api/properties/:id`
- **Method**: `GET`
- **MySQL Query**:
  ```sql
  SELECT * FROM properties WHERE id = 'property_id_value';
  ```

#### 6. Update Property
- **Path**: `/api/properties/:id`
- **Method**: `PUT`
- **Request Body**: (Similar to Add Property)
- **MySQL Query**:
  ```sql
  UPDATE properties
  SET title = 'title_value', description = 'description_value', location = 'location_value', area = 'area_value',
      bedrooms = 'bedrooms_value', bathrooms = 'bathrooms_value', price = 'price_value', near_by = 'near_by_value', image_url = 'image_url_value'
  WHERE id = 'property_id_value';
  ```

#### 7. Delete Property
- **Path**: `/api/properties/:id`
- **Method**: `DELETE`
- **MySQL Query**:
  ```sql
  DELETE FROM properties WHERE id = 'property_id_value';
  ```

#### 8. Mark Property as Interested (Buyer Action)
- **Path**: `/api/properties/:id/interested`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "user_id": "int" // Buyer ID
  }
  ```
- **MySQL Query**:
  ```sql
  INSERT INTO interested_buyers (property_id, buyer_id)
  VALUES ('property_id_value', 'user_id_value');
  ```

#### 9. Add Like to Property (Buyer Action)
- **Path**: `/api/properties/:id/like`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "user_id": "int" // User ID
  }
  ```
- **MySQL Query**:
  ```sql
  INSERT INTO likes (property_id, user_id)
  VALUES ('property_id_value', 'user_id_value');
  ```

#### 10. Get Seller Details
- **Path**: `/api/sellers/:id/details`
- **Method**: `GET`
- **MySQL Query**:
  ```sql
  SELECT * FROM properties WHERE seller_id = 'user_id_value';
  ```
#### 11. Get All Properties (Seller)
- **Path**: `/api/sellers/:id/properties`
- **Method**: `GET`
- **MySQL Query**:
  ```sql
  SELECT * FROM properties WHERE seller_id = 'seller_id_value';
  ```
  
This final design consolidates everything with the requested changes and includes the MySQL queries for each API endpoint, incorporating the single image URL directly in the `properties` table. Let me know if there are any additional requirements or further modifications needed.
