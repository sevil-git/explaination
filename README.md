# WhatsApp Notification Catalog (Sagenex)

## Global Variables (available for all templates)
- {{app_name}}: "Sagenex"
- {{support_email}}: Support email address
- {{support_phone}}: Support phone number (if available)
- {{support_whatsapp}}: Support WhatsApp number (if available)
- {{portal_url}}: Main app URL
- {{help_center_url}}: Help/FAQ URL
- {{timestamp}}: ISO timestamp of the event
- {{timezone}}: User timezone (if known)

## User Identity Variables
- {{user_id}}
- {{full_name}}
- {{first_name}}
- {{email}}
- {{phone_e164}}
- {{country}}
- {{language}}

## Security and Authentication

### 1) auth_email_otp
- Category: AUTHENTICATION
- Audience: User
- Description: Email verification OTP (also used for login OTP)
- Trigger: OTP generated for email verification or login
- Variables:
  - {{otp_code}}
  - {{otp_valid_minutes}}
  - {{requested_for}} ("signup", "login")
  - {{email}}
- Sample:
  "Your Sagenex verification code is {{otp_code}}. It expires in {{otp_valid_minutes}} minutes."

### 2) auth_password_changed
- Category: UTILITY
- Audience: User
- Description: Password set or changed
- Trigger: User sets or changes password
- Variables:
  - {{full_name}}
  - {{change_method}} ("self", "admin", "reset")
  - {{timestamp}}
- Sample:
  "Your Sagenex password was updated on {{timestamp}}. If this was not you, contact support."

### 3) auth_account_blocked
- Category: UTILITY
- Audience: User
- Description: Account blocked
- Trigger: Admin blocks user
- Variables:
  - {{full_name}}
  - {{blocked_reason}}
  - {{support_email}}
- Sample:
  "Your account was blocked. Reason: {{blocked_reason}}. Contact {{support_email}}."

### 4) auth_account_unblocked
- Category: UTILITY
- Audience: User
- Description: Account unblocked
- Trigger: Admin unblocks user
- Variables:
  - {{full_name}}
  - {{timestamp}}
- Sample:
  "Your account access was restored on {{timestamp}}."

### 5) auth_impersonation_started
- Category: UTILITY
- Audience: User
- Description: Admin starts impersonation
- Trigger: Admin login assist begins
- Variables:
  - {{admin_id}}
  - {{timestamp}}
- Sample:
  "An admin accessed your account for support on {{timestamp}} (Admin ID: {{admin_id}})."

### 6) auth_impersonation_stopped
- Category: UTILITY
- Audience: User
- Description: Admin stops impersonation
- Trigger: Admin stops impersonation
- Variables:
  - {{admin_id}}
  - {{timestamp}}

## KYC

### 7) kyc_submitted
- Category: UTILITY
- Audience: User
- Description: KYC submitted for review
- Trigger: KYC submit for review
- Variables:
  - {{full_name}}
  - {{kyc_status}} ("PENDING")
  - {{timestamp}}

### 8) kyc_verified
- Category: UTILITY
- Audience: User
- Description: KYC approved
- Trigger: KYC verified
- Variables:
  - {{full_name}}
  - {{verified_at}}

### 9) kyc_rejected
- Category: UTILITY
- Audience: User
- Description: KYC rejected
- Trigger: KYC rejected
- Variables:
  - {{full_name}}
  - {{rejection_reason}}
  - {{resubmit_url}}

## Referrals and Team (Tree)

### 10) referral_direct_joined
- Category: UTILITY
- Audience: Sponsor (parent)
- Description: A new direct referral joined under the sponsor
- Trigger: New user registration linked to sponsor
- Variables:
  - {{sponsor_name}}
  - {{new_member_name}}
  - {{new_member_user_id}}
  - {{join_date}}

### 11) referral_placed_in_team
- Category: UTILITY
- Audience: Sponsor or upline
- Description: A new user was placed in the downline (if placement logic exists)
- Trigger: Placement action
- Variables:
  - {{sponsor_name}}
  - {{new_member_name}}
  - {{placement_position}}
  - {{level_depth}}

