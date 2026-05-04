# WhatsApp Notification Catalog (Sagenex)


## Quick examples (non-technical)

The table below shows example messages with real values filled in. These are examples only and can be customized.

| Category | Notification | Example message |
| --- | --- | --- |
| Account | Welcome | Welcome to Sagenex, Amit Sharma (U042). Your account is ready. |
| Auth | Email verification OTP | Your Sagenex verification code is 381204. It expires in 10 minutes. |
| Auth | Login OTP | Your Sagenex login code is 904117. It expires in 10 minutes. |
| Wallet | Transfer OTP | Transfer code: 552091. Do not share this code with anyone. |
| KYC | KYC submitted | We received your KYC documents on 2026-05-05 10:30 IST. Status: PENDING. |
| KYC | KYC approved | Your KYC is VERIFIED. Thank you, Amit. |
| KYC | KYC rejected | Your KYC is REJECTED. Reason: PAN image not clear. Please resubmit. |
| Wallet | Deposit status | Deposit of USD 250.00 is CONFIRMED. Txn ID: DPT-93841. |
| Wallet | Withdrawal status | Withdrawal of INR 25,000 is PROCESSING. Ref: WD-1183. |
| Wallet | Transfer sent | You sent USD 100.00 to Riya Kapoor (U389). Txn ID: TR-22091. |
| Wallet | Transfer received | You received USD 100.00 from Amit Sharma (U042). Txn ID: TR-22091. |
| Earnings | ROI payout | ROI credited: USD 18.25 for cycle Apr 2026. New balance: USD 410.60. |
| Earnings | Bonus credited | Direct bonus credited: USD 12.00. New balance: USD 422.60. |
| Earnings | Bonus unlocked | Unilevel L3 bonus is now unlocked. Locked amount USD 50.00 is released. |
| Rank | Rank upgrade | Congrats. You are now Builder Plus (was Builder). |
| Team | New referral | New referral joined: Priya Singh (U512). Sponsor: Amit Sharma. |
| Team | Placement update | New team member placed under you on Left. Member: U512. |
| SGChain | Transfer status | SGChain transfer INITIATED. Code: SG-9R2K1. Amount: USD 75.00. |
| SGBN | Coupon status | SGBN coupon created: SGBN-7F21. Amount: USD 200.00. Expires: 2026-06-01. |
| LP | Liquidity pool | LP deposit of USD 500.00 is CONFIRMED. Request ID: LP-4021. |
| SGGOLD | Autopay status | SGGOLD autopay SUCCESS. Amount: USD 40.00. Due date: 2026-05-10. |
| SGNXGOLD | Autopay status | SGNXGOLD autopay FAILED. Reason: insufficient balance. |
| Lottery | Ticket purchased | Lottery ticket purchased. Ticket ID: LT-1120. Draw: 2026-05-31. |
| Lottery | Result | Lottery result: WIN. Prize: USD 100. Ticket ID: LT-1120. |
| Support | Ticket update | Support ticket ST-9012 is RESOLVED. We have emailed the details. |
| System | Maintenance notice | Scheduled maintenance on 2026-05-07 01:00-02:00 UTC. Some features may be unavailable. |

## Naming and variable rules

- Template keys are snake_case and stable. Example: `wallet_withdrawal_status`.
- Variable placeholders use double braces in this document, e.g., `{{user_full_name}}`.
- WhatsApp templates use numbered placeholders (e.g., `{{1}}`, `{{2}}`). Map the named variables to numbers in code.
- All amounts should be formatted with currency (USD, INR, USDT).
- All dates should include timezone (example: 2026-05-05 10:30 IST).

## Variable glossary (common)

These variables are used across many templates.

