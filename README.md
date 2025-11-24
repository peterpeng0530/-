  return (
    <div className="min-h-screen bg-gray-50 flex flex-col max-w-2xl mx-auto shadow-2xl overflow-hidden">
      {/* Header */}
      <header className="bg-brand-500 text-white p-4 sticky top-0 z-30 shadow-md">
        <div className="flex justify-between items-center">
          <div>
            <h1 className="text-xl font-bold flex items-center gap-2">
              <span className="text-2xl">☀️</span> 早安点餐
            </h1>
            <p className="text-brand-100 text-xs mt-1">美好的一天从早餐开始</p>
          </div>
          <div className="bg-white/20 p-2 rounded-lg backdrop-blur-sm">
             <span className="text-xs font-medium">营业中 06:00-11:00</span>
          </div>
        </div>
      </header>

      {/* Category Tabs */}
      <nav className="sticky top-[76px] z-20 bg-white shadow-sm overflow-x-auto no-scrollbar">
        <div className="flex px-4 py-3 gap-4 min-w-max">
          {CATEGORIES.map((cat) => (
            <button
              key={cat}
              onClick={() => setActiveCategory(cat)}
              className={`px-4 py-2 rounded-full text-sm font-bold transition-all whitespace-nowrap ${
                activeCategory === cat
                  ? 'bg-brand-500 text-white shadow-md scale-105'
                  : 'bg-gray-100 text-gray-500 hover:bg-gray-200'
              }`}
            >
              {cat}
            </button>
          ))}
        </div>
      </nav>

      {/* Menu Grid */}
      <main className="flex-grow p-4 pb-28">
        <div className="grid grid-cols-1 sm:grid-cols-2 gap-6">
          {filteredItems.map((item) => (
            <MenuItemCard
              key={item.id}
              item={item}
              quantityInCart={cart.find((c) => c.id === item.id)?.quantity || 0}
              onAdd={addToCart}
              onRemove={removeFromCart}
            />
          ))}
        </div>
        
        {/* Empty State Suggestion */}
        {filteredItems.length === 0 && (
           <div className="text-center py-20 text-gray-400">
             <p>该分类下暂无商品</p>
           </div>
        )}
      </main>

      {/* Sticky Cart Summary Bar */}
      <div className="fixed bottom-0 left-0 right-0 z-40 p-4 max-w-2xl mx-auto">
        <div 
          onClick={() => setIsCartOpen(true)}
          className="bg-gray-900 text-white rounded-2xl shadow-xl p-3 flex justify-between items-center cursor-pointer hover:bg-gray-800 transition-colors"
        >
          <div className="flex items-center gap-4 pl-2">
            <div className="relative">
              <div className={`w-12 h-12 rounded-full flex items-center justify-center ${totalItems > 0 ? 'bg-brand-500 text-white' : 'bg-gray-700 text-gray-400'}`}>
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"/></svg>
              </div>
              {totalItems > 0 && (
                <div className="absolute -top-2 -right-2 bg-red-500 text-white text-xs font-bold w-6 h-6 flex items-center justify-center rounded-full border-2 border-gray-900 animate-bounce">
                  {totalItems}
                </div>
              )}
            </div>
            <div className="flex flex-col">
              <span className="text-xl font-bold">¥{totalPrice.toFixed(1)}</span>
              <span className="text-xs text-gray-400">免配送费</span>
            </div>
          </div>
          <button 
            className="bg-brand-500 text-white px-6 py-2.5 rounded-xl font-bold text-sm hover:bg-brand-400 transition-colors"
          >
            去结算
          </button>
        </div>
      </div>

      {/* Cart Modal/Drawer */}
      <CartDrawer 
        cart={cart}
        isOpen={isCartOpen}
        onClose={() => setIsCartOpen(false)}
        onAdd={addToCart}
        onRemove={removeFromCart}
        totalPrice={totalPrice}
      />
    </div>
  );
};

export default App;
