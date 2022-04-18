# Affordable Security

This README only pertains to Max Limit Request and Security Dev Flag implementation.

## Installation

Previous installation for application setup required.

```bash
npm install x-frame-options
npm install strict-transport-security
```
### Adding Max Limit HTTP Request

```typescript
const app = express();
app.use(express.json({limit: '2mb'}));  //adding 2mb limit for express.json - max limit for request
app.use(express.urlencoded({limit: '2mb'})); //adding 2mb limit for express.urlencoded - max limit for http request
```

### Testing with PostMan
Entering workspace for POST request :
```
http://localhost:4000/register
```
Set Body to 

```
x-www-form-urlencoded
```
Under Params create first key as 'TEST' and intoduce value greater or less than 2mb.

## Contributing
Pull requests are allowed.
