# MandáTodo Logística

[Español](README.md) · **English**

Web system for a last-mile logistics company that receives orders through WhatsApp, Instagram, email and other channels. Its main goal is to **normalize and geolocate delivery addresses** to avoid failed trips, and to follow each order from entry through delivery and payment.

Academic project PPP1 · Group 9 · Case 7.

## Features

### Users and access
- Login with individual accounts and JWT tokens.
- Three roles with separate permissions: **Administrator**, **Operator** and **Driver**. Permissions are enforced on the server.
- User management (administrator only).

### Customers
- Customer management with search by name, ID number (DNI), phone or email.
- DNI normalization and rejection of duplicate DNIs; warning (no automatic merge) on repeated phone or email.
- Per-customer address book to reuse addresses from previous shipments.

### Orders and addresses
- Manual order entry with a structured address (street, number, floor/apartment, cross streets, locality, province, postal code) and source channel.
- Normalization of Argentine provinces and localities (24 jurisdictions, locality catalog).
- Address geocoding and location preview on a map during entry.
- **Mandatory human confirmation** of the location: an employee reviews the point on the map and confirms or rejects it. If the address changes, the confirmation is invalidated.
- Review queue for pending addresses.
- Alert for potentially duplicate orders (same customer and same address within a time window).
- General order list with filters by status, validation status, customer and dates.

### Rates and amounts
- Configuration of the price per kilometer and the origin branch (administrator).
- Suggested amount based on the distance between the branch and the delivery point, also available during entry.

### Assignment and delivery
- Manual assignment of orders to drivers (only with a confirmed address and an active driver).
- Preparation and dispatch status changes with status history.
- Driver view with assigned orders, delivery and payment recording.
- Payment receipt upload by the driver and payment approval by the administrator.

### Export and import
- Export of an order's information and map to PDF.
- Import of historical orders from Excel, with data cleanup.

## Technologies

| Layer | Technologies |
| --- | --- |
| Frontend | React 19, Vite 8, React Router 7, Axios, Leaflet + React Leaflet (maps), jsPDF and pdf.js (PDF), ESLint, Vitest |
| Backend | Node.js 24, Express 5 (CommonJS), JSON Web Token, bcryptjs (password hashing), Zod (validation), mysql2, xlsx (Excel import), dotenv |
| Database | MySQL 8.4 with versioned migrations |
| Geolocation | Georef API (official Argentine geographic data) and Leaflet maps; alternative adapters prepared for Nominatim and Google |
| Infrastructure | Docker and Docker Compose (MySQL, backend and frontend services) |

## Structure

| Folder | Contents |
| --- | --- |
| `frontend/` | React web app (pages, components, API client, session and role guards) |
| `backend/` | Express REST API organized into routes, controllers, services and repositories |
| `database/` | SQL schema and migrations |
| `docs/` | Project documentation: context, architecture, decisions and tasks (in Spanish) |

## Getting started

Installation, Docker, migrations and local execution in [docs/arranque.md](docs/arranque.md) (in Spanish).
