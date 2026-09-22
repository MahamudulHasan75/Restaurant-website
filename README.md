# Restaurant-website
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Green Forest Restaurant</title>
  <link rel="stylesheet" href="style.css"/>
</head>
<body>

  <!-- ===== FOOD MODAL ===== -->
  <div id="food-modal" class="modal-backdrop" onclick="closeModalOutside(event)">
    <div class="modal-box">
      <button class="modal-close" onclick="closeModal()">&#x2715;</button>
      <div class="modal-header">
        <span class="modal-tag" id="modal-cat-label"></span>
        <h2 id="modal-title"></h2>
        <p id="modal-subtitle"></p>
      </div>
      <div class="modal-grid" id="modal-grid"></div>
    </div>
  </div>

  <!-- ===== CART SIDEBAR ===== -->
  <div id="cart-sidebar" class="cart-sidebar">
    <div class="cart-header">
      <h3>🛒 Your Order</h3>
      <button onclick="toggleCart()">✕</button>
    </div>
    <div id="cart-items"></div>
    <div class="cart-footer">
      <div class="cart-total">Total: <span id="cart-total-price">৳0</span></div>
      <input type="text" id="cart-table" placeholder="Table number (e.g. T1)" />
      <select id="cart-payment">
        <option value="Cash">Cash</option>
        <option value="bKash">bKash</option>
        <option value="Card">Card</option>
      </select>
      <button class="btn-checkout" onclick="checkoutCart()">✅ Place Order</button>
      <p id="cart-msg" style="display:none;color:#4caf50;margin-top:8px;text-align:center;">✔ Order placed successfully!</p>
    </div>
  </div>
  <div id="cart-overlay" onclick="toggleCart()"></div>

  <!-- ===== EDITOR PANEL ===== -->
  <div id="editor-panel">
    <button id="editor-toggle" onclick="toggleEditor()">&#9998; Edit</button>
    <div id="editor-content">
      <h3>Site Editor</h3>
      <label>Hero Background Color</label>
      <input type="color" id="hero-bg-color" value="#1a0a00" oninput="applyHeroBg(this.value)"/>
      <label>Navbar Color</label>
      <input type="color" id="nav-bg-color" value="#0f0600" oninput="applyNavBg(this.value)"/>
      <label>Accent Color</label>
      <input type="color" id="accent-color" value="#e07b39" oninput="applyAccent(this.value)"/>
      <label>Page Background</label>
      <input type="color" id="page-bg-color" value="#111111" oninput="applyPageBg(this.value)"/>
      <hr/>
      <p style="font-size:12px;color:#aaa;margin-bottom:6px;">Click any price below to edit:</p>
      <div id="price-list"></div>
    </div>
  </div>

  <!-- NAVBAR -->
  <nav id="navbar">
    <div class="nav-logo">🍽 Green Forest Restaurant</div>
    <button class="nav-toggle" onclick="toggleNav()">&#9776;</button>
    <ul id="nav-links">
      <li><a href="#home">Home</a></li>
      <li><a href="#about">About</a></li>
      <li><a href="#menu">Menu</a></li>
      <li><a href="#gallery">Gallery</a></li>
      <li><a href="#reviews">Reviews</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
    <button class="cart-btn" onclick="toggleCart()">
      🛒 Cart <span id="cart-count" class="cart-badge">0</span>
    </button>
  </nav>

  <!-- HERO -->
  <section id="home" class="hero">
    <div class="hero-overlay"></div>
    <div class="hero-content">
      <p class="hero-sub">Welcome</p>
      <h1>Green Forest Restaurant</h1>
      <p class="hero-tagline">A Taste of Nature, Every Plate</p>
      <p class="hero-desc">Our cooking is made with love, fresh ingredients, and the flavours of tradition.</p>
      <a href="#menu" class="btn-primary">View Menu</a>
    </div>
  </section>

  <!-- ABOUT -->
  <section id="about" class="section">
    <div class="container about-grid">
      <div class="about-img">
        <img src="image/Lunch Platter.jpg" alt="Restaurant food"/>
      </div>
      <div class="about-text">
        <span class="tag">Our Story</span>
        <h2>A Touch of Love in Every Dish</h2>
        <p>Since 2018, Green Forest Restaurant has been serving delicious food prepared with handcrafted traditional recipes. We believe food is the language of love.</p>
        <p>Our chefs gather fresh, local ingredients every morning to ensure the most authentic flavours in every meal.</p>
        <a href="#contact" class="btn-primary">Book a Table</a>
      </div>
    </div>
  </section>

  <!-- MENU -->
  <section id="menu" class="section section-dark">
    <div class="container">
      <div class="section-header">
        <span class="tag">Our Menu</span>
        <h2>Featured Dishes</h2>
        <p class="menu-hint">&#128247; Click on any image to see all items in that category</p>
      </div>
      <div class="menu-tabs">
        <button class="tab-btn active" onclick="filterMenu('all', this)">All</button>
        <button class="tab-btn" onclick="filterMenu('breakfast', this)">Breakfast</button>
        <button class="tab-btn" onclick="filterMenu('mains', this)">Main Course</button>
        <button class="tab-btn" onclick="filterMenu('drinks', this)">Drinks</button>
        <button class="tab-btn" onclick="filterMenu('snacks', this)">Snacks</button>
      </div>
      <div class="menu-grid" id="menu-grid">

        <!-- BREAKFAST -->
        <div class="menu-card" data-cat="breakfast">
          <div class="menu-img-wrap clickable-img" onclick="openModal('breakfast','Break-fast Dosa')">
            <img src="image/Break-fast Dosa.jpg" alt="Break-fast Dosa"/>
            <div class="img-overlay"><span>&#128065; View Breakfast</span></div>
          </div>
          <div class="menu-info">
            <h3>Break-fast Dosa</h3>
            <p>Crispy South Indian dosa served with sambar and fresh coconut chutney.</p>
            <div class="price-order">
              <span class="price editable-price" data-id="p1">৳120</span>
              <div class="qty-controls">
                <button onclick="changeQty(this,-1)">−</button>
                <span class="qty">1</span>
                <button onclick="changeQty(this,1)">+</button>
              </div>
              <button class="order-btn" onclick="addToCart(event, 'Break-fast Dosa')">🛒 Add</button>
            </div>
          </div>
        </div>

        <div class="menu-card" data-cat="breakfast">
          <div class="menu-img-wrap clickable-img" onclick="openModal('breakfast','Break-fast Platter')">
            <img src="image/Break-fast Platter.jpg" alt="Break-fast Platter"/>
            <div class="img-overlay"><span>&#128065; View Breakfast</span></div>
          </div>
          <div class="menu-info">
            <h3>Break-fast Platter</h3>
            <p>A wholesome morning platter with eggs, toast, fruits, and a hot beverage.</p>
            <div class="price-order">
              <span class="price editable-price" data-id="p2">৳180</span>
              <div class="qty-controls">
                <button onclick="changeQty(this,-1)">−</button>
                <span class="qty">1</span>
                <button onclick="changeQty(this,1)">+</button>
              </div>
              <button class="order-btn" onclick="addToCart(event, 'Break-fast Platter')">🛒 Add</button>
            </div>
          </div>
        </div>

        <div class="menu-card" data-cat="breakfast">
          <div class="menu-img-wrap clickable-img" onclick="openModal('breakfast','Idli Sambar')">
            <img src="image/Idli-Sumber.jpg" alt="Idli Sambar"/>
            <div class="img-overlay"><span>&#128065; View Breakfast</span></div>
          </div>
          <div class="menu-info">
            <h3>Idli Sambar</h3>
            <p>Soft steamed rice cakes served with tangy sambar and chutneys.</p>
            <div class="price-order">
              <span class="price editable-price" data-id="p3">৳100</span>
              <div class="qty-controls">
                <button onclick="changeQty(this,-1)">−</button>
                <span class="qty">1</span>
                <button onclick="changeQty(this,1)">+</button>
              </div>
              <button class="order-btn" onclick="addToCart(event, 'Idli Sambar')">🛒 Add</button>
            </div>
          </div>
        </div>

        <!-- MAINS -->
        <div class="menu-card" data-cat="mains">
          <div class="menu-img-wrap clickable-img" onclick="openModal('mains','Chilli Chicken Wings')">
            <img src="image/Chilli Chicken Wings.jpg" alt="Chilli Chicken Wings"/>
            <div class="img-overlay"><span>&#128065; View Main Course</span></div>
          </div>
          <div class="menu-info">
            <h3>Chilli Chicken Wings</h3>
            <p>Spicy and crispy chicken wings tossed in our signature chilli sauce.</p>
            <div class="price-order">
              <span class="price editable-price" data-id="p4">৳280</span>
              <div class="qty-controls">
                <button onclick="changeQty(this,-1)">−</button>
                <span class="qty">1</span>
                <button onclick="changeQty(this,1)">+</button>
              </div>
              <button class="order-btn" onclick="addToCart(event, 'Chilli Chicken Wings')">🛒 Add</button>
            </div>
          </div>
        </div>

        <div class="menu-card" data-cat="mains">
          <div class="menu-img-wrap clickable-img" onclick="openModal('mains','Crispy Chicken')">
            <img src="image/Crispy chicken.jpg" alt="Crispy Chicken"/>
            <div class="img-overlay"><span>&#128065; View Main Course</span></div>
          </div>
          <div class="menu-info">
            <h3>Crispy Chicken</h3>
            <p>Golden fried crispy chicken with special seasoning, served with dipping sauce.</p>
            <div class="price-order">
              <span class="price editable-price" data-id="p5">৳320</span>
              <div class="qty-controls">
                <button onclick="changeQty(this,-1)">−</button>
                <span class="qty">1</span>
                <button onclick="changeQty(this,1)">+</button>
              </div>
              <button class="order-btn" onclick="addToCart(event, 'Crispy Chicken')">🛒 Add</button>
            </div>
          </div>
        </div>

        <div class="menu-card" data-cat="mains">
          <div class="menu-img-wrap clickable-img" onclick="openModal('mains','Creamy Soup')">
            <img src="image/Creamy Soup.jpg" alt="Creamy Soup"/>
            <div class="img-overlay"><span>&#128065; View Main Course</span></div>
          </div>
          <div class="menu-info">
            <h3>Creamy Soup</h3>
            <p>Rich and velvety cream soup made with fresh vegetables and herbs.</p>
            <div class="price-order">
              <span class="price editable-price" data-id="p6">৳150</span>
              <div class="qty-controls">
                <button onclick="changeQty(this,-1)">−</button>
                <span class="qty">1</span>
                <button onclick="changeQty(this,1)">+</button>
              </div>
              <button class="order-btn" onclick="addToCart(event, 'Creamy Soup')">🛒 Add</button>
            </div>
          </div>
        </div>

        <div class="menu-card" data-cat="mains">
          <div class="menu-img-wrap clickable-img" onclick="openModal('mains','Dinner Platter')">
            <img src="image/Dinner Platter.jpg" alt="Dinner Platter"/>
            <div class="img-overlay"><span>&#128065; View Main Course</span></div>
          </div>
          <div class="menu-info">
            <h3>Dinner Platter</h3>
            <p>A generous platter with grilled meats, rice, salad, and sides.</p>
            <div class="price-order">
              <span class="price editable-price" data-id="p7">৳450</span>
              <div class="qty-controls">
                <button onclick="changeQty(this,-1)">−</button>
                <span class="qty">1</span>
                <button onclick="changeQty(this,1)">+</button>
              </div>
              <button class="order-btn" onclick="addToCart(event, 'Dinner Platter')">🛒 Add</button>
            </div>
          </div>
        </div>

        <div class="menu-card" data-cat="mains">
          <div class="menu-img-wrap clickable-img" onclick="openModal('mains','Lunch Platter')">
            <img src="image/Lunch Platter.jpg" alt="Lunch Platter"/>
            <div class="img-overlay"><span>&#128065; View Main Course</span></div>
          </div>
          <div class="menu-info">
            <h3>Lunch Platter</h3>
            <p>Complete midday meal with rice, curry, vegetables, and dessert.</p>
            <div class="price-order">
              <span class="price editable-price" data-id="p8">৳380</span>
              <div class="qty-controls">
                <button onclick="changeQty(this,-1)">−</button>
                <span class="qty">1</span>
                <button onclick="changeQty(this,1)">+</button>
              </div>
              <button class="order-btn" onclick="addToCart(event, 'Lunch Platter')">🛒 Add</button>
            </div>
          </div>
        </div>

        <!-- SNACKS -->
        <div class="menu-card" data-cat="snacks">
          <div class="menu-img-wrap clickable-img" onclick="openModal('snacks','Fries')">
            <img src="image/Fries.jpg" alt="Fries"/>
            <div class="img-overlay"><span>&#128065; View Snacks</span></div>
          </div>
          <div class="menu-info">
            <h3>Crispy Fries</h3>
            <p>Golden crispy fries seasoned with special spices, served with ketchup.</p>
            <div class="price-order">
              <span class="price editable-price" data-id="p9">৳90</span>
              <div class="qty-controls">
                <button onclick="changeQty(this,-1)">−</button>
                <span class="qty">1</span>
                <button onclick="changeQty(this,1)">+</button>
              </div>
              <button class="order-btn" onclick="addToCart(event, 'Crispy Fries')">🛒 Add</button>
            </div>
          </div>
        </div>

        <div class="menu-card" data-cat="snacks">
          <div class="menu-img-wrap clickable-img" onclick="openModal('snacks','Fuchka')">
            <img src="image/Fuchka.jpg" alt="Fuchka"/>
            <div class="img-overlay"><span>&#128065; View Snacks</span></div>
          </div>
          <div class="menu-info">
            <h3>Fuchka</h3>
            <p>Classic Bangladeshi street food – crispy shells with tangy tamarind water.</p>
            <div class="price-order">
              <span class="price editable-price" data-id="p10">৳60</span>
              <div class="qty-controls">
                <button onclick="changeQty(this,-1)">−</button>
                <span class="qty">1</span>
                <button onclick="changeQty(this,1)">+</button>
              </div>
              <button class="order-btn" onclick="addToCart(event, 'Fuchka')">🛒 Add</button>
            </div>
          </div>
        </div>

        <!-- DRINKS -->
        <div class="menu-card" data-cat="drinks">
          <div class="menu-img-wrap clickable-img" onclick="openModal('drinks','Green Mocktail')">
            <img src="image/Green Mocktail.jpg" alt="Green Mocktail"/>
            <div class="img-overlay"><span>&#128065; View Drinks</span></div>
          </div>
          <div class="menu-info">
            <h3>Green Mocktail</h3>
            <p>Refreshing blend of mint, lime, and cucumber for a cool tropical vibe.</p>
            <div class="price-order">
              <span class="price editable-price" data-id="p11">৳110</span>
              <div class="qty-controls">
                <button onclick="changeQty(this,-1)">−</button>
                <span class="qty">1</span>
                <button onclick="changeQty(this,1)">+</button>
              </div>
              <button class="order-btn" onclick="addToCart(event, 'Green Mocktail')">🛒 Add</button>
            </div>
          </div>
        </div>

        <div class="menu-card" data-cat="drinks">
          <div class="menu-img-wrap clickable-img" onclick="openModal('drinks','Lemon Drinks')">
            <img src="image/Lemon Drinks.jpg" alt="Lemon Drinks"/>
            <div class="img-overlay"><span>&#128065; View Drinks</span></div>
          </div>
          <div class="menu-info">
            <h3>Lemon Drinks</h3>
            <p>Chilled fresh lemon squeeze with sugar and a hint of salt.</p>
            <div class="price-order">
              <span class="price editable-price" data-id="p12">৳80</span>
              <div class="qty-controls">
                <button onclick="changeQty(this,-1)">−</button>
                <span class="qty">1</span>
                <button onclick="changeQty(this,1)">+</button>
              </div>
              <button class="order-btn" onclick="addToCart(event, 'Lemon Drinks')">🛒 Add</button>
            </div>
          </div>
        </div>

        <div class="menu-card" data-cat="drinks">
          <div class="menu-img-wrap clickable-img" onclick="openModal('drinks','Pink Smoothie')">
            <img src="image/Pink Smoothe.jpg" alt="Pink Smoothie"/>
            <div class="img-overlay"><span>&#128065; View Drinks</span></div>
          </div>
          <div class="menu-info">
            <h3>Pink Smoothie</h3>
            <p>Creamy berry and banana smoothie with a beautiful pink colour.</p>
            <div class="price-order">
              <span class="price editable-price" data-id="p13">৳130</span>
              <div class="qty-controls">
                <button onclick="changeQty(this,-1)">−</button>
                <span class="qty">1</span>
                <button onclick="changeQty(this,1)">+</button>
              </div>
              <button class="order-btn" onclick="addToCart(event, 'Pink Smoothie')">🛒 Add</button>
            </div>
          </div>
        </div>

        <div class="menu-card" data-cat="drinks">
          <div class="menu-img-wrap clickable-img" onclick="openModal('drinks','Red Drinks')">
            <img src="image/Red Drinks.jpg" alt="Red Drinks"/>
            <div class="img-overlay"><span>&#128065; View Drinks</span></div>
          </div>
          <div class="menu-info">
            <h3>Red Drinks</h3>
            <p>Vibrant red fruit punch with mixed tropical berries and ice.</p>
            <div class="price-order">
              <span class="price editable-price" data-id="p14">৳100</span>
              <div class="qty-controls">
                <button onclick="changeQty(this,-1)">−</button>
                <span class="qty">1</span>
                <button onclick="changeQty(this,1)">+</button>
              </div>
              <button class="order-btn" onclick="addToCart(event, 'Red Drinks')">🛒 Add</button>
            </div>
          </div>
        </div>

        <div class="menu-card" data-cat="drinks">
          <div class="menu-img-wrap clickable-img" onclick="openModal('drinks','Strawberry Milkshake')">
            <img src="image/Stawberry milkshake.jpg" alt="Strawberry Milkshake"/>
            <div class="img-overlay"><span>&#128065; View Drinks</span></div>
          </div>
          <div class="menu-info">
            <h3>Strawberry Milkshake</h3>
            <p>Thick creamy milkshake blended with fresh strawberries and vanilla ice cream.</p>
            <div class="price-order">
              <span class="price editable-price" data-id="p15">৳150</span>
              <div class="qty-controls">
                <button onclick="changeQty(this,-1)">−</button>
                <span class="qty">1</span>
                <button onclick="changeQty(this,1)">+</button>
              </div>
              <button class="order-btn" onclick="addToCart(event, 'Strawberry Milkshake')">🛒 Add</button>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>

  <!-- GALLERY -->
  <section id="gallery" class="section">
    <div class="container">
      <div class="section-header">
        <span class="tag">Gallery</span>
        <h2>A Feast for the Eyes</h2>
      </div>
      <div class="gallery-grid">
        <img src="image/Dinner Platter.jpg" alt="Dinner Platter"/>
        <img src="image/Chilli Chicken Wings.jpg" alt="Chilli Chicken Wings"/>
        <img src="image/Fuchka.jpg" alt="Fuchka"/>
        <img src="image/Green Mocktail.jpg" alt="Green Mocktail"/>
        <img src="image/Crispy chicken.jpg" alt="Crispy Chicken"/>
        <img src="image/Stawberry milkshake.jpg" alt="Strawberry Milkshake"/>
      </div>
    </div>
  </section>

  <!-- ===== REVIEWS SECTION ===== -->
  <section id="reviews" class="section section-dark">
    <div class="container">
      <div class="section-header">
        <span class="tag">Customer Feedback</span>
        <h2>Reviews &amp; Ratings</h2>
      </div>

      <!-- Existing Reviews Display -->
      <div class="reviews-grid" id="reviews-grid">
        <!-- Static sample reviews -->
        <div class="review-card">
          <div class="review-stars">★★★★★</div>
          <p class="review-text">"The Fuchka and Crispy Chicken are amazing! I want to come back every time."</p>
          <div class="review-author">— Rahela Begum, Dhaka</div>
        </div>
        <div class="review-card">
          <div class="review-stars">★★★★★</div>
          <p class="review-text">"Best restaurant in Sonargaon! The Dinner Platter is absolutely amazing."</p>
          <div class="review-author">— Md. Karim</div>
        </div>
        <div class="review-card">
          <div class="review-stars">★★★★☆</div>
          <p class="review-text">"The Strawberry Milkshake is wonderful. The ambience is also very beautiful."</p>
          <div class="review-author">— Sumaiya Akter</div>
        </div>
      </div>

      <!-- Dynamic reviews from PHP -->
      <div id="dynamic-reviews"></div>

      <!-- Review Form -->
      <div class="review-form-wrap">
        <h3>Leave Your Review</h3>
        <form class="review-form" onsubmit="submitReview(event)">
          <input type="text" name="reviewer_name" placeholder="Your Name" required/>
          <div class="star-rating-input">
            <label>Rating:</label>
            <div class="stars-select">
              <span class="star-opt" data-val="5" onclick="setRating(5)">★</span>
              <span class="star-opt" data-val="4" onclick="setRating(4)">★</span>
              <span class="star-opt" data-val="3" onclick="setRating(3)">★</span>
              <span class="star-opt" data-val="2" onclick="setRating(2)">★</span>
              <span class="star-opt" data-val="1" onclick="setRating(1)">★</span>
            </div>
            <input type="hidden" name="rating" id="rating-val" value="5"/>
          </div>
          <textarea name="review_text" placeholder="Write about your experience..." rows="3" required></textarea>
          <button type="submit" class="btn-primary">Submit Review ✉</button>
          <p id="review-msg" style="display:none;color:#4caf50;margin-top:8px;">✔ Review submitted successfully!</p>
        </form>
      </div>
    </div>
  </section>

  <!-- CONTACT -->
  <section id="contact" class="section">
    <div class="container contact-grid">
      <div>
        <span class="tag">Get in Touch</span>
        <h2>Table Reservation</h2>
        <p>📍 123 Sonargaon Road, Dhaka, Bangladesh</p>
        <p>📞 +880 1700-000000</p>
        <p>✉️ hello@greenforestrestaurant.com</p>
        <p>🕐 Mon–Sun: 8:00 AM – 10:00 PM</p>
      </div>
      <form class="contact-form" onsubmit="submitReservation(event)">
        <input type="text" name="name" placeholder="Your Name" required/>
        <input type="email" name="email" placeholder="Email Address" required/>
        <input type="date" name="date" required/>
        <select name="guests">
          <option value="">Number of Guests</option>
          <option>1–2</option>
          <option>3–4</option>
          <option>5–6</option>
          <option>7+</option>
        </select>
        <textarea name="message" placeholder="Special requests..." rows="3"></textarea>
        <button type="submit" class="btn-primary full-width">Make a Reservation</button>
        <p id="form-msg" style="display:none;color:#4caf50;margin-top:8px;">
          ✔ Reservation confirmed!
        </p>
      </form>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <p>&copy; 2026 Green Forest Restaurant. All rights reserved.</p>
  </footer>

  <script src="script.js"></script>
</body>
</html>