| Variable | Meaning | Example value |
| --- | --- | --- |
| {{company_name}} | Brand name | Sagenex |
| {{user_full_name}} | User full name | Amit Sharma |
| {{user_first_name}} | First name | Amit |
| {{user_id}} | User ID | U042 |
| {{support_email}} | Support email | support@sagenex.ai |
| {{support_phone}} | Support phone | +91-90000-00000 |
| {{support_whatsapp}} | Support WhatsApp | +91-90000-00000 |
| {{date_time}} | Date and time with timezone | 2026-05-05 10:30 IST |
| {{amount}} | Money amount with currency | USD 250.00 |
| {{balance}} | Current balance | USD 410.60 |
| {{status}} | Current status | CONFIRMED |
| {{reason}} | Reason text | PAN image not clear |
| {{transaction_id}} | Transaction reference | TR-22091 |
| {{action_url}} | Link to app or web | https://app.sagenex.ai |

## Notification catalog (detailed)

### Account: welcome

- Template key: `account_welcome`
- Category: Utility
- Audience: User
- Trigger: User registration completed.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{user_full_name}} | User full name | Amit Sharma |
| {{user_id}} | User ID | U042 |
| {{action_url}} | App link | https://app.sagenex.ai |

Example message:
Welcome to {{company_name}}, {{user_full_name}} ({{user_id}}). Your account is ready. Open: {{action_url}}

### Auth: email verification OTP

- Template key: `auth_otp_email_verification`
- Category: Authentication
- Audience: User
- Trigger: Email verification OTP requested.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{otp_code}} | One-time code | 381204 |
| {{otp_expires_in_minutes}} | Expiry minutes | 10 |

Example message:
Your {{company_name}} verification code is {{otp_code}}. It expires in {{otp_expires_in_minutes}} minutes.

### Auth: login OTP

- Template key: `auth_otp_login`
- Category: Authentication
- Audience: User
- Trigger: Login OTP requested.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{otp_code}} | One-time code | 904117 |
| {{otp_expires_in_minutes}} | Expiry minutes | 10 |

Example message:
Your {{company_name}} login code is {{otp_code}}. It expires in {{otp_expires_in_minutes}} minutes.

### Wallet: transfer OTP

- Template key: `wallet_otp_transfer`
- Category: Authentication
- Audience: User
- Trigger: Transfer OTP requested.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{otp_code}} | One-time code | 552091 |
| {{otp_expires_in_minutes}} | Expiry minutes | 10 |

Example message:
Transfer code: {{otp_code}}. This code expires in {{otp_expires_in_minutes}} minutes. Do not share it.

### Security: new login alert

- Template key: `security_new_login`
- Category: Utility
- Audience: User
- Trigger: Successful login from a device or IP.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{user_first_name}} | First name | Amit |
| {{date_time}} | Login time | 2026-05-05 10:30 IST |
| {{location}} | Approx location | Bengaluru, IN |
| {{device}} | Device name | iPhone 14 |

Example message:
Hi {{user_first_name}}, new login on {{date_time}} from {{location}} using {{device}}. If this was not you, contact support.

### Account: status update (blocked or unblocked)

- Template key: `account_status_update`
- Category: Utility
- Audience: User
- Trigger: Account blocked or unblocked.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{status}} | BLOCKED or UNBLOCKED | BLOCKED |
| {{reason}} | Reason | KYC verification pending |
| {{support_email}} | Support email | support@sagenex.ai |

Example message:
Your account status is {{status}}. Reason: {{reason}}. Need help? {{support_email}}

### Profile: updated

- Template key: `profile_updated`
- Category: Utility
- Audience: User
- Trigger: Profile updated (email/phone/name).

| Variable | Meaning | Example |
| --- | --- | --- |
| {{user_first_name}} | First name | Amit |
| {{date_time}} | Update time | 2026-05-05 10:40 IST |

Example message:
Hi {{user_first_name}}, your profile was updated on {{date_time}}. If you did not do this, contact support.

### Nominee: status update

