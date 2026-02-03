---
layout: post
title: "stratascratch 2054: Consecutive Days"
date:  2026-02-04 13:00:00 -5
excerpt: "Simple DP"
mathjax: true
math: true
hidden: false
categories: [SQL]
tags: [SQL, optimization, stratascratch]
---

[stratascratch 2054 | Consecutive Days](https://platform.stratascratch.com/coding/2054-consecutive-days)

# Intuition & Approach

The question requires to write a sql query to find any user who has 3 consecutive days with activity.

## Step 1: Simple Intutive Solution

The very basic or intutive solution is, join in 2 levels.

```
SELECT DISTINCT a.user_id FROM sf_events AS a
INNER JOIN sf_events AS b ON a.user_id = b.user_id AND b.record_date = a.record_date + '1 days'
INNER JOIN sf_events AS c ON a.user_id = c.user_id AND c.record_date = b.record_date + '1 days';
```

## Step2: Analysis Complexity

What is the worst case? Assume there's very terrible situation, most user has 2 consecutive days within the database. Then you should compare almost $\Theta(n^3)$ times! It's a disaster.

# Optimization & Extension

## Step3: Consider general case

If you're asked to find 4,5,6 even 20 consecutive days, will you write 20 level join clause? That's impossible.

What about: group the first date together? 

This is written in postgresql. Let's try to get ```ROW_NUMBER()``` as the baseline of first date. For example, you have Jan 1 asthe baseline, then Jan 2 will be on the second row, minus 1 more days compare with Jan 1, they're in the same group! Otherwise, if the next row is Jan 3, it won't be in the same group with Jan 1.

```
sf_processed AS (
    SELECT
        user_id,
        record_date - (ROW_NUMBER() OVER (PARTITION BY user_id ORDER BY record_date ASC))::INTEGER AS group_id
    FROM sf_cleaned
)
```

So we only need to count how many dumplicates in the table.

```
SELECT user_id
FROM grouped_events
GROUP BY user_id, group_id
HAVING COUNT(*) >= 3;
```

Additionally, don't forget to clean your data! There may be multiple rows for one user on the same day!

```
with sf_cleaned as(
select distinct user_id, record_date from sf_events),
```

## Step4: Complexity Analysis

This only counts $O(n\log{n})$. Why? There's a sort algorithm! 


When you're asked by your boss to count 21 consecutive days, this idea saves a lot of time!