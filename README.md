# Sales Analytics API

A NestJS-based REST API for analyzing sales data from CSV files.

## Prerequisites

- Node.js (v22.16.0 or higher)
- PostgreSQL (v17.5)
- npm or yarn package manager

## Setup

1. Clone the repository:
```bash
git clone <repository-url>
cd sales-analytics-api
```

2. Install dependencies:
```bash
npm install
```

3. Create a PostgreSQL database named `sales_analytics`

4. Configure environment variables:
Create a `.env` file in the root directory (at the same level as package.json) with the following content:
```
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=postgres
DB_DATABASE=sales_analytics
PORT=3000
```
> **Note:**  
> - Make sure your PostgreSQL server is running and the credentials above match your local setup.
> - The `PORT` variable sets the port for the NestJS server (default: 3000).
> - Never commit your `.env` file to public repositories.

5. Start the application:
```bash
npm run start:dev
```

## API Endpoints

> Interactive API docs are available at [http://localhost:3000/api](http://localhost:3000/api) after starting the server.

### Data Loading

#### Upload CSV File
- **URL**: `/analytics/upload`
- **Method**: `POST`
- **Content-Type**: `multipart/form-data`
- **Body**: 
  - `file`: CSV file containing sales data
- **Response**:
```json
{
  "message": "Data loaded successfully"
}
```

### Analytics

#### Get Revenue
- **URL**: `/analytics/revenue`
- **Method**: `GET`
- **Query Parameters**:
  - `startDate`: Start date (YYYY-MM-DD)
  - `endDate`: End date (YYYY-MM-DD)
  - `groupBy`: Optional grouping by 'product', 'category', or 'region'
- **Response**:
```json
{
  "totalRevenue": 15000.00
}
```
or when grouped:
```json
[
  {
    "name": "Electronics",
    "revenue": 5000.00
  },
  {
    "name": "Clothing",
    "revenue": 10000.00
  }
]
```

#### Get Top Products
- **URL**: `/analytics/top-products`
- **Method**: `GET`
- **Query Parameters**:
  - `startDate`: Start date (YYYY-MM-DD)
  - `endDate`: End date (YYYY-MM-DD)
  - `limit`: Number of products to return (default: 10)
  - `category`: Optional category filter
  - `region`: Optional region filter
- **Response**:
```json
[
  {
    "name": "iPhone 15 Pro",
    "totalQuantity": 150
  },
  {
    "name": "UltraBoost Running Shoes",
    "totalQuantity": 100
  }
]
```

#### Get Customer Analysis
- **URL**: `/analytics/customer-analysis`
- **Method**: `GET`
- **Query Parameters**:
  - `startDate`: Start date (YYYY-MM-DD)
  - `endDate`: End date (YYYY-MM-DD)
- **Response**:
```json
{
  "totalCustomers": 500,
  "totalOrders": 1000,
  "avgOrderValue": 150.00
}
```

## CSV File Format

The CSV file should have the following columns:
- Order ID
- Product ID
- Customer ID
- Product Name
- Category
- Region
- Date of Sale
- Quantity Sold
- Unit Price
- Discount
- Shipping Cost
- Payment Method
- Customer Name
- Customer Email
- Customer Address

## Error Handling

The API returns appropriate HTTP status codes and error messages:
- 200: Success
- 400: Bad Request
- 404: Not Found
- 500: Internal Server Error

## Development

### Running Tests
```bash
npm run test
```

### Building for Production
```bash
npm run build
```

### Running in Production
```bash
npm run start:prod
```

## Troubleshooting

- If you get a database connection error, double-check your `.env` values and ensure PostgreSQL is running.
- If you change your `.env`, restart the server to apply changes.
- For file upload issues, ensure your request is `multipart/form-data` and the field name is `file`.

## Description

[Nest](https://github.com/nestjs/nest) framework TypeScript starter repository.

## Project setup

```bash
$ npm install
```

## Compile and run the project

```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

## License

Nest is [MIT licensed](https://github.com/nestjs/nest/blob/master/LICENSE).

node_modules/
dist/
.env
