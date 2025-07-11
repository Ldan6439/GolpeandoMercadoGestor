# GolpeandoMercadoGestor
```jsx
import { useState, useEffect } from 'react';

export default function App() {
  const [cart, setCart] = useState([]);
  const [categories, setCategories] = useState([]);
  const [products, setProducts] = useState([]);
  const [activeCategory, setActiveCategory] = useState('all');
  const [searchQuery, setSearchQuery] = useState('');
  const [showCart, setShowCart] = useState(false);
  const [notification, setNotification] = useState(null);
  const [customerInfo, setCustomerInfo] = useState({ name: '', phone: '' });

  // Set categories from user request
  useEffect(() => {
    const newCategories = [
      'all',
      'Absorbentes',
      'Servilletas',
      'Palillos',
      'Bolsas',
      'Papel térmico',
      'Vasos desechables',
      'Envases',
      'Platos y termopack',
      'Retráctil',
      'Ceniceros',
      'Cristaleria',
      'Tajín',
      'Moldes',
      'Abridores',
      'Cubiertos',
      'Otros',
      'Venenos'
    ];
    setCategories(newCategories);
  }, []);

  // Set products from user request
  useEffect(() => {
    const productData = [
      // Absorbentes
      { id: 1, name: "Absorbentes biodegradables 100 unidades", category: "Absorbentes", price: "0.00", stock: 0, image: "https://images.pexels.com/photos/1146473/pexels-photo-1146473.jpeg?auto=format&fit=crop&w=300&q=80" },
      { id: 2, name: "Absorbente plástico flexible 100 unidades", category: "Absorbentes", price: "0.00", stock: 0, image: "https://images.pexels.com/photos/1146473/pexels-photo-1146473.jpeg?auto=format&fit=crop&w=300&q=80" },
      { id: 3, name: "Absorbente plástico moldeable 100 unidades", category: "Absorbentes", price: "500.00", stock: 10, image: "https://images.pexels.com/photos/1146473/pexels-photo-1146473.jpeg?auto=format&fit=crop&w=300&q=80" },
      { id: 4, name: "Absorbente para sueros y batidos 9mm ancho 100 unidades", category: "Absorbentes", price: "500.00", stock: 15, image: "https://images.pexels.com/photos/1146473/pexels-photo-1146473.jpeg?auto=format&fit=crop&w=300&q=80" },
      { id: 5, name: "Absorbentes clásicos finos 500 unidades 5mm", category: "Absorbentes", price: "1100.00", stock: 8, image: "https://images.pexels.com/photos/1146473/pexels-photo-1146473.jpeg?auto=format&fit=crop&w=300&q=80" },
      
      // Servilletas
      { id: 6, name: "Servilleta la excelencia 30x30cm 100 hojas doble", category: "Servilletas", price: "0.00", stock: 0, image: "https://images.pexels.com/photos/3393379/pexels-photo-3393379.jpeg?auto=format&fit=crop&w=300&q=80" },
      { id: 7, name: "Servilletas prosa 40x40cm 40 hojas doble", category: "Servilletas", price: "500.00", stock: 12, image: "https://images.pexels.com/photos/3393379/pexels-photo-3393379.jpeg?auto=format&fit=crop&w=300&q=80" },
      { id: 8, name: "Servilletas prosito 100 hojas simples 30x33cm", category: "Servilletas", price: "500.00", stock: 20, image: "https://images.pexels.com/photos/3393379/pexels-photo-3393379.jpeg?auto=format&fit=crop&w=300&q=80" },
      
      // Palillos
      { id: 9, name: "Púas para cócteles Acero inoxidable", category: "Palillos", price: "200.00", stock: 15, image: "https://images.pexels.com/photos/998591/pexels-photo-998591.jpeg?auto=format&fit=crop&w=300&q=80" },
      { id: 10, name: "Paquete de palillos 230 unidades (aprox)", category: "Palillos", price: "300.00", stock: 25, image: "https://images.pexels.com/photos/998591/pexels-photo-998591.jpeg?auto=format&fit=crop&w=300&q=80" },
      
      // Bolsas
      { id: 13, name: "Bolsas para desechos (negras) Rollo de 25 unidades", category: "Bolsas", price: "900.00", stock: 10, image: "https://images.pexels.com/photos/398793/pexels-photo-398793.jpeg?auto=format&fit=crop&w=300&q=80" },
      
      // Papel térmico
      { id: 16, name: "Rollo de papel térmico 57mm x 22m", category: "Papel térmico", price: "250.00", stock: 30, image: "https://images.pexels.com/photos/398793/pexels-photo-398793.jpeg?auto=format&fit=crop&w=300&q=80" },
      
      // Vasos desechables
      { id: 18, name: "Vasos desechables para café 3onz 100 unidades", category: "Vasos desechables", price: "500.00", stock: 20, image: "https://images.pexels.com/photos/1376404/pexels-photo-1376404.jpeg?auto=format&fit=crop&w=300&q=80" },
      
      // Ceniceros
      { id: 26, name: "Cenicero de cristal clásico 10.5cm", category: "Ceniceros", price: "800.00", stock: 15, image: "https://images.pexels.com/photos/774911/pexels-photo-774911.jpeg?auto=format&fit=crop&w=300&q=80" },
      
      // Cristaleria
      { id: 28, name: "Jarra de cristal para batido Viene con su absorbente 500ml~16onz", category: "Cristaleria", price: "1000.00", stock: 8, image: "https://images.pexels.com/photos/774911/pexels-photo-774911.jpeg?auto=format&fit=crop&w=300&q=80" },
      
      // Venenos
      { id: 40, name: "Veneno para moscas 100 uni", category: "Venenos", price: "150.00", stock: 30, image: "https://images.pexels.com/photos/590017/pexels-photo-590017.jpeg?auto=format&fit=crop&w=300&q=80" }
    ];
    
    setProducts(productData);
  }, []);

  const filteredProducts = products.filter(
    (product) =>
      (activeCategory === 'all' || product.category === activeCategory) &&
      product.name.toLowerCase().includes(searchQuery.toLowerCase())
  );

  const addToCart = (product) => {
    const existingItem = cart.find((item) => item.id === product.id);
    if (existingItem) {
      setCart(
        cart.map((item) =>
          item.id === product.id ? { ...item, quantity: item.quantity + 1 } : item
        )
      );
    } else {
      setCart([...cart, { ...product, quantity: 1 }]);
    }
    showNotification(`Añadido al carrito: ${product.name}`);
  };

  const updateQuantity = (id, quantity) => {
    if (quantity <= 0) {
      setCart(cart.filter((item) => item.id !== id));
    } else {
      setCart(
        cart.map((item) => (item.id === id ? { ...item, quantity } : item))
      );
    }
  };

  const getTotalItems = () => {
    return cart.reduce((total, item) => total + item.quantity, 0);
  };

  const getTotalPrice = () => {
    return cart
      .reduce((total, item) => total + parseFloat(item.price) * item.quantity, 0)
      .toFixed(2);
  };

  const sendToWhatsApp = () => {
    if (cart.length === 0) {
      showNotification('El carrito está vacío');
      return;
    }
    
    if (!customerInfo.phone || !customerInfo.name) {
      showNotification('Por favor complete nombre y teléfono');
      return;
    }

    let message = encodeURIComponent(`PEDIDO GESTOR I94\nCliente: ${customerInfo.name}\nTeléfono: ${customerInfo.phone}\n\nProductos:\n`);
    cart.forEach((item) => {
      message += encodeURIComponent(`${item.name} - Cantidad: ${item.quantity}\n`);
    });
    message += encodeURIComponent(`\nTotal: ₱${getTotalPrice()}`);
    
    window.open(`https://wa.me/5352663106?text=${message}`, '_blank');
    setCart([]);
    setShowCart(false);
    setCustomerInfo({ name: '', phone: '' });
    showNotification('Pedido enviado por WhatsApp');
  };

  const showNotification = (text) => {
    setNotification(text);
    setTimeout(() => setNotification(null), 3000);
  };

  return (
    <div className="min-h-screen bg-gray-50">
      {/* Notification */}
      {notification && (
        <div className="fixed top-4 right-4 bg-green-500 text-white px-4 py-2 rounded shadow-lg z-50">
          {notification}
        </div>
      )}
      
      {/* Hero Section */}
      <div className="relative bg-indigo-900 text-white">
        <div className="absolute inset-0 overflow-hidden">
          <img 
            src="https://images.pexels.com/photos/338501/pexels-photo-338501.jpeg?auto=format&fit=crop&w=1920&q=80" 
            alt="Mercado de desechables" 
            className="w-full h-64 object-cover opacity-30"
          />
        </div>
        <div className="container mx-auto px-4 py-16 relative">
          <h1 className="text-4xl md:text-5xl font-bold mb-4">Golpeando el mercado Gestor I94</h1>
          <p className="text-xl md:text-2xl max-w-3xl">Tu proveedor confiable para productos de mercado y desechables</p>
        </div>
      </div>

      {/* Header */}
      <header className="bg-white shadow-sm sticky top-0 z-40">
        <div className="container mx-auto px-4 py-4 flex justify-between items-center">
          <h1 className="text-2xl font-bold text-indigo-600">Golpeando el mercado Gestor I94</h1>
          <div className="relative">
            <input
              type="text"
              placeholder="Buscar productos..."
              value={searchQuery}
              onChange={(e) => setSearchQuery(e.target.value)}
              className="pl-10 pr-4 py-2 border rounded-full focus:outline-none focus:ring-2 focus:ring-indigo-500"
            />
            <svg
              className="w-5 h-5 absolute left-3 top-2.5 text-gray-500"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                strokeLinecap="round"
                strokeLinejoin="round"
                strokeWidth="2"
                d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
              />
            </svg>
          </div>
          <button
            onClick={() => setShowCart(true)}
            className="relative p-2 rounded-full hover:bg-gray-100 transition-colors"
          >
            <svg
              className="w-6 h-6 text-gray-700"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                strokeLinecap="round"
                strokeLinejoin="round"
                strokeWidth="2"
                d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"
              />
            </svg>
            {getTotalItems() > 0 && (
              <span className="absolute -top-1 -right-1 bg-red-500 text-white text-xs w-5 h-5 flex items-center justify-center rounded-full">
                {getTotalItems()}
              </span>
            )}
          </button>
        </div>
        
        {/* Categories */}
        <div className="bg-gray-100 overflow-x-auto whitespace-nowrap pb-2">
          <div className="container mx-auto px-4">
            {categories.map((category) => (
              <button
                key={category}
                onClick={() => setActiveCategory(category)}
                className={`px-4 py-2 capitalize whitespace-nowrap ${
                  activeCategory === category
                    ? 'bg-indigo-600 text-white rounded-full'
                    : 'hover:bg-gray-200'
                }`}
              >
                {category}
              </button>
            ))}
          </div>
        </div>
      </header>
      
      {/* Main content */}
      <main className="container mx-auto px-4 py-8">
        <h2 className="text-3xl font-bold mb-6">
          {activeCategory === 'all' ? 'Todos los productos' : activeCategory}
        </h2>
        
        {/* Products grid */}
        <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
          {filteredProducts.length > 0 ? (
            filteredProducts.map((product) => (
              <div
                key={product.id}
                className="bg-white rounded-lg overflow-hidden shadow-md hover:shadow-xl transition-shadow duration-300 flex flex-col"
              >
                <img
                  src={product.image}
                  alt={product.name}
                  className="w-full h-48 object-cover"
                />
                <div className="p-4 flex-grow flex flex-col justify-between">
                  <div>
                    <h3 className="font-semibold text-lg mb-1">{product.name}</h3>
                    <p className="text-gray-600 mb-2">₱{product.price}</p>
                    <p className="text-sm text-gray-500 mb-4">
                      {product.stock > 0 ? `Stock: ${product.stock}` : 'Agotado'}
                    </p>
                  </div>
                  <button
                    onClick={() => addToCart(product)}
                    disabled={product.stock <= 0}
                    className={`mt-4 py-2 px-4 rounded-full font-medium transition-colors ${
                      product.stock > 0
                        ? 'bg-indigo-600 hover:bg-indigo-700 text-white'
                        : 'bg-gray-300 text-gray-500 cursor-not-allowed'
                    }`}
                  >
                    {product.stock > 0 ? 'Agregar al carrito' : 'Sin stock'}
                  </button>
                </div>
              </div>
            ))
          ) : (
            <div className="col-span-full text-center py-12">
              <p className="text-gray-500 text-xl">No se encontraron productos.</p>
            </div>
          )}
        </div>
      </main>
      
      {/* Footer */}
      <footer className="bg-white mt-12 py-8 border-t">
        <div className="container mx-auto px-4 text-center text-gray-600">
          <p>© 2025 Golpeando el mercado Gestor I94. Todos los derechos reservados.</p>
        </div>
      </footer>
      
      {/* Cart sidebar */}
      {showCart && (
        <div className="fixed inset-0 z-50 flex">
          <div
            className="fixed inset-0 bg-black bg-opacity-50"
            onClick={() => setShowCart(false)}
          ></div>
          <div className="relative bg-white w-full max-w-md ml-auto h-full shadow-xl flex flex-col">
            <div className="p-6 border-b flex justify-between items-center">
              <h2 className="text-xl font-bold">Tu Carrito</h2>
              <button
                onClick={() => setShowCart(false)}
                className="text-gray-500 hover:text-gray-700"
              >
                <svg
                  className="w-6 h-6"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    strokeLinecap="round"
                    strokeLinejoin="round"
                    strokeWidth="2"
                    d="M6 18L18 6M6 6l12 12"
                  />
                </svg>
              </button>
            </div>
            <div className="flex-grow overflow-y-auto p-6">
              {cart.length === 0 ? (
                <p className="text-gray-500 text-center py-8">
                  Tu carrito está vacío
                </p>
              ) : (
                <>
                  <ul className="space-y-4">
                    {cart.map((item) => (
                      <li
                        key={item.id}
                        className="flex items-center border rounded-lg p-3"
                      >
                        <img
                          src={item.image}
                          alt={item.name}
                          className="w-16 h-16 object-cover rounded mr-4"
                        />
                        <div className="flex-grow">
                          <h4 className="font-medium">{item.name}</h4>
                          <p className="text-gray-600">₱{item.price}</p>
                        </div>
                        <div className="flex items-center ml-2">
                          <button
                            onClick={() =>
                              updateQuantity(item.id, item.quantity - 1)
                            }
                            className="w-8 h-8 flex items-center justify-center rounded-full bg-gray-200 text-gray-700"
                          >
                            -
                          </button>
                          <span className="mx-2 w-8 text-center">{item.quantity}</span>
                          <button
                            onClick={() =>
                              updateQuantity(item.id, item.quantity + 1)
                            }
                            className="w-8 h-8 flex items-center justify-center rounded-full bg-gray-200 text-gray-700"
                          >
                            +
                          </button>
                        </div>
                      </li>
                    ))}
                  </ul>
                  
                  {/* Customer Info Form */}
                  <div className="mt-6">
                    <h3 className="font-semibold mb-2">Datos del Cliente</h3>
                    <div className="space-y-3">
                      <input
                        type="text"
                        placeholder="Nombre completo"
                        value={customerInfo.name}
                        onChange={(e) => setCustomerInfo({...customerInfo, name: e.target.value})}
                        className="w-full px-3 py-2 border rounded"
                      />
                      <input
                        type="text"
                        placeholder="Teléfono (ej: 5352663106)"
                        value={customerInfo.phone}
                        onChange={(e) => setCustomerInfo({...customerInfo, phone: e.target.value})}
                        className="w-full px-3 py-2 border rounded"
                      />
                    </div>
                  </div>
                </>
              )}
            </div>
            {cart.length > 0 && (
              <div className="border-t p-6">
                <div className="flex justify-between mb-4">
                  <span className="font-bold">Total:</span>
                  <span className="font-bold">₱{getTotalPrice()}</span>
                </div>
                <button
                  onClick={sendToWhatsApp}
                  className="w-full bg-green-600 hover:bg-green-700 text-white py-3 rounded-full font-bold transition-colors flex items-center justify-center"
                >
                  <svg
                    className="w-5 h-5 mr-2"
                    fill="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.072.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347z" />
                  </svg>
                  Enviar pedido por WhatsApp
                </button>
              </div>
            )}
          </div>
        </div>
      )}
    </div>
  );
}
```
