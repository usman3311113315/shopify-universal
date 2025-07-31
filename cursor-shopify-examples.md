# Cursor for Shopify Development - Practical Examples

## Quick Reference Guide

### Keyboard Shortcuts
- `Cmd + K` (Mac) / `Ctrl + K` (Windows): Quick actions on selected code
- `Tab`: Accept AI suggestions
- `Option + Cmd + B` (Mac) / `Alt + Ctrl + B` (Windows): Open AI Agent
- `Cmd + ,` (Mac) / `Ctrl + ,` (Windows): Open settings

---

## Example 1: Announcement Bar with Icons

### Step 1: Find the Announcement Bar File
**Agent Query**: "Where can I change the announcement bar messages in the code?"

**Result**: Opens `sections/announcement-bar.liquid`

### Step 2: Add Icon Functionality
**Agent Query**: "Can you add an icon to the announcement bar message with settings?"

**Generated Code**:
```liquid
<!-- sections/announcement-bar.liquid -->
<div class="announcement-bar" style="background-color: {{ section.settings.background_color }};">
  <div class="announcement-bar__container">
    {% if section.settings.icon != blank %}
      <span class="announcement-bar__icon">
        {% case section.settings.icon %}
          {% when 'truck' %}
            <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
              <path d="M20 8h-3V4H3c-1.1 0-2 .9-2 2v11h2c0 1.66 1.34 3 3 3s3-1.34 3-3h4c0 1.66 1.34 3 3 3s3-1.34 3-3h2v-5l-3-4zM6 18.5c-.83 0-1.5-.67-1.5-1.5s.67-1.5 1.5-1.5 1.5.67 1.5 1.5-.67 1.5-1.5 1.5zm13.5-9l1.96 2.5H17V9.5h2.5zm-1.5 9c-.83 0-1.5-.67-1.5-1.5s.67-1.5 1.5-1.5 1.5.67 1.5 1.5-.67 1.5-1.5 1.5z"/>
            </svg>
          {% when 'star' %}
            <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/>
            </svg>
          {% when 'heart' %}
            <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
            </svg>
        {% endcase %}
      </span>
    {% endif %}
    <span class="announcement-bar__message">
      {{ section.settings.message }}
    </span>
  </div>
</div>
```

### Step 3: Add Settings
```json
{% schema %}
{
  "name": "Announcement Bar",
  "settings": [
    {
      "type": "text",
      "id": "message",
      "label": "Message",
      "default": "Free shipping on orders over $50"
    },
    {
      "type": "select",
      "id": "icon",
      "label": "Icon",
      "options": [
        { "value": "", "label": "No Icon" },
        { "value": "truck", "label": "Truck" },
        { "value": "star", "label": "Star" },
        { "value": "heart", "label": "Heart" }
      ],
      "default": ""
    },
    {
      "type": "color",
      "id": "background_color",
      "label": "Background Color",
      "default": "#000000"
    },
    {
      "type": "color",
      "id": "text_color",
      "label": "Text Color",
      "default": "#ffffff"
    }
  ]
}
{% endschema %}
```

### Step 4: Add CSS
```css
/* assets/announcement-bar.css */
.announcement-bar {
  padding: 8px 0;
  text-align: center;
}

.announcement-bar__container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
}

.announcement-bar__icon {
  display: flex;
  align-items: center;
}

.announcement-bar__message {
  font-size: 14px;
  font-weight: 500;
}
```

---

## Example 2: Shipping Info Block

### Step 1: Create Shipping Info Block
**Tab Completion Workflow**:
1. Type: `shipping-info` → Press Tab
2. Type: `div class="shipping-info"` → Press Tab
3. Type: `if product.available` → Press Tab

**Generated Code**:
```liquid
<!-- snippets/shipping-info.liquid -->
<div class="shipping-info">
  {% if product.available %}
    <span class="shipping-info__status shipping-info__status--in-stock">
      {{ section.settings.in_stock_text }}
    </span>
  {% else %}
    <span class="shipping-info__status shipping-info__status--out-of-stock">
      {{ section.settings.out_of_stock_text }}
    </span>
  {% endif %}
</div>
```

### Step 2: Add to Product Template
```liquid
<!-- sections/main-product.liquid -->
<div class="product-form">
  <!-- Existing product form code -->
  
  {% render 'shipping-info' %}
  
  <!-- Rest of product form -->
</div>
```

