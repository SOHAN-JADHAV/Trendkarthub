import React, { useState } from "react"; import { Button } from "@/components/ui/button"; import { Card, CardContent } from "@/components/ui/card"; import { ShoppingCart, Phone, CreditCard, Filter, MessageCircle, Moon, Sun, Mic, Truck } from "lucide-react"; import Link from "next/link"; import { motion } from "framer-motion";

const orders = [ { id: "12345", status: "Shipped", estimatedDelivery: "April 10, 2025" }, { id: "67890", status: "Out for Delivery", estimatedDelivery: "April 8, 2025" }, ];

export default function Home() { const [darkMode, setDarkMode] = useState(false); const [trackingVisible, setTrackingVisible] = useState(false); const [orderId, setOrderId] = useState(""); const [orderStatus, setOrderStatus] = useState(null);

const trackOrder = () => { const order = orders.find((o) => o.id === orderId); if (order) { setOrderStatus(order); } else { setOrderStatus({ status: "Order Not Found", estimatedDelivery: "N/A" }); } };

return ( <div className={darkMode ? "bg-gray-900 text-white" : "bg-gray-100 text-gray-900"}> <header className="flex justify-between items-center p-4 shadow-md"> <h1 className="text-xl font-bold">TrendKartHub</h1> <div className="flex items-center space-x-4"> <Button onClick={() => setDarkMode(!darkMode)}> {darkMode ? <Sun size={20} /> : <Moon size={20} />} </Button> <Button> <Mic size={20} /> Voice Search </Button> <Button onClick={() => setTrackingVisible(!trackingVisible)}> <Truck size={20} /> Track Order </Button> </div> </header> <main className="container mx-auto py-8"> <motion.div initial={{ opacity: 0, y: -20 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 0.5 }} className="text-center text-2xl font-bold" > AI-Powered Shopping Experience </motion.div>

{trackingVisible && (
      <motion.div
        initial={{ scale: 0.8, opacity: 0 }}
        animate={{ scale: 1, opacity: 1 }}
        transition={{ duration: 0.3 }}
        className="border p-4 rounded bg-white shadow-md max-w-md mx-auto mt-4"
      >
        <h2 className="text-lg font-bold mb-2">Track Your Order</h2>
        <input
          type="text"
          className="border p-2 w-full mb-2"
          value={orderId}
          onChange={(e) => setOrderId(e.target.value)}
          placeholder="Enter Order ID"
        />
        <Button onClick={trackOrder} className="w-full">Track</Button>
        {orderStatus && (
          <div className="mt-4">
            <p><strong>Status:</strong> {orderStatus.status}</p>
            <p><strong>Estimated Delivery:</strong> {orderStatus.estimatedDelivery}</p>
          </div>
        )}
      </motion.div>
    )}
  </main>
</div>

); }