- Template key: `nominee_status_update`
- Category: Utility
- Audience: User
- Trigger: Nominee access enabled, reset, or disabled.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{status}} | ENABLED, RESET, DISABLED | ENABLED |
| {{date_time}} | Change time | 2026-05-05 11:10 IST |
| {{phrase_hint}} | Hint shown to user | 7Q9Z |

Example message:
Nominee access {{status}} on {{date_time}}. Hint: {{phrase_hint}}.

### KYC: status update

- Template key: `kyc_status_update`
- Category: Utility
- Audience: User
- Trigger: KYC status changed or submitted.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{status}} | NOT_SUBMITTED, PENDING, VERIFIED, REJECTED | PENDING |
| {{reason}} | Rejection reason (if any) | PAN image not clear |
| {{date_time}} | Change time | 2026-05-05 10:30 IST |
| {{action_url}} | KYC page | https://app.sagenex.ai/kyc |

Example message:
KYC status: {{status}} on {{date_time}}. {{reason}}. Continue here: {{action_url}}

### Wallet: deposit status (crypto)

- Template key: `wallet_deposit_status`
- Category: Utility
- Audience: User
- Trigger: Crypto deposit created or updated.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{status}} | CREATED, CONFIRMED, FAILED, REFUNDED, EXPIRED | CONFIRMED |
| {{amount}} | Deposit amount | USD 250.00 |
| {{transaction_id}} | Deposit reference | DPT-93841 |
| {{date_time}} | Status time | 2026-05-05 12:05 IST |

Example message:
Deposit {{status}}. Amount: {{amount}}. Ref: {{transaction_id}}. Time: {{date_time}}.

### Wallet: withdrawal status

- Template key: `wallet_withdrawal_status`
- Category: Utility
- Audience: User
- Trigger: Withdrawal requested or status updated.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{status}} | REQUESTED, PROCESSING, PAID, REJECTED, CANCELED | PROCESSING |
| {{amount}} | Withdrawal amount | INR 25,000 |
| {{transaction_id}} | Withdrawal reference | WD-1183 |
| {{date_time}} | Status time | 2026-05-05 12:15 IST |
| {{reason}} | Rejection reason | Bank details invalid |

Example message:
Withdrawal {{status}}. Amount: {{amount}}. Ref: {{transaction_id}}. {{reason}}

### Wallet: transfer status (sent)

- Template key: `wallet_transfer_status`
- Category: Utility
- Audience: User
- Trigger: Transfer sent or status updated for sender.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{status}} | SENT, FAILED, REVERSED | SENT |
| {{amount}} | Transfer amount | USD 100.00 |
| {{transaction_id}} | Transfer reference | TR-22091 |
| {{recipient_name}} | Recipient name | Riya Kapoor |
| {{recipient_id}} | Recipient ID | U389 |
| {{date_time}} | Status time | 2026-05-05 12:20 IST |

Example message:
Transfer {{status}} to {{recipient_name}} ({{recipient_id}}). Amount: {{amount}}. Ref: {{transaction_id}}.

### Wallet: transfer received

- Template key: `wallet_transfer_received`
- Category: Utility
- Audience: User
- Trigger: Transfer received by recipient.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{amount}} | Transfer amount | USD 100.00 |
| {{transaction_id}} | Transfer reference | TR-22091 |
| {{sender_name}} | Sender name | Amit Sharma |
| {{sender_id}} | Sender ID | U042 |
| {{date_time}} | Received time | 2026-05-05 12:20 IST |

Example message:
You received {{amount}} from {{sender_name}} ({{sender_id}}). Ref: {{transaction_id}}.

### Wallet: balance or cap alert

- Template key: `wallet_cap_alert`
- Category: Utility
- Audience: User
- Trigger: Earnings cap or withdrawal cap reached.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{cap_type}} | EARNINGS_CAP or WITHDRAWAL_CAP | EARNINGS_CAP |
| {{amount}} | Cap amount | USD 2,500.00 |
| {{date_time}} | Alert time | 2026-05-05 12:30 IST |

