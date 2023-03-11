# Protect your Webhook from being compromised!

This JavaScript script creates a server to handle requests to protect your webhook from being compromised. Even if your stealer is decrypted, they won't be able to delete your webhook or send spam messages to it.

## Code Example

```javascript
const crypto = require('crypto');
const wh = 'webhook to protect here';

function verifyWH(body, workingWH) {
  const apiWH = 'sha1=' + crypto.createHmac('sha1', wh).update(body).digest('hex');

  return apiWH === workingWH;
}

const http = require('http');

const server = http.createServer((req, res) => {
  let body = '';

  req.on('data', (chunk) => {
    body += chunk.toString();
  });

  req.on('end', () => {
    const workingWH = req.headers['x-hub-signature'];

    if (verifyWH(body, workingWH)) {
      console.log('Request sent');
      res.end('Request sent');
    } else {
      console.log('Request not sent');
      res.statusCode = 401;
      res.end('Request not sent');
    }
  });
});

server.listen(3000);
```

# Explanation

The code is a simple Node.js script that creates a server to handle incoming requests to your webhook. Here is a step-by-step explanation of what the code does:

1. The script imports the crypto module and sets a wh variable to hold the webhook URL you want to protect.
2. The verifyWH function is defined to check if the webhook signature in the request matches the expected signature. It takes two parameters: body (the request body) and workingWH (the signature from the request).
3. Inside the verifyWH function, the crypto.createHmac method is used to create a HMAC object that uses the SHA1 algorithm and your webhook URL (wh) as the secret key. The update method is called on the HMAC object with the request body as the parameter, and then digest('hex') is called to convert the HMAC to a hexadecimal string.
4. The apiWH variable is set to a string that includes the prefix sha1= and the hexadecimal webhook signature generated in the previous step.
5. The http module is imported, and a new server is created using the http.createServer method. The server takes two parameters: a request handler function and a response handler function.
6. The request handler function is defined to handle incoming requests. When a request is received, the request body is read and added to a body variable using the req.on('data') method. When the request ends, the webhook signature from the request headers is stored in a workingWH variable.
7. The verifyWH function is called with the request body and webhook signature as parameters. If the webhook signature is valid, the server sends a Request sent message to the console and responds to the client with a Request sent message. If the webhook signature is invalid, the server sends a Request not sent message to the console, sets the response status code to 401 Unauthorized, and responds to the client with a Request not sent message.
8. The server is set to listen on port 3000.

That's it! With this code in place, your webhook is now protected from unauthorized requests.
