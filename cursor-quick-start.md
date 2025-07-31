# Cursor for Shopify Development - Quick Start Guide

## 🚀 Get Started in 5 Minutes

### Step 1: Install Cursor
1. Go to [cursor.sh](https://cursor.sh)
2. Download for your OS (Windows/Mac/Linux)
3. Install and open Cursor

### Step 2: Set Up Your Shopify Project
```bash
# Install Shopify CLI
npm install -g @shopify/cli @shopify/theme

# Initialize theme project
shopify theme init my-theme

# Connect to your store
shopify theme dev --store=your-store.myshopify.com
```

### Step 3: Open Project in Cursor
1. Open Cursor
2. File → Open Folder → Select your theme folder
3. Import VS Code settings when prompted

### Step 4: Create Cursor Rules
Create `.cursorrules` in your project root:
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

## 🎯 Essential Commands

### Quick Actions (Cmd/Ctrl + K)
- Select code → `Cmd + K` → Ask questions or request edits
- Perfect for: "Add a button here", "Fix this error", "Explain this code"

### Tab Completion
- Type code → Press `Tab` → Accept AI suggestions
- Perfect for: Building sections, creating schemas, writing Liquid

### AI Agent (Option + Cmd + B)
- Opens full AI assistant
- Perfect for: Complex tasks, debugging, code reviews

---

## 📝 Common Workflows

### 1. Create a New Section
```
1. Type: "section" → Tab
2. Type: "my-section" → Tab
3. Type: "container" → Tab
4. Type: "schema" → Tab
```

### 2. Add Settings to Section
```
1. Type: "text" → Tab
2. Type: "title" → Tab
3. Type: "Section Title" → Tab
```

### 3. Debug Code
```
1. Select problematic code
2. Cmd + K
3. "Why isn't this working?"
```

### 4. Optimize Performance
```
1. Open AI Agent
2. "How can I optimize this code for better performance?"
```

---

## 🔧 MCP Server Setup (Optional)

### Add Shopify MCP
1. Open Cursor Settings (`Cmd + ,`)
2. Navigate to "MCP" section
3. Add new MCP service
4. Paste configuration:
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
5. Restart Cursor

---

## 🎯 Pro Tips

### 1. Start Simple
- Begin with basic questions
- Build complexity gradually
- Test each step

### 2. Provide Context
- Add relevant files to context panel
- Include error messages
- Describe the problem clearly

### 3. Verify Output
- Always test generated code
- Check for syntax errors
- Verify functionality

### 4. Use Specific Prompts
✅ Good: "Add a quick add button to product cards"
❌ Bad: "Create a comprehensive e-commerce solution"

### 5. Restart When Stuck
- After 3-4 exchanges, start fresh
- Take notes from previous attempts
- Provide clear, specific instructions

---

## 🚨 Common Issues & Solutions

### AI Not Understanding
**Solution**: Add more context or restart conversation

### Generated Code Has Errors
**Solution**: Ask AI to debug the specific error

### Slow Responses
**Solution**: Use simpler prompts or break into smaller tasks

### Inconsistent Results
**Solution**: Start fresh conversations for new topics

---

## 📚 Next Steps

1. **Practice**: Try the examples in the main course
2. **Experiment**: Test different AI features
3. **Learn**: Read Shopify documentation
4. **Join**: Connect with the Cursor community
5. **Build**: Start with simple projects

---

## 🎉 You're Ready!

You now have everything you need to start using Cursor effectively for Shopify development. Remember:

- **AI is a tool, not a replacement**
- **Always verify and test code**
- **Start simple and build up**
- **Keep learning and improving**

Happy coding! 🚀