Example message:
Alert: {{cap_type}} reached ({{amount}}) on {{date_time}}.

### Earnings: ROI payout credited

- Template key: `roi_payout_credited`
- Category: Utility
- Audience: User
- Trigger: ROI payout job credits wallet.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{amount}} | ROI amount | USD 18.25 |
| {{cycle_label}} | Payout cycle | Apr 2026 |
| {{balance}} | New balance | USD 410.60 |
| {{date_time}} | Credit time | 2026-05-05 01:00 IST |

Example message:
ROI credited: {{amount}} for {{cycle_label}}. New balance: {{balance}}.

### Earnings: bonus credited

- Template key: `bonus_credited`
- Category: Utility
- Audience: User
- Trigger: Bonus credit applied.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{bonus_type}} | DIRECT, UNILEVEL, REINVESTMENT | DIRECT |
| {{amount}} | Bonus amount | USD 12.00 |
| {{balance}} | New balance | USD 422.60 |
| {{date_time}} | Credit time | 2026-05-05 12:45 IST |

Example message:
{{bonus_type}} bonus credited: {{amount}}. New balance: {{balance}}.

### Earnings: bonus level unlocked

- Template key: `bonus_level_unlocked`
- Category: Utility
- Audience: User
- Trigger: Locked bonus level becomes unlocked.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{bonus_level}} | Bonus level | L3 |
| {{amount}} | Released amount | USD 50.00 |
| {{date_time}} | Unlock time | 2026-05-05 13:10 IST |

Example message:
Unilevel {{bonus_level}} unlocked. Released: {{amount}}.

### Rank: upgrade

- Template key: `rank_upgrade`
- Category: Utility
- Audience: User
- Trigger: Rank changes upward.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{rank_previous}} | Old rank | Builder |
| {{rank_new}} | New rank | Builder Plus |
| {{date_time}} | Change time | 2026-05-05 02:30 IST |

Example message:
Congrats. You are now {{rank_new}} (was {{rank_previous}}).

### Team: new referral joined

- Template key: `referral_joined`
- Category: Utility
- Audience: User
- Trigger: New user joins with you as sponsor.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{referral_name}} | Referral name | Priya Singh |
| {{referral_id}} | Referral ID | U512 |
| {{date_time}} | Join time | 2026-05-05 13:20 IST |

Example message:
New referral joined: {{referral_name}} ({{referral_id}}).

### Team: placement update

- Template key: `placement_update`
- Category: Utility
- Audience: User
- Trigger: New team member placed under user.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{placed_user_name}} | Placed user name | Priya Singh |
| {{placed_user_id}} | Placed user ID | U512 |
| {{placement_side}} | Left or Right | Left |
| {{date_time}} | Placement time | 2026-05-05 13:22 IST |

Example message:
New team placement on {{placement_side}}: {{placed_user_name}} ({{placed_user_id}}).

### Team: milestone

- Template key: `team_milestone`
- Category: Utility
- Audience: User
- Trigger: Team milestone reached (active legs, depth, or volume).

| Variable | Meaning | Example |
| --- | --- | --- |
| {{milestone_name}} | Milestone name | 10 Active Legs |
| {{milestone_value}} | Value | 10 |
| {{date_time}} | Milestone time | 2026-05-05 13:30 IST |

Example message:
Milestone reached: {{milestone_name}} ({{milestone_value}}).

### SGChain: transfer status

- Template key: `sgchain_transfer_status`
- Category: Utility
- Audience: User
- Trigger: Transfer to or from SGChain updated.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{status}} | INITIATED, REDEEMED, FAILED | INITIATED |
| {{amount}} | Transfer amount | USD 75.00 |
| {{sgchain_code}} | Transfer code | SG-9R2K1 |
| {{transaction_id}} | Reference | SG-4412 |
| {{date_time}} | Status time | 2026-05-05 13:40 IST |

