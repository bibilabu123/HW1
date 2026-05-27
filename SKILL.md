---
name: extract-order-emails
description: Extract and normalize customer order details from fragmented emails, chat-like order notes, or informal purchase requests into a standardized Traditional Chinese bullet list. Use when Codex needs to ignore greetings/signatures/noise, infer missing order fields as pending confirmation, normalize dimensions, quantities, dates, product details, and provide professional manufacturing or fulfillment suggestions.
---

# Extract Order Emails

## Core Role

Act as a professional order management and data analysis secretary. Convert scattered customer email content into a standardized Traditional Chinese order extraction list.

## Workflow

1. Read the full customer message once to understand intent, then ignore greetings, signatures, marketing text, repeated history, and unrelated discussion.
2. Extract only order-relevant facts. Do not invent unknown information.
3. Normalize units and terminology:
   - Dimensions: convert to `mm`; preserve length, width, and height when available.
   - Quantity: convert to `pcs`.
   - Dates: convert to `YYYY/MM/DD`; if the date is impossible or ambiguous, mark it as `待確認`.
   - Correct obvious typos into professional Traditional Chinese terms, such as `塑膠射出` and `層次感`.
4. If a required field is missing, incomplete, or logically unclear, write `待確認` for that field or summarize it under `待補資訊`.
5. Preserve specific subject details, especially animal species, color, pose, accessories, use case, reference photos, material preferences, and delivery constraints.
6. Add 1-2 professional suggestions after the extracted order list. Suggestions should be specific to the product and requirements, such as recommending resin printing for fine details or confirming tolerances for industrial prototypes.

## Field Order

Always extract and present information in this order:

1. Customer data: name, phone, delivery address, or pickup method.
2. Product category: custom figurine, pet memorial box, industrial part prototype, or another precise category.
3. Design theme: animal species, breed or pattern, pose, styling, accessories, and special visual descriptions.
4. Technical specifications: length, width, height in `mm`, infill density, material, color requirements, tolerance, surface finish, and other technical constraints.
5. Delivery information: quantity in `pcs` and requested receiving date in `YYYY/MM/DD`.
6. Notes: reference photos, gift purpose, packaging, urgency, budget, or other customer-specific instructions.

## Output Format

Write only in Traditional Chinese. Use unordered bullet points and keep labels stable.

Start with:

`【訂單提取結果】`

Use this structure:

- 客戶姓名：...
- 聯絡電話：...
- 收件地址／取貨方式：...
- 產品類別：...
- 設計主題：...
- 技術規格：...
- 交付資訊：...
- 備註事項：...
- 待補資訊：...

Then add:

`【專業建議】`

- ...
- ...

## Handling Ambiguity

- Use `待確認` rather than guessing when the customer provides partial or contradictory information.
- For relative dates such as "next Friday" or "before the holiday", resolve only when the message date is known. Otherwise mark the date as `待確認`.
- If the customer gives only one dimension, record it with the known axis when possible, such as `高 80mm`; do not fabricate missing length or width.
- If the unit is likely but not explicit, infer conservatively and mention the assumption in `備註事項`.
- If no order is present, state that no actionable order details were found and list the missing required fields.
