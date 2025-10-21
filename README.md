# Weekly Grocery Management Database System

A comprehensive database-driven application for managing weekly grocery shopping, tracking expenses, and analyzing purchasing patterns.

## Team Members
- Manasi Mali
- Samiksha Dalvi  
- Tzu-Chun Kuo

## Features

### Core Functionality
- **User Management**: Secure registration and login system
- **Product Catalog**: Browse and search products by category
- **Shopping Lists**: Create and manage weekly shopping lists
- **Purchase Tracking**: Record purchases with store and payment details
- **Expense Monitoring**: Track spending patterns over time
- **Analytics Dashboard**: Visualize spending trends and product statistics
- **Inventory Management**: Monitor stock levels
- **Smart Recommendations**: Generate lists from frequently purchased items

### Key Capabilities
- Multi-user support with individual profiles
- Category-based product organization
- Real-time expense tracking
- Historical purchase analysis
- Automated shopping list generation
- Comprehensive reporting system

## Technology Stack
- **Database**: MySQL 8.0+
- **Backend**: Python 3.8+
- **Frontend**: Streamlit
- **Visualization**: Plotly
- **Security**: SHA-256 password hashing

## Prerequisites

Before you begin, ensure you have the following installed:
- Python 3.8 or higher
- MySQL 8.0 or higher
- pip (Python package manager)
- Git (optional, for cloning repository)

## Installation Guide

### Step 1: Install MySQL

#### Windows
1. Download MySQL Installer from https://dev.mysql.com/downloads/installer/
2. Run the installer and choose "Developer Default"
3. Set root password when prompted (remember this!)
4. Complete the installation

#### Mac
```bash
# Using Homebrew
brew install mysql
brew services start mysql
mysql_secure_installation  # Set root password
```

#### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install mysql-server
sudo mysql_secure_installation  # Set root password
```

### Step 2: Set Up Project Directory

```bash
# Create project directory
mkdir weekly-grocery-management
cd weekly-grocery-management

# Create subdirectories
mkdir database src
```

### Step 3: Create Python Virtual Environment

#### Windows
```bash
python -m venv venv
venv\Scripts\activate
```

#### Mac/Linux
```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 4: Install Python Dependencies

Create `requirements.txt` file with this content:
```
streamlit==1.28.0
mysql-connector-python==8.2.0
pandas==2.1.1
plotly==5.17.0
python-dotenv==1.0.0
```

Install dependencies:
```bash
pip install -r requirements.txt
```

### Step 5: Set Up MySQL Database

1. **Connect to MySQL:**
```bash
mysql -u root -p
# Enter your root password
```

2. **Create the database:**
```sql
CREATE DATABASE grocery_management;
USE grocery_management;
```

3. **Run the schema file** (copy content from schema.sql artifact above):
```sql
-- Copy and paste the entire schema.sql content here
-- Or run: source database/schema.sql
```

4. **Load sample data** (copy content from sample_data.sql artifact above):
```sql
-- Copy and paste the entire sample_data.sql content here
-- Or run: source database/sample_data.sql
```

5. **Verify installation:**
```sql
SHOW TABLES;
-- Should show 8 tables + 3 views
```

6. **Exit MySQL:**
```sql
EXIT;
```

### Step 6: Configure Environment Variables

Create `.env` file in project root:
```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_mysql_password_here
DB_NAME=grocery_management
DB_PORT=3306
DEBUG=False
SECRET_KEY=your-secret-key-here
```

**Important**: Replace `your_mysql_password_here` with your actual MySQL root password!

### Step 7: Save Application Files

1. Save the **app.py** content from the artifact above as `app.py`
2. Save the **config.py** content from the artifact above as `config.py`

### Step 8: Run the Application

```bash
# Make sure virtual environment is activated
# Run Streamlit app
streamlit run app.py
```

The application will open in your browser at http://localhost:8501

## Default Login Credentials

Use these test accounts to explore the system:

| Username | Password | Description |
|----------|----------|-------------|
| john_doe | password123 | User with purchase history |
| jane_smith | password123 | User with party shopping |
| test_user | test123 | Clean test account |

## Usage Guide

### First Time Setup
1. Open the application in your browser
2. Register a new account or use test credentials
3. Explore the dashboard to see spending overview
4. Create your first shopping list
5. Make a test purchase
6. View analytics and reports

### Creating a Shopping List
1. Navigate to "📝 Shopping Lists"
2. Go to "Create New List" tab
3. Enter list name and date
4. Select products from categories
5. Specify quantities
6. Click "Create Shopping List"

