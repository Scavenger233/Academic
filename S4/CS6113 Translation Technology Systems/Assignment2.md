# Temu 购物流程 BPMN 图

```mermaid
graph TD
    A[🛍️ User Browses Products] --> B{Product Available?}
    
    B -- Yes --> C[🛒 Add to Cart]
    B -- No --> X[❌ Show Out of Stock Message]
    
    C --> D[🔍 Review Cart]
    D --> E[💳 Proceed to Checkout]
    
    E --> F{User Logged In?}
    F -- No --> G[🔑 User Logs In / Registers] --> E
    F -- Yes --> H[📦 Select Shipping Method]
    
    H --> I[💰 Choose Payment Method]
    I --> J[✅ Confirm & Pay]
    
    J --> K{Payment Successful?}
    K -- No --> L[⚠️ Show Payment Error] --> I
    K -- Yes --> M[📨 Order Confirmation Sent]
    
    M --> N[🚀 Order Processed & Shipped]
    N --> O[📦 Order Delivered]
