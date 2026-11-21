---
title: Decision log of JN C Crate
reader: anyone who needs to know why this node is shaped the way it is, including an agent that only sees this node
purpose: Backbone of this node's decisions (D-NNNN). Full reasoning stays where the work was done, linked from each entry.
lifecycle: durable (append-only, read by id)
---

# Decision log

Format: `### D-NNNN · title · date`, then surface, what it replaces, and the rule. Framework decisions (PFD-NNNN) go to `JN C RnD/framework/`.

### D-0001 · Node created · 2026-11-22

**Surface:** whole node · **Replaces:** nothing · **Source:** `agentic-setup-project-jn`, request by Jordi

Jordi wants to build an alternative to Music League and has several ideas to improve on it. The project starts with market research (what Music League and its competitors offer, user complaints, platform constraints such as the Spotify API terms) before any product decision. Everything in this node, docs and code, is in English (Jordi, 2026-11-22). It lives in `AI Projects/` because it is a first trial with an end; if it becomes a long-lived product, it moves to `AI Areas/` with a new decision. Working name `Crate` (crate digging); the product name is decided later, after the market study shows which names are taken. GitHub repo: `jn-c-crate`, private, created by Jordi.
