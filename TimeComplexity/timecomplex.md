# Time Complexity — Explained with a Deck of Cards 🃏

<style>
body, p, li, td, th { font-size: 16px !important; line-height: 1.7 !important; }
h1 { font-size: 30px !important; }
h2 { font-size: 24px !important; border-bottom: 2px solid #d0d7de; padding-bottom: 4px; }
h3 { font-size: 19px !important; }
table { font-size: 16px !important; }
code, pre { font-size: 15px !important; }
.badge { display: inline-block; padding: 4px 12px; border-radius: 12px; font-weight: bold; color: #fff; margin-bottom: 8px; }
.b-o1 { background: #2e7d32; }
.b-logn { background: #1565c0; }
.b-n { background: #ef6c00; }
.b-n2 { background: #c62828; }
.b-n3 { background: #ad1457; }
.b-2n { background: #6a1b9a; }
.b-nf { background: #212121; }
</style>

## 📑 Table of Contents
1. [The Big Question](#the-big-question)
2. [O(N) — Shuffled Deck](#story-1-searching-a-shuffled-unsorted-deck)
3. [O(log N) — Sorted Deck](#story-2-searching-a-sorted-deck)
4. [O(1) — Constant Time](#story-3-constant-time--o1)
5. [O(N²) — Matching Pairs](#story-4-matching-pairs--on)
6. [O(N³) — Three Decks](#story-5-three-decks--on-1)
7. [O(2ⁿ) — Doubling Every Time](#story-6-doubling-every-time--o2)
8. [O(N!) — All the Orderings](#story-7-all-the-orderings--on-2)
9. [Full Recap & Ranking](#-full-recap)
10. [Why "Big O"?](#why-do-we-call-it-big-o)

---

## The Big Question

> If the number of items I'm searching through keeps growing, how much MORE time will it take me?

That question is what **time complexity** answers. It's just a way to describe: *"as things get bigger, how much slower do I get?"*

---

## Story 1: Searching a Shuffled (Unsorted) Deck
<span class="badge b-n">O(N) · LINEAR</span>

You have a deck of cards thrown in **random order**. You need to find the **6 of Spades**.

Since the cards are in no particular order, there's only one way to find it: **check every card, one at a time**, until you find it.

```
🎴 🎴 🎴 🎴 🎴 🎴 🎴 🎴 🎴 🎴
 1   2   3   4   5   6   7   8   9  10  ← you might have to check ALL of these
                                          before finding the 6 of Spades
```

- 10 cards → check up to 10 cards
- 100 cards → check up to 100 cards
- 1,000 cards → check up to 1,000 cards

**The pattern:** double the cards, double the work. The effort grows in a straight line as the input grows.

📌 This is called **O(N)** — "N" just means "the number of items". Read it as: *the work grows at the same rate as the input.*

```
Work
  |
  |                     ●
  |               ●
  |         ●
  |    ●
  |●
  +----------------------------- Number of cards
```
☝️ A straight diagonal line — that's what O(N) looks like.

---

## Story 2: Searching a Sorted Deck
<span class="badge b-logn">O(log N) · LOGARITHMIC</span>

Now lay the same cards down, but this time **sorted in order** (smallest to largest). You need to find the **7 of Hearts**.

Because the deck is sorted, you don't need to check every card. You can be smart about it:

**Step 1** — Open the card in the *middle* of the deck.

```
🎴 🎴 🎴 🎴 [🎴 6] 🎴 🎴 🎴 🎴
                ↑
          middle card = 6
```
Since you want 7 (bigger than 6), you know it must be somewhere on the **right side**. You completely ignore the left side — no need to look at it at all.

**Step 2** — Open the middle card of what's left (the right half).

```
              🎴 🎴 [🎴 7] 🎴
                        ↑
                found it!
```

That's it — found in just a couple of checks, without ever touching most of the deck.

**The pattern:** every time you look at a card, you throw away **half** of what remains.

📌 This is called **O(log N)** — read it as: *the work barely grows, even when the input grows a lot.*

| Cards in deck | Checks needed (roughly) |
| ---: | ---: |
| 8 | 3 |
| 16 | 4 |
| 1,000 | ~10 |
| 1,000,000 | ~20 |

```
Work
  |
  |                  ●───●───●───●   (barely goes up)
  |         ●
  |   ●
  |●
  +----------------------------- Number of cards
```
☝️ A curve that flattens out — that's what O(log N) looks like. Even with a million cards, you'd only need about 20 checks!

### 🤔 Why is it called O(log N)?

Because on **every single step**, you're not just removing one card — you're throwing away almost **half of everything that's left** in one go.

```
Start: 6 cards ── check middle ──► throw away half (3 gone)
       3 cards ── check middle ──► throw away half (1-2 gone)
       1 card  ── found it! ✅
```

In the original story, opening the middle card eliminated 4 cards on the right and 2 on the left — a huge chunk gone after just one look. That's why even **10 million cards** can be searched in only a handful of steps. This "cutting things in half" pattern is exactly what the word **logarithm** describes.

---

## Story 3: Constant Time — O(1)
<span class="badge b-o1">O(1) · CONSTANT</span>

Imagine 6 bowls lined up in order, each holding a number of blackberries that **matches the bowl's position**:

```
Bowl:        1️⃣    2️⃣    3️⃣    4️⃣    5️⃣    6️⃣
Berries:     🍇     🍇🍇   🍇🍇🍇  🍇🍇🍇🍇 🍇🍇🍇🍇🍇 🍇🍇🍇🍇🍇🍇
```

If someone asks *"how many blackberries are in bowl 5?"* — you don't need to search or count anything. You already know the answer just by looking at the position: **bowl 5 has 5 berries**.

📌 This is called **O(1)** — read it as: *the work never changes, no matter how big the input gets.*

Whether there are 6 bowls or 6 million bowls, finding bowl #5's answer takes exactly the same, tiny amount of effort — **one direct lookup**, every time.

```
Work
  |
  |●──────●──────●──────●──────●   (flat line — never grows!)
  +----------------------------- Number of bowls
```

---

## So What's the Actual Difference?

| | 🔀 Shuffled deck (O(N)) | 🔢 Sorted deck (O(log N)) | 🍇 Numbered bowls (O(1)) |
| --- | --- | --- | --- |
| **How you search** | Check cards one by one, in order | Jump to the middle, eliminate half each time | Go directly to the answer |
| **Requirement** | Works on any deck, sorted or not | Deck **must** be sorted first | Position must directly tell you the answer |
| **1,000 items → work needed** | Up to 1,000 | About 10 | Always 1 |
| **Feels like** | Reading every page of a book to find one word | Using a dictionary — flipping to the middle, then narrowing down | Looking up a locker by its number |

**In one sentence:**
- **O(N)** = "I look at everything, one by one."
- **O(log N)** = "I keep cutting my search area in half, so I barely have to look at anything."
- **O(1)** = "I already know exactly where to look — no searching at all."

That's the whole idea — same kind of problem, three different strategies, three very different amounts of work as the input gets bigger.

---

## 📋 Recap So Far

| Complexity | Example | What happens as input grows |
| --- | --- | --- |
| **O(1)** | Finding blackberries in the right numbered bowl | Work stays the same |
| **O(log N)** | Finding a card in a **sorted** deck | Work grows *very slowly* |
| **O(N)** | Finding a card in a **random/shuffled** deck | Work grows in a straight line |

---

## Story 4: Matching Pairs — O(N²)
<span class="badge b-n2">O(N²) · QUADRATIC</span>

Now imagine **two separate decks** of cards. You pick a card from deck 1 — say the **8** — and now you need to find its match in deck 2.

To find that match, you may have to go through the **entire second deck**, card by card, until you find the 8.

```
Deck 1:  8  →  search all of Deck 2 →  🎴 🎴 🎴 🎴 🎴 [8] 🎴 🎴
```

Now repeat this for **every single card** in deck 1. In the worst case, for *each* of the N cards in deck 1, you do N work searching deck 2.

```
For each card in Deck 1 (N cards):
    Search through all of Deck 2 (N cards)
```

That's "a loop inside a loop" — N work, done N times.

📌 This is called **O(N²)** — read it as: *the work grows by the square of the input.*

| Cards in each deck | Checks needed (worst case) |
| ---: | ---: |
| 10 | 100 |
| 100 | 10,000 |
| 1,000 | 1,000,000 |

```
Work
  |                                ●
  |                        ●
  |                ●
  |         ●
  |    ●
  +----------------------------- Number of cards
```
☝️ A curve that shoots up fast — that's what O(N²) looks like.

---

## Story 5: Three Decks — O(N³)
<span class="badge b-n3">O(N³) · CUBIC</span>

Same idea as O(N²), but now with **three separate decks** instead of two. To find a matching combination, you need a loop inside a loop inside another loop — one for each deck.

```
For each card in Deck 1 (N cards):
    For each card in Deck 2 (N cards):
        Search through all of Deck 3 (N cards)
```

📌 This is called **O(N³)** — read it as: *the work grows by the cube of the input.* Every extra "nested loop" for an extra deck multiplies the work by N again.

---

## Story 6: Doubling Every Time — O(2ⁿ)
<span class="badge b-2n">O(2ⁿ) · EXPONENTIAL</span>

Picture flipping a coin. It has **2 possibilities**: heads or tails.

Now add a second coin. The possibilities **double**: HH, HT, TH, TT — that's **4** outcomes.

Add a third coin, and it **doubles again** — **8** outcomes.

```
1 coin  →  2 possibilities
2 coins →  4 possibilities   (doubled)
3 coins →  8 possibilities   (doubled again)
```

Every single new input **multiplies** the total work by 2, instead of just adding a little more.

📌 This is called **O(2ⁿ)** — read it as: *the work doubles with every additional input.*

This complexity grows so explosively that it's considered **unmanageable** for large inputs — even a modest number of items can produce more possibilities than a computer could reasonably process.

---

## Story 7: All the Orderings — O(N!)
<span class="badge b-nf">O(N!) · FACTORIAL</span>

Imagine a plane with **3 seats** and **3 passengers**, and you want to know every possible way to seat them.

- For **seat 1**, any of the **3** people could sit there.
- For **seat 2**, only **2** people are left to choose from.
- For **seat 3**, only **1** person is left.

```
3 × 2 × 1 = 6 possible seating arrangements
```

📌 This is called **O(N!)** ("N factorial") — read it as: *the work is the product of every number from N down to 1.* It grows even faster than O(2ⁿ) and quickly becomes impossible to compute as N increases.

📝 We'll cover the leftover complexities (O(N log N), O(√N), etc.) by name with a one-line explanation later in the course.

---

## 📋 Full Recap

| Complexity | Example | What happens as input grows |
| --- | --- | --- |
| <span class="badge b-o1">O(1)</span> | Finding blackberries in the right numbered bowl | Work stays the same |
| <span class="badge b-logn">O(log N)</span> | Finding a card in a **sorted** deck | Work grows *very slowly* |
| <span class="badge b-n">O(N)</span> | Finding a card in a **random/shuffled** deck | Work grows in a straight line |
| <span class="badge b-n2">O(N²)</span> | Matching a card between **two** decks | Work grows by the square of N |
| <span class="badge b-n3">O(N³)</span> | Matching a card across **three** decks | Work grows by the cube of N |
| <span class="badge b-2n">O(2ⁿ)</span> | Every possible outcome of flipping N coins | Work doubles with each new input |
| <span class="badge b-nf">O(N!)</span> | Every possible seating order of N passengers | Work grows faster than any of the above — unmanageable for large N |

### 📈 Ranked from Best to Worst (for N = 10)

| Rank | Complexity | Relative work | Growth bar |
| :---: | --- | ---: | --- |
| 🥇 | O(1) | 1 | `█` |
| 🥈 | O(log N) | ~3 | `███` |
| 🥉 | O(N) | 10 | `██████████` |
| 4 | O(N²) | 100 | `████████████████████` |
| 5 | O(N³) | 1,000 | `████████████████████████████` |
| 6 | O(2ⁿ) | 1,024 | `██████████████████████████████` |
| 7 | O(N!) | 3,628,800 | `████████████████████████████████████` |

⚡ **The rule of thumb:** the further down this list your algorithm falls, the fewer inputs it can handle before it becomes too slow to run.

---

## Why Do We Call It "Big O"?

Whenever we describe how fast an algorithm runs, we describe it **in terms of its growth rate relative to the input size** — not the exact time, but how that time changes as the input changes.

For example: if an input of 10 takes 10 seconds, and an input of 1,000 takes 1,000 seconds, there's a **linear relationship** between input size and time — the algorithm runs "in the order of N" time.

That's exactly what the **O** stands for: **Order of** — order of whatever growth rate the input relates to. Big O describes the **upper bound** of an algorithm's growth rate — the worst-case rate at which the work grows as the input grows.