Example message:
SGChain transfer {{status}}. Amount: {{amount}}. Code: {{sgchain_code}}.

### SGBN: coupon status

- Template key: `sgbn_coupon_status`
- Category: Utility
- Audience: User
- Trigger: SGBN coupon created, redeemed, or expired.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{status}} | CREATED, REDEEMED, EXPIRED | CREATED |
| {{amount}} | Coupon amount | USD 200.00 |
| {{coupon_code}} | Coupon code | SGBN-7F21 |
| {{expiry_date}} | Expiry date | 2026-06-01 |

Example message:
SGBN coupon {{status}}. Code: {{coupon_code}}. Amount: {{amount}}. Expires: {{expiry_date}}.

### SGGOLD: autopay status

- Template key: `sggold_autopay_status`
- Category: Utility
- Audience: User
- Trigger: SGGOLD autopay run.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{status}} | SUCCESS, FAILED | SUCCESS |
| {{amount}} | Payment amount | USD 40.00 |
| {{due_date}} | Due date | 2026-05-10 |
| {{reason}} | Failure reason | Insufficient balance |

Example message:
SGGOLD autopay {{status}}. Amount: {{amount}}. Due: {{due_date}}. {{reason}}

### SGNXGOLD: autopay status

- Template key: `sgnxgold_autopay_status`
- Category: Utility
- Audience: User
- Trigger: SGNXGOLD autopay run.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{status}} | SUCCESS, FAILED | FAILED |
| {{amount}} | Payment amount | USD 25.00 |
| {{reason}} | Failure reason | Insufficient balance |
| {{date_time}} | Run time | 2026-05-05 01:05 IST |

Example message:
SGNXGOLD autopay {{status}}. Amount: {{amount}}. {{reason}}

### LP: liquidity pool status

- Template key: `lp_pool_status`
- Category: Utility
- Audience: User
- Trigger: LP deposit or withdrawal request and updates.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{status}} | DEPOSIT_CONFIRMED, WITHDRAWAL_REQUESTED, WITHDRAWAL_PROCESSED, EARLY_WITHDRAWAL_REQUESTED, EARLY_WITHDRAWAL_APPROVED, EARLY_WITHDRAWAL_DENIED | WITHDRAWAL_REQUESTED |
| {{amount}} | Amount | USD 500.00 |
| {{request_id}} | Request ID | LP-4021 |
| {{date_time}} | Status time | 2026-05-05 14:10 IST |
| {{reason}} | Denial reason | Yield in progress |

Example message:
LP status: {{status}}. Amount: {{amount}}. Request: {{request_id}}.

### Courses: status

- Template key: `course_status`
- Category: Utility
- Audience: User
- Trigger: Course enrollment or completion.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{status}} | ENROLLED, COMPLETED | ENROLLED |
| {{course_title}} | Course name | Sagenex Basics |
| {{course_id}} | Course ID | CR-110 |
| {{date_time}} | Status time | 2026-05-05 14:20 IST |

Example message:
Course {{status}}: {{course_title}} ({{course_id}}).

### Lottery: OTP for purchase

- Template key: `lottery_otp_purchase`
- Category: Authentication
- Audience: User
- Trigger: Lottery ticket OTP requested.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{otp_code}} | One-time code | 231990 |
| {{otp_expires_in_minutes}} | Expiry minutes | 10 |

Example message:
Lottery OTP: {{otp_code}}. Expires in {{otp_expires_in_minutes}} minutes.

### Lottery: ticket purchased

- Template key: `lottery_ticket_purchased`
- Category: Utility
- Audience: User
- Trigger: Lottery ticket purchased.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{ticket_id}} | Ticket ID | LT-1120 |
| {{draw_date}} | Draw date | 2026-05-31 |
| {{amount}} | Ticket amount | USD 5.00 |