### 12) referral_nominee_login
- Category: UTILITY
- Audience: User
- Description: Nominee access used
- Trigger: Nominee login
- Variables:
  - {{timestamp}}
  - {{ip_address}}

## Rank, Multiplier, and Bonuses

### 13) rank_upgraded
- Category: UTILITY
- Audience: User
- Description: Rank or multiplier upgraded (builder -> higher level)
- Trigger: Rank update or promotion job
- Variables:
  - {{full_name}}
  - {{old_rank}}
  - {{new_rank}}
  - {{achieved_at}}
  - {{earnings_multiplier}}

### 14) rank_downgraded
- Category: UTILITY
- Audience: User
- Description: Rank downgraded (if applicable)
- Trigger: Rank update job
- Variables:
  - {{full_name}}
  - {{old_rank}}
  - {{new_rank}}
  - {{reason}}

### 15) bonus_unlocked
- Category: UTILITY
- Audience: User
- Description: Unilevel or direct bonus unlocked
- Trigger: Bonus unlock logic
- Variables:
  - {{bonus_name}}
  - {{bonus_level}}
  - {{amount}}
  - {{timestamp}}

### 16) bonus_credited
- Category: UTILITY
- Audience: User
- Description: Bonus credited to wallet
- Trigger: Bonus posting
- Variables:
  - {{bonus_type}} ("direct", "unilevel", "reinvestment")
  - {{amount}}
  - {{wallet_balance}}

### 17) roi_payout_processed
- Category: UTILITY
- Audience: User
- Description: ROI payout processed
- Trigger: ROI payout job
- Variables:
  - {{amount}}
  - {{payout_date}}
  - {{wallet_balance}}

### 18) earnings_cap_near
- Category: UTILITY
- Audience: User
- Description: Earnings cap near limit (threshold based)
- Trigger: Post-earnings check
- Variables:
  - {{cap_total}}
  - {{cap_remaining}}
  - {{threshold_percent}}

### 19) earnings_cap_reached
- Category: UTILITY
- Audience: User
- Description: Earnings cap reached
- Trigger: Post-earnings check
- Variables:
  - {{cap_total}}
  - {{earned_total}}

## Wallet, Deposits, and Withdrawals

### 20) deposit_invoice_created
- Category: UTILITY
- Audience: User
- Description: Crypto deposit invoice created
- Trigger: Create crypto deposit invoice
- Variables:
  - {{amount}}
  - {{currency}}
  - {{invoice_id}}
  - {{payment_address}}
  - {{expires_at}}

### 21) deposit_confirmed
- Category: UTILITY
- Audience: User
- Description: Deposit confirmed
- Trigger: Deposit webhook confirms
- Variables:
  - {{amount}}
  - {{currency}}
  - {{tx_id}}
  - {{wallet_balance}}

### 22) deposit_failed
- Category: UTILITY
- Audience: User
- Description: Deposit failed or expired
- Trigger: Deposit webhook status failed/refunded/expired
- Variables:
  - {{amount}}
  - {{currency}}
  - {{reason}}

### 23) withdrawal_requested
- Category: UTILITY
- Audience: User
- Description: Withdrawal request submitted
- Trigger: Withdrawal request created
- Variables:
  - {{amount}}
  - {{method}} ("crypto", "bank", "upi")
  - {{request_id}}
  - {{timestamp}}

### 24) withdrawal_approved
- Category: UTILITY
- Audience: User
- Description: Withdrawal approved by admin
- Trigger: Admin approval
- Variables:
  - {{amount}}
  - {{method}}
  - {{approved_at}}

### 25) withdrawal_paid
- Category: UTILITY
- Audience: User
- Description: Withdrawal paid out
- Trigger: Payout processed
- Variables:
  - {{amount}}
  - {{method}}
  - {{tx_id}}
  - {{paid_at}}

### 26) withdrawal_rejected
- Category: UTILITY
- Audience: User
- Description: Withdrawal rejected
- Trigger: Admin rejection
- Variables:
  - {{amount}}
  - {{reason}}
  - {{support_email}}

