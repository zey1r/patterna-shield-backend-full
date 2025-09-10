# Patterna Shield Backend - API Documentation

## API Test Examples

Bu dosya, Patterna Shield Backend API'sini test etmek için örnek istekler içerir.

### 1. Health Check
```bash
curl -X GET "http://localhost:8007/health"
```

### 2. Fraud Detection
```bash
curl -X POST "http://localhost:8007/api/v1/fraud-detection" \
  -H "Content-Type: application/json" \
  -d '{
    "transaction_id": "TXN_123456",
    "amount": 15000.0,
    "currency": "TRY",
    "merchant_name": "Test Merchant",
    "customer_id": "CUST_789",
    "card_last_4": "1234"
  }'
```

### 3. URL Analysis
```bash
curl -X POST "http://localhost:8007/api/v1/analyze-url" \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://suspicious-site.com/login",
    "user_id": "user123"
  }'
```

### 4. Email Analysis
```bash
curl -X POST "http://localhost:8007/api/v1/analyze-email" \
  -H "Content-Type: application/json" \
  -d '{
    "email_content": "ACIL! Hesabınız askıya alındı, hemen link'e tıklayın",
    "sender_email": "fake@suspicious-bank.com",
    "subject": "Acil Güvenlik Uyarısı",
    "user_id": "user123"
  }'
```

### 5. Phone Analysis
```bash
curl -X POST "http://localhost:8007/api/v1/analyze-phone" \
  -H "Content-Type: application/json" \
  -d '{
    "phone_number": "+90850123456",
    "caller_name": "Suspicious Caller"
  }'
```

### 6. System Statistics
```bash
curl -X GET "http://localhost:8007/api/v1/stats"
```

### 7. Demo Analysis
```bash
curl -X POST "http://localhost:8007/api/v1/demo-analysis"
```

## Python Examples

### Using requests library:

```python
import requests

# Fraud Detection
response = requests.post(
    "http://localhost:8007/api/v1/fraud-detection",
    json={
        "transaction_id": "TXN_123456",
        "amount": 15000.0,
        "currency": "TRY",
        "merchant_name": "Test Merchant",
        "customer_id": "CUST_789",
        "card_last_4": "1234"
    }
)
print(response.json())

# URL Analysis
response = requests.post(
    "http://localhost:8007/api/v1/analyze-url",
    json={
        "url": "https://suspicious-site.com/login",
        "user_id": "user123"
    }
)
print(response.json())
```

## Expected Responses

### High Risk Transaction:
```json
{
  "success": true,
  "data": {
    "transaction_id": "TXN_123456",
    "risk_score": 70,
    "risk_level": "HIGH",
    "recommended_action": "BLOCK",
    "risk_factors": [
      "Yüksek tutar",
      "Şüpheli merchant"
    ],
    "analysis_timestamp": "2025-09-10T12:00:00",
    "processing_time_ms": 45
  },
  "message": "İşlem analizi tamamlandı"
}
```

### URL Analysis:
```json
{
  "success": true,
  "data": {
    "url": "https://suspicious-site.com/login",
    "domain": "suspicious-site.com",
    "risk_score": 85,
    "risk_level": "HIGH",
    "risk_factors": [
      "Şüpheli parametreler"
    ],
    "is_safe": false,
    "analysis_timestamp": "2025-09-10T12:00:00"
  },
  "message": "URL analizi tamamlandı"
}
```
