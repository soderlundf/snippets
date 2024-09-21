# snippets

# Express JSON from req.body

```node
console.log(`Data received: ${req.body ? JSON.stringify(req.body) : 'No data'}`);
```

# Swagger

## Enable Swagger for Express app

```bash
npm i swagger-ui-express swagger-jsdoc
```

## Add `swagger.js` to your project

```node
const swaggerUi = require('swagger-ui-express');
const swaggerJsdoc = require('swagger-jsdoc');

const options = {
    definition: {
        openapi: '3.0.0',
        info: {
            title: 'Gallery Indexer API',
            version: '1.0.0',
            description: 'API documentation for the Gallery Indexer',
        },
    },
    apis: ['./indexer.js'], // Path to the API docs
};

const specs = swaggerJsdoc(options);

module.exports = (app) => {
    app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(specs));
}
```

## Use `swagger.js` using `consign`

```node
consign()
  .include('./swagger.js')
  .into(app);
```