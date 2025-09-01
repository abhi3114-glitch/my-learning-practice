# Webhooks

## Overview
Webhooks are HTTP callbacks that notify your application when events occur in external systems.

## Receiving Webhooks
```javascript
app.post('/webhooks/stripe', express.raw({type: 'application/json'}), (req, res) => {
  const sig = req.headers['stripe-signature'];
  
  try {
    const event = stripe.webhooks.constructEvent(req.body, sig, webhookSecret);
    
    switch (event.type) {
      case 'payment_intent.succeeded':
        handlePaymentSuccess(event.data.object);
        break;
      case 'customer.subscription.deleted':
        handleSubscriptionCanceled(event.data.object);
        break;
    }
    
    res.json({ received: true });
  } catch (err) {
    res.status(400).send(`Webhook Error: ${err.message}`);
  }
});
```

## Sending Webhooks
```javascript
async function sendWebhook(url, payload, secret) {
  const signature = crypto
    .createHmac('sha256', secret)
    .update(JSON.stringify(payload))
    .digest('hex');

  await fetch(url, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'X-Webhook-Signature': signature
    },
    body: JSON.stringify(payload)
  });
}
```

## Best Practices
1. **Verify signatures** to ensure authenticity
2. **Respond quickly** (< 5s) with 200 status
3. **Process async** - queue for heavy processing
4. **Implement retries** for failed deliveries
5. **Log all webhook events**

## Resources
- Webhook.site (testing)
