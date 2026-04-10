---
name: exchange-converter
description: Convert between fiat currencies AND cryptocurrencies using live exchange rates with offline cache support. Trigger when user says "convert currency", "how much is X in Y", "exchange rate", "convert BTC to USD", "how much is ETH in EUR", "help", or asks to convert an amount from one currency/crypto to another.
metadata:
  homepage: https://github.com/victoralv/exchange-converter
---

# Exchange Converter

Supports **fiat currencies** (USD, EUR, GBP, JPY, MXN...) and **cryptocurrencies** (BTC, ETH, SOL, BNB, XRP, DOGE, ADA, DOT, MATIC, LTC, and hundreds more).

## Examples

- "Convert 100 USD to EUR"
- "How much is 50 euros in Japanese yen?"
- "Exchange rate from GBP to USD"
- "500 MXN to dollars"
- "Convert 0.5 BTC to USD"
- "How much is 1 ETH in EUR?"
- "1000 DOGE to GBP"
- "What currencies are available?"
- "Help" / "What can you do?"

## Instructions

When the user asks to convert currencies/crypto or check exchange rates:

1. Identify the action:
   - **help**: user asks for help, what this does, or how to use it → set `action` to `"help"`
   - **list**: user asks to see available/cached/supported currencies → set `action` to `"list"`
   - **convert**: user asks to convert an amount → set `action` to `"convert"` (default)

2. For **convert**: identify the amount, source currency/crypto, and target currency/crypto.
3. Use standard codes: ISO 4217 for fiat (USD, EUR...) and ticker symbols for crypto (BTC, ETH, SOL...). Always uppercase.
4. If the user does not specify an amount, default to 1.
5. **Before calling `run_js`, confirm these extracted values to yourself:**
   - action
   - amount (number, convert only)
   - from (uppercase code, convert only)
   - to (uppercase code, convert only)
6. Call the `run_js` tool:
   - For **help**: `{"action": "help"}`
   - For **list**: `{"action": "list"}`
   - For **convert**: `{"action": "convert", "amount": 100, "from": "USD", "to": "EUR"}`
   - **Double-check** that the JSON values match what the user asked for before calling.

## IMPORTANT: Multiple Conversions in One Chat

When the user asks for multiple conversions in the same chat session, IGNORE all previous conversion results completely. Each conversion is independent. Only read values from the LATEST `run_js` response (identified by its unique `id` field). Never mix numbers from a previous conversion into the current one.

## Output Format (MANDATORY)

### For `action: "help"` response

Output the `help` field value exactly as-is.

### For `action: "list"` response

Fields: `total`, `date`, `currencies` (space-separated list of all currency codes).

Output exactly this, no changes:
📋 {total} currencies available (rates from {date}):

{currencies}

### For `action: "convert"` response

The `run_js` response is a JSON object. Read EACH field individually and place it into the template below. Do NOT look at previous messages for any values.

Fields returned:
- `id`: unique request identifier (ignore this in output)
- `fromFlag`: flag emoji
- `fromAmount`: source amount string
- `fromCode`: source currency code
- `toFlag`: flag emoji
- `toAmount`: converted amount string
- `toCode`: target currency code
- `rate`: exchange rate string
- `date`: rate date string
- `offline`: boolean

Fill this template with ONLY the values from the LATEST response:

{fromFlag} {fromAmount} {fromCode} → {toFlag} {toAmount} {toCode}
📊 1 {fromCode} = {rate} {toCode}
📅 {date}

If `offline` is true, append:
⚠️ Offline — cached rates from {date}

RULES:
- ONLY use values from the LATEST `run_js` response. NEVER reuse numbers from earlier messages.
- Output ONLY the filled template. Nothing before, nothing after.
- Do NOT modify, round, truncate, or reformat any value. Copy each field exactly.
- Do NOT add greetings, commentary, follow-up questions, or markdown formatting.
- If the response has an `error` field, show only: ❌ {error}
