# Cursor for Shopify Development - Complete Mastery Course

## Table of Contents
1. [Introduction to Cursor](#introduction-to-cursor)
2. [Installation & Setup](#installation--setup)
3. [Core Features Deep Dive](#core-features-deep-dive)
4. [Real-World Implementation Examples](#real-world-implementation-examples)
5. [MCP Server Integration](#mcp-server-integration)
6. [Best Practices & Tips](#best-practices--tips)
7. [Advanced Techniques](#advanced-techniques)
8. [Troubleshooting Guide](#troubleshooting-guide)

---

## 1. Introduction to Cursor

### What is Cursor?
Cursor is an AI-powered code editor built on top of VS Code that revolutionizes how Shopify developers work. It combines the familiarity of VS Code with advanced AI capabilities specifically designed for coding tasks.

### Key Benefits for Shopify Developers:
- **Context-Aware AI**: Understands your entire codebase
- **Intelligent Code Completion**: Suggests code based on your project structure
- **Real-time Assistance**: Get help without switching between tools
- **Shopify-Specific Features**: Optimized for Liquid, JavaScript, and Shopify development

### Why Cursor Over Traditional Tools?
- **No Context Switching**: Unlike ChatGPT, Cursor understands your codebase
- **Faster Development**: AI suggestions reduce coding time significantly
- **Better Code Quality**: AI helps maintain consistency and best practices
- **Shopify Integration**: Built-in support for Shopify development workflows

---

## 2. Installation & Setup

### Step 1: Download Cursor
1. Visit [cursor.sh](https://cursor.sh)
2. Click "Download" for your operating system (Windows/Mac/Linux)
3. Install the application

### Step 2: Initial Configuration
```bash
# After installation, Cursor will ask if you want to:
# - Import VS Code settings (Recommended: Yes)
# - Import VS Code extensions (Recommended: Yes)
# - Set up workspace preferences
```

### Step 3: Shopify CLI Setup
```bash
# Install Shopify CLI for remote theme development
npm install -g @shopify/cli @shopify/theme

# Initialize your theme project
shopify theme init

# Connect to your Shopify store
shopify theme dev --store=your-store.myshopify.com
```

### Step 4: Workspace Configuration
Create a `.cursorrules` file in your project root:
```json
{
  "rules": [
    "This is a Shopify theme development project",
    "Use Liquid templating language for dynamic content",
    "Follow Shopify's coding standards and best practices",
    "Implement responsive design principles",
    "Use semantic HTML and accessible markup"
  ]
}
```

---

## 3. Core Features Deep Dive

### Feature 1: Command + K (Quick Actions)

**What it does**: Provides instant code assistance for selected code blocks.

**How to use**:
1. Select any code in your editor
2. Press `Cmd + K` (Mac) or `Ctrl + K` (Windows)
3. Choose between:
   - **Quick Questions**: Ask about the selected code
   - **Submit Edit**: Request modifications to the code

**Example Usage**:
```liquid
<!-- Select this code block -->
{% for product in collection.products %}
  <div class="product-card">
    <img src="{{ product.featured_image | img_url: '300x300' }}" alt="{{ product.title }}">
    <h3>{{ product.title }}</h3>
    <p>{{ product.price | money }}</p>
  </div>
{% endfor %}
```

**Command + K Prompt**: "Add a quick add to cart button to each product card"

**Result**: AI will modify the code to include cart functionality.

### Feature 2: Tab Completion (Intelligent Suggestions)

**What it does**: Provides context-aware code suggestions as you type.

**How to use**:
1. Start typing code
2. Press `Tab` to accept suggestions
3. Continue typing and pressing `Tab` for multi-step completions

**Example Workflow**:
```liquid
<!-- Type: "section" -->
<section class="shop-the-look">
  <!-- Tab to complete -->
  <div class="container">
    <!-- Tab to complete -->
    <div class="shop-the-look__header">
      <!-- Tab to complete -->
      <h2>{{ section.settings.title }}</h2>
    </div>
  </div>
</section>
```

**Advanced Tab Usage**:
```liquid
<!-- Type: "schema" and press Tab -->
{% schema %}
{
  "name": "Shop The Look",
  "settings": [
    {
      "type": "text",
      "id": "title",
      "label": "Section Title",
      "default": "Shop The Look"
    }
  ]
}
{% endschema %}
```

### Feature 3: AI Agent (The Powerhouse)

**What it does**: Comprehensive AI assistant that can handle complex tasks and understand your entire codebase.

**How to access**:
- **Method 1**: `View → Appearance → Secondary Sidebar`
- **Method 2**: `Option + Cmd + B` (Mac) or `Alt + Ctrl + B` (Windows)

**Agent Interface Components**:

1. **Context Panel**:
   - Add files, code, or documentation
   - Provide specific context for your questions

2. **Mode Selection**:
   - **Agent Mode**: Full AI assistant (recommended)
   - **Ask Mode**: Simple Q&A
   - **Edit Mode**: Direct code editing

3. **Model Selection**:
   - **Auto Select**: Automatically chooses best model
   - **Claude 3.5 Sonnet**: Best for complex tasks
   - **GPT-4**: Good for general coding tasks

4. **Image Upload**: Add screenshots or mockups for visual context

**Example Agent Workflows**:

**Simple Question**:
```
Q: "How do I center a div in CSS?"
A: Agent provides CSS solutions with explanations
```

**Codebase-Specific Question**:
```
Q: "Where can I find the announcement bar code?"
A: Agent searches your codebase and opens the relevant file
```

**Complex Task**:
```
Q: "Add an upsell section to the cart drawer"
A: Agent creates complete implementation with all necessary files
```

---

## 4. Real-World Implementation Examples

### Example 1: Low Complexity, Low Knowledge Task

**Scenario**: Client wants icons before announcement bar messages.

**Step-by-Step Process**:

1. **Ask Agent for Location**:
   ```
   "Where can I change the announcement bar messages in the code?"
   ```

2. **Add Context**:
   - Select the announcement bar file
   - Add to context panel

3. **Request Implementation**:
   ```
   "Can you add an icon to the announcement bar message with settings?"
   ```

4. **Review and Refine**:
   ```liquid
   <!-- Generated code -->
   <div class="announcement-bar">
     {% if section.settings.icon != blank %}
       <span class="announcement-bar__icon">
         {{ section.settings.icon }}
       </span>
     {% endif %}
     <span class="announcement-bar__message">
       {{ section.settings.message }}
     </span>
   </div>
   ```

5. **Add Settings**:
   ```json
   {
     "type": "select",
     "id": "icon",
     "label": "Icon",
     "options": [
       { "value": "truck", "label": "Truck" },
       { "value": "star", "label": "Star" },
       { "value": "heart", "label": "Heart" }
     ]
   }
   ```

6. **Style the Icons**:
   ```css
   .announcement-bar__icon {
     margin-right: 8px;
     font-size: 16px;
   }
   ```

### Example 2: Low Complexity, High Knowledge Task

**Scenario**: Add shipping time display to product page.

**Process**:
1. **Use Tab Completion** (since you know what to do):
   ```liquid
   <!-- Type: "shipping-info" and press Tab -->
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

2. **Add Settings via Tab**:
   ```json
   {
     "type": "text",
     "id": "in_stock_text",
     "label": "In Stock Text",
     "default": "In Stock"
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
     "label": "In Stock Color"
   },
   {
     "type": "color",
     "id": "out_of_stock_color",
     "label": "Out of Stock Color"
   }
   ```

### Example 3: High Complexity Task (Any Knowledge Level)

**Scenario**: Build upsell functionality in cart drawer.

**Process**:
1. **Use Agent for Complex Tasks**:
   ```
   "Can you please add an upsell functionality in the cart drawer?"
   ```

2. **Agent Creates Complete Implementation**:
   - Creates new section file
   - Adds JavaScript functionality
   - Implements cart integration
   - Handles styling

3. **Review Generated Code**:
   ```liquid
   <!-- Generated cart-drawer-upsell.liquid -->
   <div class="cart-drawer-upsell">
     <h3>{{ section.settings.title }}</h3>
     <div class="cart-drawer-upsell__products">
       {% for product in collections[section.settings.collection].products limit: 4 %}
         <div class="cart-drawer-upsell__product">
           <img src="{{ product.featured_image | img_url: '150x150' }}" alt="{{ product.title }}">
           <h4>{{ product.title }}</h4>
           <p>{{ product.price | money }}</p>
           <button class="add-to-cart" data-product-id="{{ product.id }}">
             Add to Cart
           </button>
         </div>
       {% endfor %}
     </div>
   </div>
   ```

4. **Add Settings**:
   ```json
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
   }
   ```

5. **Refine and Fix Issues**:
   ```
   "The cart drawer does not rerender when adding upsell products. Can you fix that?"
   ```

---

## 5. MCP Server Integration

### What is MCP (Model Context Protocol)?
MCP allows Cursor to connect to external systems and data sources, providing additional context for AI assistance.

### Shopify MCP Server Setup

**Step 1: Get MCP Configuration**
Visit: [Shopify MCP Server GitHub](https://github.com/shopify/shopify-mcp-server)

**Step 2: Add to Cursor**
1. Open Cursor Settings (`Cmd + ,`)
2. Navigate to "MCP" section
3. Add new MCP service
4. Paste the configuration:

```json
{
  "mcpServers": {
    "shopify-dev": {
      "command": "npx",
      "args": ["@shopify/mcp-server"],
      "env": {}
    }
  }
}
```

**Step 3: Restart Cursor**
- Close and reopen Cursor
- Verify green dot appears next to "Shopify Dev MCP"

### Using Shopify MCP Features

**Feature 1: Search Shopify Dev Documentation**
```
Q: "How to implement settings for sections?"
A: Agent uses MCP to search official Shopify docs
```

**Feature 2: Access GraphQL Schema**
```
Q: "What are the available fields for the Product object?"
A: Agent queries Shopify's GraphQL schema
```

**Example MCP Usage**:
```
"Show me how to create a product recommendation section"
```

Agent will:
1. Search Shopify documentation
2. Provide official implementation guide
3. Generate code based on current best practices

---

## 6. Best Practices & Tips

### Tip 1: Know How to Code
**Why**: AI is a tool, not a replacement for coding knowledge.
**How**: 
- Understand basic programming concepts
- Know Shopify Liquid syntax
- Familiarize yourself with CSS and JavaScript
- Learn Shopify's theme structure

### Tip 2: Ask Simple Questions
**Why**: Complex prompts confuse AI and slow down development.
**Examples**:
- ✅ "Add a quick add button to product cards"
- ❌ "Create a comprehensive e-commerce solution with advanced cart functionality, user authentication, and payment processing"

**Best Practices**:
- One question per prompt
- Be specific but concise
- Use clear, direct language
- Avoid ambiguous terms

### Tip 3: Start Fresh When Stuck
**Why**: AI gets confused with long conversations about the same problem.
**When to restart**:
- After 3-4 back-and-forth exchanges
- When AI starts giving inconsistent answers
- When the solution becomes overly complex

**How to restart**:
1. Take notes from the conversation
2. Start a new chat
3. Provide clear, specific instructions
4. Include relevant context

### Tip 4: Always Verify AI Output
**Why**: AI can make mistakes, especially with Shopify-specific code.
**Verification checklist**:
- [ ] Test the code in development
- [ ] Check for syntax errors
- [ ] Verify functionality works as expected
- [ ] Review for security issues
- [ ] Ensure responsive design
- [ ] Test across different browsers

**Common AI Mistakes in Shopify**:
- Incorrect Liquid syntax
- Missing schema settings
- Hardcoded values instead of dynamic content
- Inconsistent naming conventions

### Tip 5: Continue Learning
**Why**: AI knowledge is limited to its training data.
**How to stay updated**:
- Read Shopify documentation regularly
- Follow Shopify's developer blog
- Join Shopify developer communities
- Experiment with new features
- Share knowledge with the community

---

## 7. Advanced Techniques

### Technique 1: Context Management
**Strategy**: Provide relevant context for better AI responses.

**Methods**:
1. **File Context**: Add specific files to the context panel
2. **Code Snippets**: Include relevant code blocks
3. **Documentation**: Add Shopify docs or your own notes
4. **Screenshots**: Upload mockups or reference images

**Example**:
```
Context: [product-card.liquid, theme.css, product-page.liquid]
Question: "How can I add a wishlist button to product cards?"
```

### Technique 2: Progressive Enhancement
**Strategy**: Build features incrementally with AI assistance.

**Process**:
1. Start with basic functionality
2. Use AI to add features one by one
3. Test each addition
4. Refine and optimize

**Example Workflow**:
```
Step 1: "Create a basic product card"
Step 2: "Add hover effects to the card"
Step 3: "Include a quick add button"
Step 4: "Add wishlist functionality"
Step 5: "Implement loading states"
```

### Technique 3: Code Review with AI
**Strategy**: Use AI to review and improve existing code.

**Process**:
1. Select code block
2. Use Command + K
3. Ask: "Review this code for best practices"
4. Implement suggested improvements

**Review Questions**:
- "Is this code following Shopify best practices?"
- "How can I optimize this for performance?"
- "Are there any security issues in this code?"
- "How can I make this more accessible?"

### Technique 4: Debugging with AI
**Strategy**: Use AI to identify and fix issues.

**Process**:
1. Describe the problem
2. Provide error messages
3. Include relevant code
4. Let AI suggest solutions

**Example**:
```
Problem: "The cart drawer doesn't update when adding products"
Error: "Uncaught TypeError: Cannot read property 'update' of undefined"
Code: [cart-drawer.js, cart-functions.js]
```

### Technique 5: Performance Optimization
**Strategy**: Use AI to identify and fix performance issues.

**Common Optimizations**:
- Lazy loading images
- Minimizing JavaScript
- Optimizing CSS
- Reducing API calls
- Implementing caching

**AI Prompts**:
- "How can I optimize this code for better performance?"
- "What's causing the slow page load?"
- "How can I reduce the bundle size?"

---

## 8. Troubleshooting Guide

### Common Issues and Solutions

**Issue 1: AI Not Understanding Context**
**Symptoms**: AI gives generic answers or doesn't understand your codebase
**Solutions**:
- Add more context to the conversation
- Include relevant files in context panel
- Be more specific in your questions
- Restart the conversation

**Issue 2: Generated Code Doesn't Work**
**Symptoms**: AI creates code that causes errors or doesn't function
**Solutions**:
- Check for syntax errors
- Verify Shopify-specific syntax
- Test in development environment
- Ask AI to debug the issue

**Issue 3: Slow Response Times**
**Symptoms**: AI takes too long to respond
**Solutions**:
- Use simpler prompts
- Break complex tasks into smaller parts
- Check your internet connection
- Try a different AI model

**Issue 4: Inconsistent Suggestions**
**Symptoms**: AI gives different answers for the same question
**Solutions**:
- Provide consistent context
- Use the same AI model
- Be more specific in your prompts
- Start fresh conversations for new topics

**Issue 5: MCP Server Not Working**
**Symptoms**: Shopify MCP features not available
**Solutions**:
- Verify MCP configuration
- Restart Cursor
- Check network connection
- Update MCP server

### Debugging Workflow

1. **Identify the Problem**
   - What's not working?
   - What error messages appear?
   - When does the issue occur?

2. **Gather Context**
   - Relevant code files
   - Error messages
   - Steps to reproduce

3. **Ask AI for Help**
   - Describe the problem clearly
   - Provide all relevant context
   - Include error messages

4. **Test Solutions**
   - Implement AI suggestions
   - Test in development
   - Verify functionality

5. **Iterate if Needed**
   - If solution doesn't work, ask for alternatives
   - Provide feedback to AI
   - Try different approaches

### Performance Optimization Checklist

- [ ] Images are optimized and lazy-loaded
- [ ] JavaScript is minified and bundled
- [ ] CSS is optimized and critical styles are inlined
- [ ] API calls are minimized and cached
- [ ] Third-party scripts are loaded asynchronously
- [ ] Database queries are optimized
- [ ] CDN is properly configured
- [ ] Browser caching is enabled

---

## Conclusion

Cursor is a powerful tool that can significantly improve your Shopify development workflow. By mastering these features and following the best practices outlined in this course, you can:

- **Increase Development Speed**: Complete tasks in minutes instead of hours
- **Improve Code Quality**: AI helps maintain consistency and best practices
- **Reduce Errors**: AI catches common mistakes and suggests improvements
- **Stay Updated**: MCP integration keeps you informed of latest Shopify features
- **Focus on Creativity**: Let AI handle repetitive tasks while you focus on unique solutions

Remember: AI is a tool to enhance your skills, not replace them. The best results come from combining AI assistance with solid coding knowledge and critical thinking.

**Next Steps**:
1. Install Cursor and set up your development environment
2. Practice with the examples in this course
3. Integrate the Shopify MCP server
4. Start with simple tasks and gradually tackle more complex projects
5. Join the Cursor and Shopify developer communities for support

Happy coding with Cursor! 🚀