### 27) transfer_sent
- Category: UTILITY
- Audience: Sender
- Description: User-to-user transfer sent
- Trigger: Transfer execution success
- Variables:
  - {{amount}}
  - {{recipient_id}}
  - {{recipient_name}}
  - {{transaction_id}}

### 28) transfer_received
- Category: UTILITY
- Audience: Recipient
- Description: User-to-user transfer received
- Trigger: Transfer execution success
- Variables:
  - {{amount}}
  - {{sender_id}}
  - {{sender_name}}
  - {{transaction_id}}

### 29) transfer_failed
- Category: UTILITY
- Audience: Sender
- Description: Transfer failed
- Trigger: Transfer execution failed
- Variables:
  - {{amount}}
  - {{recipient_id}}
  - {{reason}}

### 30) wallet_low_balance
- Category: UTILITY
- Audience: User
- Description: Balance below threshold
- Trigger: Periodic check
- Variables:
  - {{available_balance}}
  - {{threshold}}

### 31) wallet_credit
- Category: UTILITY
- Audience: User
- Description: Any wallet credit
- Trigger: Ledger credit posted
- Variables:
  - {{amount}}
  - {{source}}
  - {{wallet_balance}}

### 32) wallet_debit
- Category: UTILITY
- Audience: User
- Description: Any wallet debit
- Trigger: Ledger debit posted
- Variables:
  - {{amount}}
  - {{reason}}
  - {{wallet_balance}}

## Package and Plan Events

### 33) package_activated
- Category: UTILITY
- Audience: User
- Description: Package activated
- Trigger: Package activation
- Variables:
  - {{package_usd}}
  - {{activation_date}}
  - {{earnings_multiplier}}

### 34) package_upgraded
- Category: UTILITY
- Audience: User
- Description: Package upgraded
- Trigger: Package upgrade
- Variables:
  - {{old_package_usd}}
  - {{new_package_usd}}
  - {{upgrade_date}}

### 35) package_deactivated
- Category: UTILITY
- Audience: User
- Description: Package deactivated/inactive
- Trigger: Package deactivation
- Variables:
  - {{reason}}
  - {{effective_date}}

### 36) compounding_toggled
- Category: UTILITY
- Audience: User
- Description: Compounding toggled
- Trigger: Compounding toggle
- Variables:
  - {{compounding_enabled}}
  - {{timestamp}}

## SGChain / SGBN / SGGOLD / SGNX Gold

### 37) sgchain_transfer_initiated
- Category: UTILITY
- Audience: User
- Description: Transfer to SGChain initiated
- Trigger: SGChain transfer initiation
- Variables:
  - {{amount}}
  - {{transfer_code}}
  - {{expires_at}}

### 38) sgchain_transfer_redeemed
- Category: UTILITY
- Audience: User
- Description: Transfer from SGChain redeemed
- Trigger: SGChain redeem
- Variables:
  - {{amount}}
  - {{wallet_balance}}

### 39) sgbn_coupon_created
- Category: UTILITY
- Audience: User
- Description: SGBN coupon generated
- Trigger: SGBN coupon creation
- Variables:
  - {{amount}}
  - {{coupon_code}}
  - {{expires_at}}

### 40) sgbn_coupon_expired
- Category: UTILITY
- Audience: User
- Description: SGBN coupon expired
- Trigger: Coupon expiry job
- Variables:
  - {{coupon_code}}
  - {{expired_at}}

### 41) sggold_autopay_success
- Category: UTILITY
- Audience: User
- Description: SGGOLD autopay success
- Trigger: Autopay job
- Variables:
  - {{amount}}
  - {{paid_at}}

### 42) sggold_autopay_failed
- Category: UTILITY
- Audience: User
- Description: SGGOLD autopay failed
- Trigger: Autopay job
- Variables:
  - {{amount}}
  - {{reason}}

### 43) sgnxgold_autopay_success
- Category: UTILITY
- Audience: User
- Description: SGNX Gold autopay success
- Trigger: Autopay job
- Variables:
  - {{amount}}
  - {{paid_at}}

