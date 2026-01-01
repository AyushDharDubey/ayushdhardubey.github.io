---
layout: post
title:  "What Competitive Programming Doesn’t Teach About Performance"
date:   2025-12-25 18:16:00 +0530
author: Ayush Dhar Dubey
categories: blogs
---

# Competitive Programmers entering production

Competitive Programming trains one to fear O(N²) like a mortal sin. Somewhere along the way, it became the ultimate marker of “bad code”. But in production, the real killers usually look far more innocent:

* one N+1 query
* a handful of network or disk calls inside a “cheap” loop
* synchronous I/O hiding behind a clean abstraction

In institutes, the Codeforces / LeetCode culture is so dominant that many engineers grow up optimizing toy problems in isolation, while staying largely unaware of how real systems behave under load.

To be clear, this training *is* useful. Competitive programming teaches fundamentals extremely well: algorithmic thinking, complexity analysis, edge cases, and discipline. But stopping there gives you a very skewed mental model. CP and DSA alone won’t take one very far once they start building production-ready systems.

## Boundaries are expensive

In production, every time your code crosses a boundary, the cost explodes.

* process boundary
* network boundary
* database boundary
* disk boundary

CP problems live entirely inside one process. Production code mostly exists to cope with the cost of boundaries, not pretend they don’t exist.

Production projects have a habit of forcing reality into the picture. They make you confront how expensive a read or write operation really is, even when the task itself looks trivial. A single ORM loop doing database queries can dwarf the cost of any “suboptimal” in-memory algorithm one was taught to fear.

## The limits of Big-O

Big-O, by design, abstracts away things that dominate real-world performance:

* it ignores constants
* it assumes uniform cost per operation
* it ignores latency and blocking
* it ignores contention, queues, and backpressure

In the hoard of DSA, CP problems, and script-level solutions, it’s easy to forget that Big-O is a theoretical tool. It was never meant to answer system-level questions. At the system level, we deal with network latency, disk I/O, thread contention, cache misses, and coordination costs. Big-O does not, and cannot, account for these.

**Big-O answers “what happens as *n* grows”.**  
**Production asks “what happens when this runs 10,000 times per minute”.**

## The N+1 query problem

If you’ve worked with databases and applications long enough, you’ve almost certainly met the N+1 query problem.

Imagine a list of users, where each user can have multiple uploaded models. This is a classic one-to-many relationship. Now suppose you need to fetch all users along with their models. A naive approach is to first query all users, and then, for each user, issue another query to fetch their models.

It looks harmless. It even feels clean.

That’s the N+1 query devil.

You run one query to get *N* users, then *N* additional queries to fetch their related data. With 100 users, that’s 101 queries.

That's way too much for a single request. But in the CP world, it's just O(1)*N operations, right? Now let's say you serve 100 users per minute. That’s 10,100 queries per minute. Over an hour, that’s 606,000 queries. Over a day, that’s over 14 million queries. This is what's gonna smoke your database server. No O(N²) here, just N+1, but the effect is multiplicative.

As the dataset grows, the latency quietly balloons. Test cases often don’t catch this because they run on small datasets where the overhead is negligible. In production, with real data and real traffic, this pattern can cripple performance.

*Solution: Use joins to fetch data in one query, or use ORM batch loading to avoid N+1.*

## Real-world performance considerations

One might carefully optimize a sorting algorithm from O(NlogN) to O(N), while overlooking that the data is fetched over a network with 200ms latency – making the sort time irrelevant.

Big-O still matters. Algorithmic thinking still matters. One just need to know when it stops being the dominant factor in the system.

I recently ran into a case in a large-scale project where we were performing disk I/O on every API call just to load environment variables. In an otherwise highly optimized ecosystem, this alone accounted for roughly 25–30% of the total request latency. At that scale, this wasn’t a micro-optimization. It was the bottleneck.

That’s the gap between algorithmic cleanliness and system reality. And it’s a gap one will only notice after something catches fire.