### Step 3: Add Settings
```json
{
  "type": "text",
  "id": "in_stock_text",
  "label": "In Stock Text",
  "default": "In Stock - Ships in 1-2 business days"
},
{
  "type": "text",
  "id": "out_of_stock_text",
  "label": "Out of Stock Text",
  "default": "Out of Stock"
},
{
  "type": "color",
  "id": "in_stock_color",
  "label": "In Stock Color",
  "default": "#28a745"
},
{
  "type": "color",
  "id": "out_of_stock_color",
  "label": "Out of Stock Color",
  "default": "#dc3545"
}
```

### Step 4: Add CSS
```css
/* assets/shipping-info.css */
.shipping-info {
  margin: 16px 0;
}

.shipping-info__status {
  display: inline-flex;
  align-items: center;
  padding: 8px 12px;
  border-radius: 4px;
  font-size: 14px;
  font-weight: 500;
}

.shipping-info__status--in-stock {
  background-color: {{ section.settings.in_stock_color }};
  color: white;
}

.shipping-info__status--out-of-stock {
  background-color: {{ section.settings.out_of_stock_color }};
  color: white;
}
```

---

## Example 3: Cart Drawer Upsell

### Step 1: Create Upsell Section
**Agent Query**: "Can you please add an upsell functionality in the cart drawer?"

**Generated Files**:

```liquid
<!-- sections/cart-drawer-upsell.liquid -->
<div class="cart-drawer-upsell">
  {% if section.settings.title != blank %}
    <h3 class="cart-drawer-upsell__title">{{ section.settings.title }}</h3>
  {% endif %}
  
  <div class="cart-drawer-upsell__products">
    {% assign upsell_collection = collections[section.settings.collection] %}
    {% if upsell_collection != blank %}
      {% for product in upsell_collection.products limit: section.settings.product_limit %}
        <div class="cart-drawer-upsell__product" data-product-id="{{ product.id }}">
          <div class="cart-drawer-upsell__product-image">
            <img src="{{ product.featured_image | img_url: '150x150' }}" 
                 alt="{{ product.title }}"
                 loading="lazy">
          </div>
          <div class="cart-drawer-upsell__product-info">
            <h4 class="cart-drawer-upsell__product-title">{{ product.title }}</h4>
            <p class="cart-drawer-upsell__product-price">{{ product.price | money }}</p>
            <button class="cart-drawer-upsell__add-button" 
                    data-product-id="{{ product.id }}"
                    {% unless product.available %}disabled{% endunless %}>
              {% if product.available %}
                Add to Cart
              {% else %}
                Out of Stock
              {% endif %}
            </button>
          </div>
        </div>
      {% endfor %}
    {% endif %}
  </div>
</div>
```

### Step 2: Add Settings
```json
{% schema %}
{
  "name": "Cart Drawer Upsell",
  "settings": [
    {
      "type": "text",
      "id": "title",
      "label": "Upsell Title",
      "default": "You might also like"
    },
    {
      "type": "collection",
      "id": "collection",
      "label": "Upsell Collection"
    },
    {
      "type": "range",
      "id": "product_limit",
      "label": "Number of Products",
      "min": 1,
      "max": 6,
      "step": 1,
      "default": 4
    }
  ]
}
{% endschema %}
```

### Step 3: Add JavaScript
```javascript
// assets/cart-drawer-upsell.js
class CartDrawerUpsell {
  constructor() {
    this.init();
  }

  init() {
    this.bindEvents();
  }

  bindEvents() {
    document.addEventListener('click', (e) => {
      if (e.target.classList.contains('cart-drawer-upsell__add-button')) {
        this.addToCart(e.target.dataset.productId);
      }
    });
  }

  async addToCart(productId) {
    try {
      const response = await fetch('/cart/add.js', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          items: [{
            id: productId,
            quantity: 1
          }]
        })
      });

      if (response.ok) {
        // Trigger cart update
        document.dispatchEvent(new CustomEvent('cart:updated'));
        
        // Show success message
        this.showMessage('Product added to cart!', 'success');
      } else {
        throw new Error('Failed to add product');
      }
    } catch (error) {
      console.error('Error adding to cart:', error);
      this.showMessage('Failed to add product to cart', 'error');
    }
  }

  showMessage(message, type) {
    // Create and show notification
    const notification = document.createElement('div');
    notification.className = `notification notification--${type}`;
    notification.textContent = message;
    
    document.body.appendChild(notification);
    
    setTimeout(() => {
      notification.remove();
    }, 3000);
  }
}

// Initialize when DOM is ready
document.addEventListener('DOMContentLoaded', () => {
  new CartDrawerUpsell();
});
```

