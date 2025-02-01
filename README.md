import Link from "next/link";

const Navbar = () => {
  return (
    <nav className="bg-gray-900 text-white p-4">
      <div className="container mx-auto flex justify-between items-center">
        <Link href="/">
          <h1 className="text-2xl font-bold cursor-pointer">MyShop</h1>
        </Link>
        <ul className="flex space-x-4">
          <li><Link href="/products">Products</Link></li>
          <li><Link href="/cart">Cart</Link></li>
        </ul>
      </div>
    </nav>
  );
};

export default Navbar;
import Image from "next/image";

const ProductCard = ({ product }) => {
  return (
    <div className="border p-4 rounded-lg shadow-lg">
      <Image src={product.image} alt={product.name} width={200} height={200} />
      <h2 className="text-lg font-bold mt-2">{product.name}</h2>
      <p className="text-gray-600">${product.price}</p>
      <button className="bg-blue-500 text-white px-4 py-2 mt-2 rounded">Add to Cart</button>
    </div>
  );
};

export default ProductCard;
import ProductCard from "../components/ProductCard";

const products = [
  { id: 1, name: "Product 1", price: 29.99, image: "/product1.jpg" },
  { id: 2, name: "Product 2", price: 49.99, image: "/product2.jpg" },
];

export default function Products() {
  return (
    <div className="container mx-auto p-4">
      <h1 className="text-2xl font-bold mb-4">Products</h1>
      <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
        {products.map((product) => (
          <ProductCard key={product.id} product={product} />
        ))}
      </div>
    </div>
  );
}
import { createContext, useState, useContext } from "react";

const CartContext = createContext();

export const CartProvider = ({ children }) => {
  const [cart, setCart] = useState([]);

  const addToCart = (product) => {
    setCart([...cart, product]);
  };

  return (
    <CartContext.Provider value={{ cart, addToCart }}>
      {children}
    </CartContext.Provider>
  );
};

export const useCart = () => useContext(CartContext);
import "../styles/globals.css";
import { CartProvider } from "../context/CartContext";

function MyApp({ Component, pageProps }) {
  return (
    <CartProvider>
      <Component {...pageProps} />
    </CartProvider>
  );
}

export default MyApp;
import { useCart } from "../context/CartContext";

export default function Cart() {
  const { cart } = useCart();

  return (
    <div className="container mx-auto p-4">
      <h1 className="text-2xl font-bold">Shopping Cart</h1>
      {cart.length === 0 ? (
        <p>Your cart is empty.</p>
      ) : (
        <ul>
          {cart.map((item, index) => (
            <li key={index} className="border-b p-2">
              {item.name} - ${item.price}
            </li>
          ))}
        </ul>
      )}
    </div>
  );
}
import { loadStripe } from "@stripe/stripe-js";

const stripePromise = loadStripe("your-public-stripe-key");

const CheckoutButton = () => {
  const handleCheckout = async () => {
    const stripe = await stripePromise;
    stripe.redirectToCheckout({ sessionId: "your-session-id" });
  };

  return (
    <button onClick={handleCheckout} className="bg-green-500 text-white px-4 py-2 rounded">
      Checkout
    </button>
  );
};

export default CheckoutButton;
