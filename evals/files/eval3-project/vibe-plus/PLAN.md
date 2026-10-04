# Pawprint Prints: vibe-plus plan

> A small store selling custom pet-portrait posters, for the owner's Etsy customers who want to buy direct.

**Tool and plan:** Claude Pro, Claude Code, Sonnet  ·  **Capacity:** 8 pts/window (started at 8)  ·  **Availability:** 2 windows on weeknights  ·  **Target:** none

## Decisions (locked)
- Stack: Next.js (App Router) + TypeScript, Tailwind
- Payments: Stripe Checkout + webhook
- Data: SQLite via Prisma
- Hosting: Vercel

## Overview
| Window | Milestone | Tasks | Points | Cooldown 🧑 |
|--------|-----------|-------|--------|-------------|
| W1 | M1 Skeleton | T01, T02, T03 | 7 | H01 Stripe test account |
| W2 | M2 Checkout | T04, T05, T06 | 7 | H02 product photos |
| W3 | M3 Orders | T07, T08, T09 | 7 | H03 test on phone |

## Windows and tasks

### W1: Skeleton (7 / 8)
- [x] **T01 · Scaffold Next.js app** `L` 🤖
- [x] **T02 · Product list page** `M` 🤖
- [x] **T03 · Prisma + Product model + seed** `S` 🤖

### W2: Checkout (7 / 8)
- [ ] **T04 · Product detail page** `S` 🤖
  - **Done when:** /products/[id] renders name, price, image
- [ ] **T05 · Stripe Checkout session endpoint** `M` 🤖
  - **Done when:** POST /api/checkout returns a Checkout URL in test mode
- [ ] **T06 · Stripe webhook → create Order** `L` 🤖 `big`
  - **Files:** `app/api/webhooks/stripe/route.ts`, `prisma/schema.prisma`
  - **Done when:** `stripe trigger checkout.session.completed` creates an Order row
- [ ] **Wrap-up** *(reserved)*

### W3: Orders (7 / 8)
- [ ] **T07 · Order model + admin list page** `M` 🤖
- [ ] **T08 · Order confirmation email** `M` 🤖
- [ ] **T09 · Success / cancel pages** `S` 🤖
- [ ] **Wrap-up** *(reserved)*

## Log
| Date | Window | Planned | Done | Limit hit | Notes |
|------|--------|---------|------|-----------|-------|
| 2026-09-30 | W1 | 7 | 7 | n | smooth |