### Step 4: Add CSS
```css
/* assets/cart-drawer-upsell.css */
.cart-drawer-upsell {
  padding: 20px;
  border-top: 1px solid #e5e5e5;
}

.cart-drawer-upsell__title {
  font-size: 16px;
  font-weight: 600;
  margin-bottom: 16px;
  color: #333;
}

.cart-drawer-upsell__products {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 12px;
}

.cart-drawer-upsell__product {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.cart-drawer-upsell__product-image {
  width: 80px;
  height: 80px;
  margin-bottom: 8px;
  border-radius: 4px;
  overflow: hidden;
}

.cart-drawer-upsell__product-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.cart-drawer-upsell__product-title {
  font-size: 12px;
  font-weight: 500;
  margin-bottom: 4px;
  color: #333;
  line-height: 1.2;
}

.cart-drawer-upsell__product-price {
  font-size: 14px;
  font-weight: 600;
  margin-bottom: 8px;
  color: #000;
}

.cart-drawer-upsell__add-button {
  background-color: #007cba;
  color: white;
  border: none;
  padding: 6px 12px;
  border-radius: 4px;
  font-size: 12px;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.2s;
}

.cart-drawer-upsell__add-button:hover {
  background-color: #005a87;
}

.cart-drawer-upsell__add-button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

/* Notification styles */
.notification {
  position: fixed;
  top: 20px;
  right: 20px;
  padding: 12px 16px;
  border-radius: 4px;
  color: white;
  font-weight: 500;
  z-index: 1000;
}

.notification--success {
  background-color: #28a745;
}

.notification--error {
  background-color: #dc3545;
}
```

---

## Example 4: Shop The Look Section

### Step 1: Create Section with Tab Completion
**Workflow**:
1. Type: `section` → Press Tab
2. Type: `shop-the-look` → Press Tab
3. Type: `container` → Press Tab
4. Type: `header` → Press Tab

**Generated Code**:
```liquid
<!-- sections/shop-the-look.liquid -->
<section class="shop-the-look">
  <div class="container">
    <div class="shop-the-look__header">
      <h2>{{ section.settings.title }}</h2>
      {% if section.settings.subtitle != blank %}
        <p>{{ section.settings.subtitle }}</p>
      {% endif %}
    </div>
    
    <div class="shop-the-look__content">
      {% for block in section.blocks %}
        <div class="shop-the-look__item" {{ block.shopify_attributes }}>
          <div class="shop-the-look__image-container">
            {% if block.settings.lifestyle_image != blank %}
              <img src="{{ block.settings.lifestyle_image | img_url: '600x800' }}" 
                   alt="{{ block.settings.lifestyle_image.alt }}"
                   class="shop-the-look__lifestyle-image">
            {% endif %}
            
            {% if block.settings.product != blank %}
              <div class="shop-the-look__product-dot" 
                   style="left: {{ block.settings.hotspot_x }}%; top: {{ block.settings.hotspot_y }}%;">
                <div class="shop-the-look__product-info">
                  <img src="{{ block.settings.product.featured_image | img_url: '100x100' }}" 
                       alt="{{ block.settings.product.title }}">
                  <h4>{{ block.settings.product.title }}</h4>
                  <p>{{ block.settings.product.price | money }}</p>
                  <button class="shop-the-look__add-button" 
                          data-product-id="{{ block.settings.product.id }}">
                    Add to Cart
                  </button>
                </div>
              </div>
            {% endif %}
          </div>
        </div>
      {% endfor %}
    </div>
  </div>
</section>
```

