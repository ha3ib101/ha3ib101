Here’s a simple e-commerce website using Next.js and Tailwind CSS with a homepage and a products page.

1. Setup Project

Run the following commands:

npx create-next-app@latest myshop
cd myshop
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p

Configure tailwind.config.js:

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./pages/**/*.{js,ts,jsx,tsx}", "./components/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};

Add Tailwind to styles/globals.css:

@tailwind base;
@tailwind components;
@tailwind utilities;

2. Create Components

Navbar

Create components/Navbar.js:

import Link from "next/link";

const Navbar = () => {
  return (
    <nav className="bg-blue-600 text-white p-4">
      <div className="container mx-auto flex justify-between items-center">
        <Link href="/">
          <h1 className="text-2xl font-bold">MyShop</h1>
        </Link>
        <ul className="flex space-x-4">
          <li><Link href="/">Home</Link></li>
          <li><Link href="/products">Products</Link></li>
        </ul>
      </div>
    </nav>
  );
};

export default Navbar;

Product Card

Create components/ProductCard.js:

const ProductCard = ({ product }) => {
  return (
    <div className="border p-4 rounded-lg shadow-md">
      <h2 className="text-lg font-bold">{product.name}</h2>
      <p className="text-gray-600">${product.price}</p>
      <button className="bg-green-500 text-white px-4 py-2 mt-2 rounded">
        Buy Now
      </button>
    </div>
  );
};

export default ProductCard;

3. Create Pages

Homepage

Modify pages/index.js:

import Navbar from "../components/Navbar";

export default function Home() {
  return (
    <>
      <Navbar />
      <div className="container mx-auto p-4">
        <h1 className="text-3xl font-bold">Welcome to MyShop</h1>
        <p className="text-gray-600">Your one-stop shop for amazing products!</p>
      </div>
    </>
  );
}

Products Page

Create pages/products.js:

import Navbar from "../components/Navbar";
import ProductCard from "../components/ProductCard";

const products = [
  { id: 1, name: "Product 1", price: 20 },
  { id: 2, name: "Product 2", price: 35 },
];

export default function Products() {
  return (
    <>
      <Navbar />
      <div className="container mx-auto p-4">
        <h1 className="text-2xl font-bold">Products</h1>
        <div className="grid grid-cols-2 gap-4 mt-4">
          {products.map((product) => (
            <ProductCard key={product.id} product={product} />
          ))}
        </div>
      </div>
    </>
  );
}

4. Run the Website

Start the development server:

npm run dev

Now visit http://localhost:3000 to see your simple e-commerce website!

Would you like any extra features?
