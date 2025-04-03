{trendkarthub.com} from "module" import { useState, useEffect } from "react"; import Link from "next/link"; import { FaShoppingCart, FaWhatsapp, FaSearch } from "react-icons/fa"; import { Button } from "@/components/ui/button";

export default function Home() { const [cartCount, setCartCount] = useState(0); const [searchTerm, setSearchTerm] = useState(""); const [orderId, setOrderId] = useState(""); const [orderStatus, setOrderStatus] = useState(null); const [trackingProgress, setTrackingProgress] = useState([]);

const products = [ { id: 1, name: "Smart Watch", category: "Accessories", price: "₹1,999", image: "/images/product1.jpg", description: "A stylish smartwatch with multiple features.", reviews: 4.5, images: ["/images/product1_1.jpg", "/images/product1_2.jpg"] }, { id: 2, name: "Wireless Earbuds", category: "Tech Gadgets", price: "₹2,499", image: "/images/product2.jpg", description: "High-quality wireless earbuds with noise cancellation.", reviews: 4.7, images: ["/images/product2_1.jpg", "/images/product2_2.jpg"] }, ];

const filteredProducts = products.filter(product => product.name.toLowerCase().includes(searchTerm.toLowerCase()) );

const trackOrder = () => { if (!orderId) return; const statuses = ["Order Placed", "Processing", "Shipped", "Out for Delivery", "Delivered"]; let progress = []; let index = 0; setOrderStatus(statuses[index]); const interval = setInterval(() => { if (index < statuses.length - 1) { index++; progress.push(statuses[index]); setOrderStatus(statuses[index]); setTrackingProgress([...progress]); } else { clearInterval(interval); } }, 2000); };

return ( <div className="min-h-screen bg-gray-100"> <nav className="bg-white shadow-md p-4 flex justify-between items-center"> <Link href="/" className="text-xl font-bold">TrendKartHub</Link> <div className="flex items-center gap-4"> <Link href="/shop" className="text-gray-700">Shop</Link> <Link href="/about" className="text-gray-700">About Us</Link> <Link href="/contact" className="text-gray-700">Contact</Link> <div className="relative"> <FaShoppingCart size={24} /> {cartCount > 0 && ( <span className="absolute -top-2 -right-2 bg-red-500 text-white text-xs px-2 py-1 rounded-full">{cartCount}</span> )} </div> </div> </nav>

<header className="text-center py-12 px-4 bg-gradient-to-r from-blue-500 to-indigo-600 text-white">
    <h1 className="text-3xl md:text-4xl font-bold">Find the Best Deals on Trendy Products</h1>
    <p className="mt-2 text-lg">Shop now and enjoy fast delivery & secure payments</p>
    <Button className="mt-4 bg-yellow-500 hover:bg-yellow-600">Shop Now</Button>
  </header>

  <div className="p-4 flex justify-center">
    <input type="text" placeholder="Search for products..." value={searchTerm} onChange={(e) => setSearchTerm(e.target.value)} className="p-2 border border-gray-400 rounded w-full md:w-1/2" />
    <FaSearch className="ml-2 text-gray-600" size={20} />
  </div>

  <section className="p-4 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
    {filteredProducts.map((product) => (
      <div key={product.id} className="bg-white p-4 shadow rounded-lg">
        <img src={product.image} alt={product.name} className="w-full rounded" />
        <h2 className="text-lg font-bold mt-2">{product.name}</h2>
        <p className="text-gray-600">{product.price}</p>
        <p className="text-sm text-gray-500">{product.description}</p>
        <p className="text-yellow-500 font-bold">⭐ {product.reviews}/5</p>
        <Button className="mt-2 w-full bg-blue-500">Add to Cart</Button>
      </div>
    ))}
  </section>

  <section className="p-8 bg-gray-200 rounded-lg text-center">
    <h2 className="text-2xl font-bold">Track Your Order</h2>
    <p className="mt-2 text-gray-600">Enter your order ID below to check the status of your shipment</p>
    <input type="text" placeholder="Enter Order ID" value={orderId} onChange={(e) => setOrderId(e.target.value)} className="mt-4 p-2 border border-gray-400 rounded w-full md:w-1/2" />
    <Button className="mt-2 bg-blue-500" onClick={trackOrder}>Track Order</Button>
    {orderStatus && (
      <div className="mt-4">
        <h3 className="text-xl font-bold">Current Status: {orderStatus}</h3>
        <ul className="mt-2 text-gray-700">
          {trackingProgress.map((status, index) => (
            <li key={index} className="py-1">✅ {status}</li>
          ))}
        </ul>
      </div>
    )}
  </section>

  <footer className="bg-gray-800 text-white text-center p-4 mt-8">
    <p>&copy; 2025 TrendKartHub. All rights reserved.</p>
  </footer>

  <a href="https://wa.me/yourwhatsappnumber" target="_blank" className="fixed bottom-4 right-4 bg-green-500 text-white p-4 rounded-full shadow-lg hover:bg-green-600">
    <FaWhatsapp size={24} />
  </a>
</div>

); }

