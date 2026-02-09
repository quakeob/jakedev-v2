---
title: "Fuel"
description: "Calorie tracker with NLP food input, macro tracking, and barcode scanning. Built as a PWA, heading to the App Store."
status: "Live"
emoji: "🔥"
tags: ["JavaScript", "PWA", "NLP", "OpenFoodFacts API"]
github: "https://github.com/quakeob/fuel-app"
live: "https://fuel.jakedavis.dev"
order: 1
---

## The Problem

Every calorie tracker I've used makes the same mistake: they assume I want to scroll through a database of 10,000 foods to log "2 eggs and toast." That's not tracking — that's data entry. And data entry is why people quit on day three.

I wanted something that felt like texting a friend. Type what you ate in plain English, get your macros, move on.

## The Approach

Fuel takes a natural language input — like "2 eggs, slice of sourdough with butter, black coffee" — and breaks it down into calories, protein, carbs, and fat. No dropdowns. No searching. Just type and go.

For packaged foods, there's barcode scanning via the OpenFoodFacts API. Point your camera at a barcode and the nutrition data populates instantly. Between NLP and barcodes, you can log a full day of eating in under 60 seconds.

## Architecture

This is a single-file PWA. Vanilla JavaScript, no framework, no build step, no backend. Everything runs client-side with data stored in localStorage.

That was a deliberate choice. I didn't want users to create accounts. I didn't want to manage a database of food logs. I wanted something you could open, use, and close — like a calculator for food.

The NLP parsing uses a custom tokenizer that handles quantities, units, and food names. It maps common foods to a local nutrition database, with fallback to the OpenFoodFacts API for anything it doesn't recognize.

## Key Decisions

**PWA over native app.** I wanted this on people's home screens within seconds, not after an App Store download. PWAs install instantly and work offline. That said, I'm now wrapping it with Capacitor to hit the App Store too — best of both worlds.

**No accounts, no backend.** Privacy by architecture. Your food data never leaves your phone. There's no server to hack because there's no server.

**Dark, premium UI.** Most calorie trackers look like they were designed in 2012. Fuel has a dark theme with smooth animations and a minimal interface. It should feel like a premium tool, not a medical form.

## What I Learned

Building the NLP parser was the most interesting part. Natural language is messy — "2 eggs" and "a couple eggs" and "eggs x2" all mean the same thing. Getting that right without a full NLP library meant writing a lot of pattern matching and fuzzy logic by hand.

The PWA ecosystem is also more capable than most developers realize. Service workers, cache API, and the Web App Manifest give you 90% of what a native app offers with 10% of the complexity.

## Stack

- **Frontend:** Vanilla JavaScript, HTML5, CSS3
- **Data:** localStorage, OpenFoodFacts API
- **Deployment:** Static hosting, PWA
- **Coming Soon:** Capacitor for iOS/Android native builds
