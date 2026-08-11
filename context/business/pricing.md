---
title: Pricing - live deal data
type: context
status: template
---

<!--
TEMPLATE: what deals actually close at, and the logic behind the numbers. The
offer SHAPES are canonical in context/org/offers.md; this file is canonical for
the MONEY - live deal data, anchoring, what to refine after each close. Every
figure carries provenance (which deal, which document) per the financial-accuracy
rule. Filled during onboarding discovery if there's deal history; otherwise
grown from the first close onward.
-->

# Pricing - live deal data

**Last updated:** (date of the most recent close recorded here)

## Closed deals

One row per signed deal. Figures come from the signed document or invoice, never from recall.

| Deal | Signed | Contract value | Cash collected | Status |
|---|---|---|---|---|

## Pricing framework by offer

For each offer in `context/org/offers.md`: the price band, what moves a deal up or down the band, and the floor we don't cross. Filled during onboarding discovery.

## Anchoring logic

How we open, what we anchor against, and why. Filled as the sales motion settles.

## Not counted (pipeline / history)

Deals that are quoted-but-unsigned, historical engagements under a different model, or anything else that must NOT be read as current pricing truth. Fencing these off here keeps the table above quotable.

## What to refine after each close

A running list: after every close, note what the deal taught about pricing (`## YYYY-MM-DD` entries, newest first).
