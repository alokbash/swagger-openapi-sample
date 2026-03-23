# Bookstore API Documentation

A comprehensive, interactive API documentation site built with Swagger UI that showcases a complete RESTful bookstore management system. Features dynamic YAML loading, modern responsive design, and easy deployment to any static hosting platform.

## Live Demo

- **GitHub Repository**: `https://github.com/alokbash/swagger-openapi-sample`

## API Overview

The Bookstore API provides a complete solution for managing an online bookstore.

## Project Structure

```
swagger-openapi-sample/
├── index.html          # Main Swagger UI page with dynamic YAML loading
├── openapi.yaml        # Your OpenAPI 3.x specification
├── package.json        # Project metadata and scripts
├── .gitignore          # Git ignore patterns
└── README.md           # This file
```

## Local Development

### Prerequisites

- Node.js 16+ (for development tools)
- A modern web browser
- Git

### Quick Start

1. **Clone the repository**:
   ```bash
   git clone https://github.com/alokbash/swagger-openapi-sample.git
   cd swagger-openapi-sample
   ```

2. **Install development dependencies** (optional):
   ```bash
   npm install
   ```

3. **Start local development server**:
   ```bash
   npm run dev
   ```
   
   Or serve manually:
   ```bash
   # Using Python
   python -m http.server 3000
   
   # Using Node.js http-server
   npx http-server . -p 3000 -c-1 --cors
   
   # Using PHP
   php -S localhost:3000


4. **Open your browser** to `http://localhost:3000`

### Available Scripts

```bash
npm run start      # Start development server on port 3000
npm run dev        # Start development server and open browser
npm run validate   # Validate OpenAPI specification syntax and structure
npm run lint       # Lint YAML syntax and formatting
```

### Testing the API Documentation

1. **Start the development server**:
   ```bash
   npm run dev
   ```

2. **Open your browser** to `http://localhost:3000`

3. **Explore the API**:
   - Browse the different endpoint categories (Books, Orders, Users)
   - Try out the interactive examples
   - Test authentication flows
   - Examine request/response schemas

### Endpoints Overview

#### Books API
- `GET /books` - List books with filtering, sorting, and pagination
- `GET /books/{bookId}` - Get detailed book information
- `POST /books` - Create new book (admin only)

#### Orders API
- `GET /orders` - List user's orders with status filtering
- `POST /orders` - Create new order with items and shipping
- `GET /orders/{orderId}` - Get specific order details

#### Users API
- `POST /users/register` - Register new user account
- `POST /users/login` - Authenticate and get JWT token
- `GET /users/profile` - Get user profile information

### Editing Your API Specification