### 44) sgnxgold_autopay_failed
- Category: UTILITY
- Audience: User
- Description: SGNX Gold autopay failed
- Trigger: Autopay job
- Variables:
  - {{amount}}
  - {{reason}}

## Liquidity Pool (LP)

### 45) lp_deposit_created
- Category: UTILITY
- Audience: User
- Description: LP deposit created
- Trigger: LP deposit
- Variables:
  - {{amount}}
  - {{tx_id}}

### 46) lp_withdrawal_requested
- Category: UTILITY
- Audience: User
- Description: LP withdrawal requested
- Trigger: LP withdrawal request
- Variables:
  - {{amount}}
  - {{request_id}}

### 47) lp_withdrawal_processed
- Category: UTILITY
- Audience: User
- Description: LP withdrawal processed
- Trigger: LP withdrawal processed
- Variables:
  - {{amount}}
  - {{tx_id}}

## Lottery and Tests

### 48) lottery_ticket_purchased
- Category: UTILITY
- Audience: User
- Description: Lottery ticket purchased
- Trigger: Ticket purchase
- Variables:
  - {{ticket_count}}
  - {{amount}}
  - {{draw_date}}

### 49) lottery_result
- Category: UTILITY
- Audience: User
- Description: Lottery result
- Trigger: Draw processing
- Variables:
  - {{result}}
  - {{prize_amount}}

### 50) test_booking_otp
- Category: AUTHENTICATION
- Audience: User
- Description: Test booking OTP
- Trigger: Test booking OTP send
- Variables:
  - {{otp_code}}
  - {{test_type}}
  - {{amount}}

## Courses

### 51) course_enrolled
- Category: UTILITY
- Audience: User
- Description: Enrolled in a course
- Trigger: Course enrollment
- Variables:
  - {{course_name}}
  - {{enrolled_at}}

### 52) course_completed
- Category: UTILITY
- Audience: User
- Description: Completed a course
- Trigger: Course completion
- Variables:
  - {{course_name}}
  - {{completed_at}}

## Biometrics and Face Verification

### 53) face_enrolled
- Category: UTILITY
- Audience: User
- Description: Face enrollment completed
- Trigger: Face enrollment
- Variables:
  - {{timestamp}}

### 54) face_verification_failed
- Category: UTILITY
- Audience: User
- Description: Face verification failed
- Trigger: Face verification error
- Variables:
  - {{timestamp}}
  - {{reason}}

### 55) face_verification_bypassed
- Category: UTILITY
- Audience: User
- Description: Face verification bypass used
- Trigger: Bypass recorded
- Variables:
  - {{timestamp}}

## Updates and Announcements

### 56) app_update
- Category: MARKETING
- Audience: User
- Description: Product update or announcement
- Trigger: Admin update publish
- Variables:
  - {{title}}
  - {{summary}}
  - {{cta_url}}

## Admin or Support (Optional)

### 57) admin_action_needed
- Category: UTILITY
- Audience: Admin
- Description: Admin notification for actions (withdrawal approval, KYC review)
- Variables:
  - {{entity_type}}
  - {{entity_id}}
  - {{user_id}}
  - {{priority}}

## Template Naming Convention
- Prefix: sgnx_
- Category segment: auth_, util_, mkt_
- Event key: use the event key above

Example template names:
- sgnx_auth_auth_email_otp
- sgnx_util_withdrawal_requested
- sgnx_util_rank_upgraded

## Standard Payload Shape (Backend)
Use this object when you emit a notification:

```
{
  "event": "rank_upgraded",
  "userId": "U123",
  "channel": "whatsapp",
  "locale": "en",
  "payload": {
    "full_name": "Jane Doe",
    "old_rank": "Builder",
    "new_rank": "Leader",
    "achieved_at": "2026-05-05T10:30:00Z",
    "earnings_multiplier": "3.0"
  }
}
```

## WhatsApp Template Guidelines
- AUTHENTICATION templates must be used only for OTP/security codes.
- UTILITY templates are for transactional events related to a user action.
- MARKETING templates require explicit opt-in.
- Keep OTP templates very short.
- Include support contact for failure or rejection cases.