### Step 2: Add Settings
```json
{% schema %}
{
  "name": "Shop The Look",
  "settings": [
    {
      "type": "text",
      "id": "title",
      "label": "Section Title",
      "default": "Shop The Look"
    },
    {
      "type": "text",
      "id": "subtitle",
      "label": "Section Subtitle",
      "default": "Discover complete outfits and styling inspiration"
    }
  ],
  "blocks": [
    {
      "type": "look",
      "name": "Look",
      "settings": [
        {
          "type": "image_picker",
          "id": "lifestyle_image",
          "label": "Lifestyle Image"
        },
        {
          "type": "product",
          "id": "product",
          "label": "Product"
        },
        {
          "type": "range",
          "id": "hotspot_x",
          "label": "Hotspot X Position",
          "min": 0,
          "max": 100,
          "step": 1,
          "default": 50
        },
        {
          "type": "range",
          "id": "hotspot_y",
          "label": "Hotspot Y Position",
          "min": 0,
          "max": 100,
          "step": 1,
          "default": 50
        }
      ]
    }
  ],
  "presets": [
    {
      "name": "Shop The Look",
      "blocks": [
        {
          "type": "look"
        }
      ]
    }
  ]
}
{% endschema %}
```

### Step 3: Add CSS
```css
/* assets/shop-the-look.css */
.shop-the-look {
  padding: 60px 0;
}

.shop-the-look__header {
  text-align: center;
  margin-bottom: 40px;
}

.shop-the-look__header h2 {
  font-size: 32px;
  font-weight: 600;
  margin-bottom: 16px;
  color: #333;
}

.shop-the-look__header p {
  font-size: 16px;
  color: #666;
  max-width: 600px;
  margin: 0 auto;
}

.shop-the-look__content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 40px;
}

.shop-the-look__item {
  position: relative;
}

.shop-the-look__image-container {
  position: relative;
  border-radius: 8px;
  overflow: hidden;
}

.shop-the-look__lifestyle-image {
  width: 100%;
  height: auto;
  display: block;
}

.shop-the-look__product-dot {
  position: absolute;
  width: 20px;
  height: 20px;
  background-color: #007cba;
  border: 3px solid white;
  border-radius: 50%;
  cursor: pointer;
  transition: transform 0.2s;
}

.shop-the-look__product-dot:hover {
  transform: scale(1.2);
}

.shop-the-look__product-info {
  position: absolute;
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  background: white;
  border-radius: 8px;
  padding: 16px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  min-width: 200px;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.2s, visibility 0.2s;
}

.shop-the-look__product-dot:hover .shop-the-look__product-info {
  opacity: 1;
  visibility: visible;
}

.shop-the-look__product-info img {
  width: 60px;
  height: 60px;
  object-fit: cover;
  border-radius: 4px;
  margin-bottom: 8px;
}

.shop-the-look__product-info h4 {
  font-size: 14px;
  font-weight: 500;
  margin-bottom: 4px;
  color: #333;
}

.shop-the-look__product-info p {
  font-size: 14px;
  font-weight: 600;
  margin-bottom: 8px;
  color: #000;
}

.shop-the-look__add-button {
  background-color: #007cba;
  color: white;
  border: none;
  padding: 6px 12px;
  border-radius: 4px;
  font-size: 12px;
  font-weight: 500;
  cursor: pointer;
  width: 100%;
  transition: background-color 0.2s;
}

.shop-the-look__add-button:hover {
  background-color: #005a87;
}

@media (max-width: 768px) {
  .shop-the-look__content {
    grid-template-columns: 1fr;
  }
  
  .shop-the-look__header h2 {
    font-size: 24px;
  }
}
```

---

## Example 5: Quick Add to Cart

### Step 1: Use Command + K
**Select Code**:
```liquid
{% for product in collection.products %}
  <div class="product-card">
    <img src="{{ product.featured_image | img_url: '300x300' }}" alt="{{ product.title }}">
    <h3>{{ product.title }}</h3>
    <p>{{ product.price | money }}</p>
  </div>
{% endfor %}
```

**Command + K Prompt**: "Add a quick add to cart button to each product card"

**Generated Result**:
```liquid
{% for product in collection.products %}
  <div class="product-card">
    <img src="{{ product.featured_image | img_url: '300x300' }}" alt="{{ product.title }}">
    <h3>{{ product.title }}</h3>
    <p>{{ product.price | money }}</p>
    
    <button class="quick-add-button" 
            data-product-id="{{ product.id }}"
            {% unless product.available %}disabled{% endunless %}>
      {% if product.available %}
        Quick Add
      {% else %}
        Out of Stock
      {% endif %}
    </button>
  </div>
{% endfor %}
```

