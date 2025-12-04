# Weekly Grocery Management Database System

A comprehensive database-driven web application for managing weekly groceries. This system helps families efficiently organize and track weekly grocery needs, reducing problems such as forgotten items, budget overruns, and poor inventory tracking.

## Features

### 🔐 User Authentication
- Secure user registration and login
- Password hashing using SHA-256
- Session management

### 📦 Product Management
- Full CRUD operations for products
- Category-based organization
- Search and filter functionality
- Brand and unit measurement tracking

### 📝 Shopping Lists
- Create and manage multiple shopping lists
- Add/remove items with quantities
- Mark items as purchased
- Convert shopping lists to orders
- Estimated total calculation

### 🛒 Order Processing
- Create new orders manually
- Complete and cancel orders
- Full order history with details
- Automatic total calculation

### 📊 Analytics & Reports
- Spending by category (pie and bar charts)
- Monthly spending trends
- Most purchased products
- Weekly spending summary
- Personalized product suggestions

## System Architecture

The system follows a three-layered architecture:

1. **Database Layer**: SQLite database for persistent storage
2. **Application Layer**: Python with Streamlit for business logic
3. **Visualization Layer**: Plotly for interactive charts

## Database Schema

### Entity-Relationship Diagram

```
USERS ─────────┬──────────── ORDERS
               │              │
               │              │
               │         ORDERDETAILS
               │              │
               │              │
CATEGORIES ────┼──────────── PRODUCTS
               │
               │
SHOPPING_LISTS ┴── SHOPPING_LIST_ITEMS
```

### Tables

| Table | Description |
|-------|-------------|
| **users** | Stores user credentials and profile information |
| **categories** | Product categories (Dairy, Fruits, Vegetables, etc.) |
| **products** | Grocery items with name, brand, price, and unit measure |
| **orders** | Purchase records with date, total amount, and status |
| **order_details** | Links orders to products with quantity and subtotal |
| **shopping_lists** | Weekly or custom shopping lists |
| **shopping_list_items** | Items within each shopping list |

### Table Relationships

- **Users** → One-to-Many → **Orders**
- **Users** → One-to-Many → **Shopping Lists**
- **Categories** → One-to-Many → **Products**
- **Orders** → One-to-Many → **Order Details**
- **Products** → One-to-Many → **Order Details**
- **Shopping Lists** → One-to-Many → **Shopping List Items**
- **Products** → One-to-Many → **Shopping List Items**

## Installation

### Prerequisites
- Python 3.8 or higher
- pip (Python package manager)

### Setup

1. Clone or download the project files

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Run the application:
```bash
streamlit run app.py
```

4. Open your browser and navigate to `http://localhost:8501`

## Usage

### Demo Account
Use the following credentials to explore the system:
- **Username**: `demo_user`
- **Password**: `password123`

Click "Load Sample Data" on the login page to populate the database with sample categories and products.

### Getting Started

1. **Register** a new account or use the demo account
2. **Browse Products** in the Products section
3. **Create a Shopping List** for your weekly groceries
4. **Add items** to your shopping list
5. **Convert to Order** when you're ready to shop
6. **View Reports** to analyze your spending patterns

## Project Structure

```
grocery_management/
├── app.py              # Main Streamlit application
├── database.py         # Database operations and models
├── requirements.txt    # Python dependencies
├── README.md          # Project documentation
└── grocery_management.db  # SQLite database (created on first run)
```

## Technical Specifications

### Database Operations (CRUD)

**Users**
- Create: `create_user(username, email, password)`
- Read: `get_user_by_username()`, `get_user_by_id()`, `get_all_users()`
- Authenticate: `authenticate_user(username, password)`

**Categories**
- Create: `create_category(name, description)`
- Read: `get_all_categories()`, `get_category_by_id()`
- Update: `update_category(id, name, description)`
- Delete: `delete_category(id)`

**Products**
- Create: `create_product(name, category_id, price, brand, unit)`
- Read: `get_all_products()`, `get_product_by_id()`, `search_products()`
- Update: `update_product(id, name, category_id, price, brand, unit)`
- Delete: `delete_product(id)`

**Orders**
- Create: `create_order(user_id)`
- Add Items: `add_order_detail(order_id, product_id, quantity)`
- Complete: `complete_order(order_id)`
- Delete: `delete_order(order_id)`

**Shopping Lists**
- Create: `create_shopping_list(user_id, name)`
- Add Items: `add_item_to_shopping_list(list_id, product_id, quantity)`
- Toggle Status: `toggle_shopping_list_item(item_id)`
- Convert to Order: `convert_shopping_list_to_order(list_id, user_id)`

### Analytics Functions

- `get_spending_by_category(user_id, start_date, end_date)`
- `get_monthly_spending(user_id, year)`
- `get_most_purchased_products(user_id, limit)`
- `get_weekly_spending(user_id)`
- `get_total_spending(user_id)`
- `get_suggested_products(user_id, limit)`

## Sample Data Categories

1. **Dairy** - Milk, cheese, yogurt, butter, eggs
2. **Fruits** - Bananas, apples, strawberries, oranges, grapes
3. **Vegetables** - Broccoli, carrots, spinach, tomatoes, potatoes
4. **Meat & Poultry** - Chicken, beef, salmon, bacon, turkey
5. **Beverages** - Juice, coffee, tea, sparkling water, almond milk
6. **Bakery** - Bread, bagels, croissants, tortillas, muffins
7. **Frozen Foods** - Ice cream, pizza, frozen vegetables
8. **Snacks** - Chips, pretzels, trail mix, granola bars
9. **Household** - Paper towels, soap, detergent, trash bags
10. **Personal Care** - Shampoo, toothpaste, body wash

## Authors

- Manasi Mali - Indiana University-Indianapolis
- Samiksha Dalvi - Indiana University-Indianapolis
- Tzu-Chun Kuo - Indiana University-Indianapolis

## License

This project is part of the Database Systems course at Indiana University-Indianapolis.