Example message:
Lottery ticket purchased. Ticket: {{ticket_id}}. Draw: {{draw_date}}.

### Lottery: result

- Template key: `lottery_result`
- Category: Utility
- Audience: User
- Trigger: Lottery draw result.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{result}} | WIN or LOSE | WIN |
| {{prize_amount}} | Prize amount | USD 100.00 |
| {{ticket_id}} | Ticket ID | LT-1120 |
| {{draw_date}} | Draw date | 2026-05-31 |

Example message:
Lottery result: {{result}}. Prize: {{prize_amount}}. Ticket: {{ticket_id}}.

### Tests: booking OTP

- Template key: `test_booking_otp`
- Category: Authentication
- Audience: User
- Trigger: Test booking OTP requested.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{otp_code}} | One-time code | 778421 |
| {{otp_expires_in_minutes}} | Expiry minutes | 10 |
| {{test_type}} | Test type | Health Screening |
| {{amount}} | Booking amount | USD 15.00 |

Example message:
Test booking OTP: {{otp_code}} for {{test_type}}. Amount: {{amount}}. Expires in {{otp_expires_in_minutes}} minutes.

### Tickets: status update

- Template key: `tickets_status_update`
- Category: Utility
- Audience: User
- Trigger: Ticket balance or purchase update.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{ticket_count}} | Total tickets | 12 |
| {{amount}} | Related amount | USD 20.00 |
| {{date_time}} | Update time | 2026-05-05 15:00 IST |

Example message:
Tickets updated. Total: {{ticket_count}}. Amount: {{amount}}.

### Rewards: claim status

- Template key: `rewards_claim_status`
- Category: Utility
- Audience: User
- Trigger: Reward claim submitted or updated.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{status}} | SUBMITTED, APPROVED, REJECTED, SHIPPED | APPROVED |
| {{reward_name}} | Reward name | Europe Trip |
| {{date_time}} | Status time | 2026-05-05 15:10 IST |
| {{reason}} | Rejection reason | Eligibility not met |

Example message:
Reward {{reward_name}} claim {{status}}. {{reason}}

### Support: ticket status

- Template key: `support_ticket_status`
- Category: Utility
- Audience: User
- Trigger: Support ticket created or updated.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{ticket_id}} | Ticket ID | ST-9012 |
| {{status}} | OPEN, IN_PROGRESS, RESOLVED, CLOSED | RESOLVED |
| {{date_time}} | Update time | 2026-05-05 15:15 IST |
| {{action_url}} | Ticket link | https://app.sagenex.ai/support |

Example message:
Support ticket {{ticket_id}} is {{status}}. Details: {{action_url}}

### System: announcement

- Template key: `system_announcement`
- Category: Utility
- Audience: User
- Trigger: Admin announcement or update banner.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{title}} | Announcement title | New ROI Rules |
| {{message}} | Announcement text | ROI rules updated for May 2026. |
| {{action_url}} | Link | https://app.sagenex.ai/updates |

Example message:
{{title}}: {{message}} Learn more: {{action_url}}

### System: maintenance notice

- Template key: `system_maintenance_notice`
- Category: Utility
- Audience: User
- Trigger: Scheduled maintenance.

| Variable | Meaning | Example |
| --- | --- | --- |
| {{start_time}} | Start time | 2026-05-07 01:00 UTC |
| {{end_time}} | End time | 2026-05-07 02:00 UTC |
| {{impact}} | Impact text | Some features may be unavailable |

Example message:
Scheduled maintenance {{start_time}} to {{end_time}}. {{impact}}.

## WhatsApp placeholder mapping (implementation note)

WhatsApp templates use numbered placeholders like {{1}}, {{2}}. Your backend can map named variables to numbers. Example mapping for `auth_otp_login`:

- {{1}} -> otp_code
- {{2}} -> otp_expires_in_minutes

Repeat this mapping inside the code or template registry for each template key.
