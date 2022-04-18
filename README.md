# Affordable Security

This README only pertains to Max Limit Request and Security Dev Flag implementation.

## Installation

Previous installation for application setup required.

```bash
npm install x-frame-options
npm install strict-transport-security
```
## Adding Max Limit HTTP Request
In pkg/server/src/app.ts
```typescript
const app = express();
app.use(express.json({limit: '2mb'}));  //adding 2mb limit for express.json - max limit for request
app.use(express.urlencoded({limit: '2mb'})); //adding 2mb limit for express.urlencoded - max limit for http request
```

#### Testing with PostMan
Entering workspace for POST request :
```
http://localhost:4000/register
```
Set Body to 

```
x-www-form-urlencoded
```
Under Params create first key as 'TEST' and intoduce value greater or less than 2mb.
After hitting send, "entity request too large" error is received if param value is greater than 2mb.

## Adding Security Dev Flags
In pkg/app/.env
add
```
DISABLE_SECURITY=false
```

In pkg/server/.env
add
```
DISABLE_SECURITY=false
```

In pkg/server/src/app.ts
```typescript
const hsts = require('hsts');

const xFrameOptions = require('x-frame-options');

//declaration of security dev flag if statement
//change DISABLE_SECURITY in app\env. and server\env.
if(process.env.DISABLE_SECURITY == "false") {
  app.use(xFrameOptions()); // enables/disables X-Frame-Options header checked with Postman

  app.use(hsts({  // enables/disables Strict-Transport-Security header checked with Postman
    maxAge: 3600,
    includeSubDomains: true,
  }));
}
```

### Testing with PostMan
Entering workspace for POST request :
```
http://localhost:4000/register
```
If env. variables set to 
```
DISABLE_SECURITY=false
```
After hitting send, Headers(12) would show including X-Frame-Options and Strict-Transport-Security.

If env. variables set to 
```
DISABLE_SECURITY=true
```
After hitting send, Headers(10) would show including basic headers.

## Contributing
Pull requests are allowed.