### Recording a Purchase
1. Navigate to "🛍️ Make Purchase"
2. Optional: Select existing shopping list
3. Enter store name
4. Select payment method
5. Choose products and quantities
6. Review total amount
7. Click "Complete Purchase"

### Viewing Analytics
1. Navigate to "📊 Analytics"
2. Select date range
3. View spending trends
4. Analyze category distribution
5. Check top purchased products

## Troubleshooting

### Common Issues and Solutions

#### MySQL Connection Error
**Error**: "Error connecting to database: Access denied"
**Solution**: 
- Check your MySQL password in .env file
- Ensure MySQL service is running
- Verify database exists: `mysql -u root -p -e "SHOW DATABASES;"`

#### Module Not Found Error
**Error**: "ModuleNotFoundError: No module named 'streamlit'"
**Solution**:
- Activate virtual environment: `source venv/bin/activate` (Mac/Linux) or `venv\Scripts\activate` (Windows)
- Reinstall requirements: `pip install -r requirements.txt`

#### Port Already in Use
**Error**: "Port 8501 is already in use"
**Solution**:
- Kill existing process: `lsof -ti:8501 | xargs kill -9` (Mac/Linux)
- Or use different port: `streamlit run app.py --server.port 8502`

#### Database Tables Not Found
**Error**: "Table 'grocery_management.Users' doesn't exist"
**Solution**:
- Run schema.sql again
- Check if database exists: `USE grocery_management;`
- Verify tables: `SHOW TABLES;`

### Resetting the Database
If you need to start fresh:
```sql
DROP DATABASE IF EXISTS grocery_management;
CREATE DATABASE grocery_management;
USE grocery_management;
-- Then run schema.sql and sample_data.sql again
```

## Database Schema

### Tables
- **Users**: User accounts and profiles
- **Categories**: Product categories
- **Products**: All grocery items
- **Inventory**: Stock levels
- **ShoppingLists**: User shopping lists
- **ShoppingListItems**: Items in each list
- **Orders**: Completed purchases
- **OrderDetails**: Items in each order

### Key Relationships
- Users → ShoppingLists (One-to-Many)
- Users → Orders (One-to-Many)
- Products → Categories (Many-to-One)
- ShoppingLists → ShoppingListItems → Products
- Orders → OrderDetails → Products

## Project Structure
```
weekly-grocery-management/
│
├── database/
│   ├── schema.sql          # Database structure
│   ├── sample_data.sql     # Sample data
│   └── er_diagram.png      # Entity relationship diagram
│
├── src/                    # Source code (if modularized)
│
├── app.py                  # Main Streamlit application
├── config.py              # Configuration settings
├── requirements.txt       # Python dependencies
├── .env                   # Environment variables (not in git)
└── README.md             # This file
```

## Features Breakdown

### Dashboard
- Monthly spending summary
- Order count metrics
- Active shopping lists
- Favorite category analysis
- Recent purchase history

### Shopping Lists
- Create custom lists
- Generate from frequent items
- Track purchased items
- Calculate estimated costs
- Manage multiple lists

### Purchase Management
- Link to shopping lists
- Manual product selection
- Multiple payment methods
- Store tracking
- Real-time total calculation

### Analytics
- Spending trend charts
- Category distribution pie chart
- Store comparison analysis
- Top products report
- Custom date ranges

### Expense Tracker
- Monthly comparisons
- Detailed expense reports
- CSV export functionality
- Historical data analysis
- Budget tracking (planned)

## Future Enhancements

### Planned Features
- [ ] Email notifications for low stock
- [ ] Budget planning and alerts
- [ ] Recipe suggestions based on purchases
- [ ] Price comparison between stores
- [ ] Barcode scanning support
- [ ] Mobile app version
- [ ] Shared family lists
- [ ] Coupon management
- [ ] Nutritional tracking
- [ ] AI-powered recommendations

## Contributing

This is an academic project. For contributions:
1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## Support

For issues or questions:
- Check the Troubleshooting section
- Review MySQL and Streamlit documentation
- Contact the development team

## License

This project is created for academic purposes as part of a database management course.

## Acknowledgments

- Course instructors for guidance
- MySQL for database management
- Streamlit for the web framework
- Plotly for data visualization

---

**Project Status**: ✅ Complete and Functional

**Last Updated**: 2024

**Version**: 1.0.0
