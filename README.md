# VESTRA — Luxury Fashion E-Commerce

A full-stack luxury fashion e-commerce platform built with Node.js, Express, MongoDB, and GSAP animations.

## Quick Start

### 1. Install dependencies
```bash
npm install
```

### 2. Configure environment
```bash
cp .env.example .env
```
Edit `.env` with your MongoDB URI and credentials.

### 3. Generate admin password hash
```bash
node -e "require('bcryptjs').hash('yassin01022950178#', 10).then(h => console.log('ADMIN_PASSWORD_HASH=' + h))"
```
Copy the output hash into your `.env` file.

### 4. Create product images directory
```bash
mkdir -p public/images/products
```

### 5. Start the server
```bash
# Development (with auto-reload)
npm run dev

# Production
npm start
```

Visit `http://localhost:3000`

---

## Structure

```
vestra/
├── public/
│   ├── index.html          # Main storefront (full GSAP animations)
│   ├── admin.html          # Admin dashboard
│   ├── 404.html            # Custom error page
│   └── images/products/    # Uploaded product images
├── models/
│   ├── Product.js          # Product schema (title, price, image, category)
│   └── Order.js            # Order schema (customer, items, status, payment)
├── routes/
│   ├── products.js         # CRUD API for products
│   ├── orders.js           # Order creation + Pushover notifications
│   └── admin.js            # Auth (login/logout/verify)
├── middleware/
│   └── auth.js             # JWT validation middleware
├── server.js               # Express app entry point
└── .env                    # Configuration
```

---

## Features

### Storefront (index.html)
- **GSAP Loader** — Animated entry screen with logo reveal and clip-path exit
- **Parallax Hero** — ScrollTrigger-based parallax on editorial imagery
- **Product Grid** — Real-time search + category filtering
- **Wishlist** — Toggle with localStorage persistence
- **Cart Drawer** — Slide-out with quantity management and totals
- **Checkout** — Full form with Vodafone Cash & InstaPay payment options
- **WhatsApp Integration** — Pre-filled message with order summary
- **Pushover Notifications** — Auto-notifies admin on each new order
- **Scroll Animations** — Fade-up reveals on all sections

### Admin Dashboard (admin.html)
- **JWT Authentication** — Bcrypt password verification, HttpOnly cookies
- **Product CRUD** — Add, edit, delete with image upload
- **Order Management** — Status selector (Pending → Paid → Shipped → Delivered)
- **Dashboard Stats** — Live counts for products, orders, revenue

### Payment Methods
- **Vodafone Cash**: 01013202241
- **InstaPay**: 01022950178
- WhatsApp confirmation to: 01022950178

---

## API Endpoints

| Method | Route | Auth | Description |
|--------|-------|------|-------------|
| GET | /api/products | — | List all products |
| GET | /api/products/:id | — | Get single product |
| POST | /api/products | ✓ | Create product |
| PUT | /api/products/:id | ✓ | Update product |
| DELETE | /api/products/:id | ✓ | Delete product |
| POST | /api/orders | — | Place new order |
| GET | /api/orders | ✓ | List all orders |
| PUT | /api/orders/:id/status | ✓ | Update order status |
| POST | /api/admin/login | — | Admin login |
| GET | /api/admin/verify | ✓ | Verify token |
| POST | /api/admin/logout | — | Logout |

---

## Pushover Setup
1. Create account at [pushover.net](https://pushover.net)
2. Create an application to get your `APP_TOKEN`
3. Copy your `USER_KEY` from dashboard
4. Add both to `.env`:
   ```
   PUSHOVER_USER_KEY=your_key
   PUSHOVER_APP_TOKEN=your_token
   ```

---

## Production Checklist
- [ ] Set strong `JWT_SECRET` in `.env`
- [ ] Set `NODE_ENV=production`
- [ ] Generate and store bcrypt hash for admin password
- [ ] Configure MongoDB Atlas or production DB
- [ ] Add Pushover credentials
- [ ] Set up SSL/HTTPS (nginx or Cloudflare)
- [ ] Configure `public/images/products/` as persistent volume
