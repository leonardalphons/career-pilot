# Online Boutique and Fashion Design Platform

A full-stack e-commerce platform for a fashion boutique, built as a production-quality, deployable application submitted for the AZ-900 (Microsoft Azure Fundamentals) certification course.

## Overview

This project is a complete online store where customers can browse products, manage a cart, and place orders, while admins can manage inventory through a role-based dashboard. It was built end-to-end — from monorepo scaffolding to live cloud deployment on Microsoft Azure — with no steps skipped.

## Features

- User authentication — JWT-based signup/login with bcrypt password hashing
- Role-based access control — separate customer and admin permissions
- Product catalog\*\* — browse, view, and manage fashion products
- Image uploads — product images stored in Azure Blob Storage
- Shopping cart — persistent cart using React Context API + localStorage
- Order management — place and track orders
- Admin dashboard — add, edit, and manage products and orders

## Tech Stack

| Layer | Technology |
| Frontend | React (Vite) + Tailwind CSS |
| Backend | Node.js + Express |
| Database | MongoDB Atlas |
| File Storage | Azure Blob Storage (`@azure/storage-blob` SDK) |
| Auth | JWT + bcrypt |
| Hosting | Microsoft Azure App Service (frontend + backend, separate instances) |
| Region | Central India |

## Architecture

The project is structured as a monorepo with separate frontend and backend services, each deployed independently:

```
boutique-platform/
├── frontend/     # React (Vite) + Tailwind CSS
└── backend/      # Node.js + Express + Mongoose
```

- Frontend deployed to Azure App Service: `frontend.centralindia-01.azurewebsites.net`
- Backend deployed to Azure App Service: `backend.centralindia-01.azurewebsites.net`
- Resource Group: `boutique-rg`
- Database: MongoDB Atlas (cloud-hosted)
- Images: Uploaded via Multer, stored in Azure Blob Storage with public read access

## Data Models

- User — auth credentials, role (customer/admin)
- Product — name, description, price, images, stock
- Order — user reference, product line items, status

## Getting Started

### Prerequisites

- Node.js (LTS version)
- MongoDB Atlas account and connection string
- Azure account with:
  - An App Service for the frontend
  - An App Service for the backend
  - A Storage Account with a Blob container

### Environment Variables

Create a `.env` file in the `backend/` directory (this file is git-ignored):

```
MONGODB_URI=your_mongodb_atlas_connection_string
JWT_SECRET=your_jwt_secret
AZURE_STORAGE_CONNECTION_STRING=your_azure_blob_connection_string
AZURE_STORAGE_CONTAINER_NAME=your_container_name
PORT=5000
```

### Installation

```bash
# Clone the repository
git clone <your-repo-url>
cd boutique-platform

# Install backend dependencies
cd backend
npm install

# Install frontend dependencies
cd ../frontend
npm install
```

### Running Locally

```bash
# Start the backend
cd backend
npm start

# Start the frontend (in a separate terminal)
cd frontend
npm run dev
```

## Deployment

Both frontend and backend are deployed as separate Azure App Services in the Central India region under the `boutique-rg` Resource Group. Deployment uses Azure's SCM/Kudu publishing with Basic Auth enabled manually in the App Service configuration.

## Known Issues Resolved During Development

- Defensive array checks added to guard against malformed API responses
- Port mismatch fixed between frontend and backend during local development
- Azure Blob Storage container access changed from private (default) to public read
- Updated Express 5 wildcard route syntax (`*` → `/*splat`)
- Resolved an ES Module vs CommonJS conflict in the frontend server file

## Project Deliverables

- Deployed full-stack application (frontend + backend on Azure)
- Canva AI-generated presentation summarizing the project
- Screen-recorded demo video walking through the platform's features

## License

This project was created for educational purposes as part of an AZ-900 certification course submission.