### Step 2: Add JavaScript
```javascript
// assets/quick-add.js
class QuickAdd {
  constructor() {
    this.init();
  }

  init() {
    this.bindEvents();
  }

  bindEvents() {
    document.addEventListener('click', (e) => {
      if (e.target.classList.contains('quick-add-button')) {
        e.preventDefault();
        this.addToCart(e.target.dataset.productId, e.target);
      }
    });
  }

  async addToCart(productId, button) {
    const originalText = button.textContent;
    
    try {
      // Show loading state
      button.textContent = 'Adding...';
      button.disabled = true;

      const response = await fetch('/cart/add.js', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          items: [{
            id: productId,
            quantity: 1
          }]
        })
      });

      if (response.ok) {
        // Show success state
        button.textContent = 'Added!';
        button.classList.add('quick-add-button--success');
        
        // Trigger cart update
        document.dispatchEvent(new CustomEvent('cart:updated'));
        
        // Reset button after delay
        setTimeout(() => {
          button.textContent = originalText;
          button.disabled = false;
          button.classList.remove('quick-add-button--success');
        }, 2000);
      } else {
        throw new Error('Failed to add product');
      }
    } catch (error) {
      console.error('Error adding to cart:', error);
      button.textContent = 'Error';
      button.classList.add('quick-add-button--error');
      
      setTimeout(() => {
        button.textContent = originalText;
        button.disabled = false;
        button.classList.remove('quick-add-button--error');
      }, 2000);
    }
  }
}

// Initialize when DOM is ready
document.addEventListener('DOMContentLoaded', () => {
  new QuickAdd();
});
```

### Step 3: Add CSS
```css
/* assets/quick-add.css */
.quick-add-button {
  background-color: #007cba;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
  width: 100%;
  margin-top: 8px;
}

.quick-add-button:hover {
  background-color: #005a87;
}

.quick-add-button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

.quick-add-button--success {
  background-color: #28a745;
}

.quick-add-button--error {
  background-color: #dc3545;
}

.product-card {
  position: relative;
  padding: 16px;
  border: 1px solid #e5e5e5;
  border-radius: 8px;
  transition: box-shadow 0.2s;
}

.product-card:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}
```

---

## Common AI Prompts for Shopify Development

### Code Review
- "Review this code for Shopify best practices"
- "How can I optimize this Liquid template?"
- "Are there any security issues in this code?"

### Feature Implementation
- "Add a wishlist button to product cards"
- "Create a product recommendation section"
- "Implement a size guide popup"
- "Add a newsletter signup form"

### Debugging
- "Why isn't this product filter working?"
- "The cart drawer doesn't update when adding products"
- "Images are not loading properly"

### Performance
- "How can I optimize this code for better performance?"
- "What's causing the slow page load?"
- "How can I reduce the bundle size?"

### Styling
- "Make this section responsive"
- "Add hover effects to these buttons"
- "Improve the mobile layout"

### Shopify-Specific
- "How do I access product metafields?"
- "What's the correct Liquid syntax for this?"
- "How do I create a custom section setting?"

---

## Best Practices Checklist

### Before Using AI
- [ ] Understand the basic concept you want to implement
- [ ] Have a clear, specific question or request
- [ ] Gather relevant context (files, code snippets)
- [ ] Know what you want to achieve

### When Using AI
- [ ] Start with simple, specific prompts
- [ ] Provide relevant context
- [ ] Ask for explanations when needed
- [ ] Test the generated code immediately

### After Using AI
- [ ] Review the generated code
- [ ] Test functionality in development
- [ ] Check for syntax errors
- [ ] Verify responsive design
- [ ] Ensure accessibility
- [ ] Optimize for performance

### Quality Assurance
- [ ] Test across different browsers
- [ ] Verify mobile responsiveness
- [ ] Check for console errors
- [ ] Validate HTML structure
- [ ] Test user interactions
- [ ] Verify Shopify-specific functionality

---

## Troubleshooting Common Issues

### AI Not Understanding Context
**Solution**: Add more specific context and restart the conversation

### Generated Code Has Errors
**Solution**: Ask AI to debug the specific error message

### Code Doesn't Work as Expected
**Solution**: Provide detailed feedback and ask for alternatives

### Slow Response Times
**Solution**: Break complex tasks into smaller parts

### Inconsistent Results
**Solution**: Start fresh conversations for new topics

---

This practical guide provides real-world examples and code snippets that you can use immediately with Cursor. Remember to always test and verify AI-generated code before deploying to production.