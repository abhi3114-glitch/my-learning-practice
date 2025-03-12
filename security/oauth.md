# OAuth 2.0

## Overview
OAuth 2.0 is an authorization framework enabling third-party applications to obtain limited access to user accounts.

## Flows

### Authorization Code Flow
```
1. User clicks "Login with Google"
2. Redirect to: https://accounts.google.com/oauth/authorize
   ?client_id=xxx&redirect_uri=xxx&scope=email&response_type=code
3. User authorizes
4. Redirect back with code: /callback?code=xxx
5. Exchange code for tokens (server-side)
6. Use access token for API calls
```

### Implementation
```javascript
// Redirect to OAuth provider
app.get('/auth/google', (req, res) => {
  const url = `https://accounts.google.com/oauth/authorize?
    client_id=${CLIENT_ID}&
    redirect_uri=${REDIRECT_URI}&
    response_type=code&
    scope=email profile`;
  res.redirect(url);
});

// Handle callback
app.get('/auth/callback', async (req, res) => {
  const { code } = req.query;
  
  // Exchange code for tokens
  const tokens = await fetch('https://oauth2.googleapis.com/token', {
    method: 'POST',
    body: new URLSearchParams({
      code,
      client_id: CLIENT_ID,
      client_secret: CLIENT_SECRET,
      redirect_uri: REDIRECT_URI,
      grant_type: 'authorization_code'
    })
  }).then(r => r.json());
  
  // Use access_token to get user info
  const user = await fetch('https://www.googleapis.com/oauth2/v2/userinfo', {
    headers: { Authorization: `Bearer ${tokens.access_token}` }
  }).then(r => r.json());
  
  // Create session/JWT
});
```

## Tokens
- **Access Token**: Short-lived, used for API access
- **Refresh Token**: Long-lived, used to get new access tokens
- **ID Token**: Contains user identity (OpenID Connect)

## Best Practices
1. Use **PKCE** for public clients
2. Validate **state** parameter
3. Store tokens **securely**
4. Implement **token refresh**

## Resources
- OAuth 2.0 Specification