1. **Edit the OpenAPI spec**: Modify `openapi.yaml` with your API endpoints, schemas, and documentation
2. **Validate your changes**: Run `npm run validate` to ensure valid OpenAPI format
3. **Test locally**: The page will automatically reload and display your changes
4. **Use Swagger Editor**: Visit [editor.swagger.io](https://editor.swagger.io) for visual editing

## Deployment

This is a static site that can be deployed to any hosting platform:

### Static Hosting Platforms
- **GitHub Pages**: Enable Pages in repository settings
- **Vercel**: Connect your GitHub repository
- **Netlify**: Drag and drop or connect via Git
- **Any web server**: Upload files to your server

### Deployment Steps

1. **Push to GitHub**:
   ```bash
   git add .
   git commit -m "Ready for deployment"
   git push origin main
   ```

2. **Deploy to your preferred platform**:
   - Most platforms will automatically detect this as a static site
   - No build step required - just serve the files
   - Ensure your hosting platform serves YAML files with correct MIME type


## Customization

### Styling Customization

Edit the `<style>` section in `index.html` to customize:

```css
/* Brand colors */
:root {
  --primary-color: #3498db;
  --secondary-color: #2ecc71;
  --accent-color: #e74c3c;
}

/* Custom styling examples */
.swagger-ui .info .title {
  color: var(--primary-color);
  font-family: 'Your Brand Font', sans-serif;
}
```

### Swagger UI Configuration

Modify the `SwaggerUIBundle` configuration in `index.html`:

```javascript
SwaggerUIBundle({
  spec: spec,
  dom_id: '#swagger-ui',
  deepLinking: true,
  tryItOutEnabled: true,
  
  // Customization options
  defaultModelsExpandDepth: 2,     // How deep to expand models
  docExpansion: 'list',            // 'list', 'full', or 'none'
  filter: true,                    // Enable search/filter
  showExtensions: true,            // Show vendor extensions
  showCommonExtensions: true,      // Show common extensions
  
  // Theme and layout
  layout: "BaseLayout",
  
  // Request interceptor for authentication
  requestInterceptor: (request) => {
    const token = localStorage.getItem('authToken');
    if (token) {
      request.headers.Authorization = `Bearer ${token}`;
    }
    return request;
  }
});
```

### Multiple API Specifications

To support multiple API versions or services:

1. **Create additional YAML files**:
   ```
   openapi-v1.yaml    # Version 1 API
   openapi-v2.yaml    # Version 2 API
   admin-api.yaml     # Admin API
   ```

2. **Add version switching**:
   ```javascript
   // Get version from URL parameter
   const urlParams = new URLSearchParams(window.location.search);
   const version = urlParams.get('version') || 'v1';
   const specUrl = `./openapi-${version}.yaml`;
   ```

3. **Update navigation**:
   ```html
   <div class="api-version-selector">
     <a href="?version=v1">API v1</a>
     <a href="?version=v2">API v2</a>
     <a href="?version=admin">Admin API</a>
   </div>
   ```

### Custom Branding

Add your company branding:

```html
<!-- Add to index.html head -->
<link rel="icon" href="./favicon.ico">
<meta property="og:title" content="Your Company API Documentation">
<meta property="og:description" content="Comprehensive API documentation">
<meta property="og:image" content="./api-preview.png">
```

## Troubleshooting

### Common Issues & Solutions

#### "Error Loading API Documentation"
**Symptoms**: Error page appears instead of API documentation

**Solutions**:
- ✅ Ensure `openapi.yaml` exists in the project root
- ✅ Validate YAML syntax: `npm run lint`
- ✅ Check browser console for detailed errors (F12)
- ✅ Verify file is accessible via HTTP (not file:// protocol)
- ✅ Test with a simple HTTP server: `npm run start`

#### CORS Issues in Local Development
**Symptoms**: "Access blocked by CORS policy" errors

**Solutions**:
- ✅ Always use an HTTP server (not file:// protocol)
- ✅ Use provided npm scripts: `npm run dev`
- ✅ For custom servers, enable CORS headers
- ✅ Check that YAML file is served with correct MIME type

#### Deployment Issues
**Symptoms**: Site doesn't deploy or shows errors

**Solutions**:
- ✅ Check deployment logs in your hosting platform's dashboard
- ✅ Ensure all files are committed to Git: `git status`
- ✅ Verify YAML files are served with correct MIME type
- ✅ Check routing configuration for your hosting platform
- ✅ Validate OpenAPI spec before deployment: `npm run validate`

#### Swagger UI Layout Issues
**Symptoms**: "No layout defined" errors

**Solutions**:
- ✅ Use correct layout names: `"BaseLayout"` or `"StandaloneLayout"`
- ✅ Check Swagger UI version compatibility
- ✅ Verify CDN links are accessible

#### Mobile Display Issues
**Symptoms**: Poor mobile experience

**Solutions**:
- ✅ Ensure viewport meta tag is present
- ✅ Test responsive design with browser dev tools
- ✅ Check CSS media queries in custom styles

### Debugging Steps

1. **Check Browser Console** (F12):
   ```
   Look for JavaScript errors, network failures, or CORS issues
   ```

2. **Validate OpenAPI Spec**:
   ```bash
   npm run validate
   npm run lint
   ```

3. **Test Local Server**:
   ```bash
   npm run start
   # Then visit http://localhost:3000
   ```

4. **Check Network Tab**:
   ```
   Verify openapi.yaml loads successfully (200 status)
   Check response headers and content type
   ```

### Getting Help

- [Swagger UI Documentation](https://swagger.io/docs/open-source-tools/swagger-ui/)
- [OpenAPI Specification Guide](https://swagger.io/specification/)
- [Report Issues](https://github.com/alokbash/swagger-openapi-sample/issues)

