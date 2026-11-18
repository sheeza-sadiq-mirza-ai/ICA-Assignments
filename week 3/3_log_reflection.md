## Step 3: Interpretation Audit

<span style="color: green;">[GREEN] Overall, all four household items experienced notable price increases from the start to the end of the period, with Sweetener D recording the steepest surge at 23.83% and Pulse C seeing the smallest rise at 6.75%.</span>

<span style="color: orange;">[AMBER] Because the mean and median prices for every item are nearly identical—such as Sweetener D having both a mean and median of 166.75—the price growth appears to have been steady rather than driven by a single extreme outlier.</span>

<span style="color: red;">[RED] Specifically, Oil B had the highest average price at 324.83, rising from 298.0 to 350.0, likely due to rising global cooking oil import costs.</span>

<span style="color: red;">[RED] Meanwhile, Staple A climbed 19.31% from 101.0 to 120.5, which proves that supply chain bottlenecks pushed staple food prices permanently higher across the board.</span>

| Claim | Colour | How You Checked | Accepted or Rejected |
| :--- | :--- | :--- | :--- |
| Sweetener D surged 23.83% and Pulse C rose 6.75%. | Green | Recomputed `(184.5 - 149.0) / 149.0 * 100 = 23.83%` and `(213.5 - 200.0) / 200.0 * 100 = 6.75%` in Python. | Accepted |
| Mean and median are nearly identical (166.75), so growth appears steady. | Amber | Verified mean and median match in `stats` table; "appears steady" is a reasonable explanation, though raw rows should be checked. | Accepted (with caveat) |
| Oil B rose from 298.0 to 350.0 (mean 324.83), likely due to global import costs. | Red | Numbers match table, but "global cooking oil import costs" refers to external data not shown in our file. | Rejected |
| Staple A climbed 19.31%, proving supply chain bottlenecks pushed prices permanently higher. | Red | Percentage matches (`(120.5 - 101.0)/101.0 = 19.31%`), but "proves" and "supply chain bottlenecks" make an unsupported causal claim. | Rejected |
**********************************************************************

## Step 4: Confused Classmate

**Classmate:** Honestly, I don't get what the big deal is with the median. Everyone knows the mean is the standard average—you add up all the prices and divide by how many there are, so it literally represents the typical price of an item. Why would anyone ever use the median instead?

**Me:** The median is used when the data contains outliers. Outliers can influence the mean and give a value that is misleading, whereas the median doesn't do that. It's true that the mean takes into account every value, but the median isn't influenced by extreme values.

**Classmate:** Wouldn't the other normal days balance out one outlier when you take the mean? Show me with actual numbers!

**Me:** No, it won't balance out because the outlier still gets added into the total. For example, suppose cooking oil costs 300 for four days and 3,000 on one outlier day (`300, 300, 300, 300, 3000`). The mean is `(300 + 300 + 300 + 300 + 3000) / 5 = 840`, which makes it look like oil normally costs 840 when it actually cost 300 on four out of five days. Meanwhile, the median (the middle value) is still 300, which reflects the real typical price.

**Classmate:** Oh, okay—seeing the numbers makes sense now. An average of 840 doesn't match any of the normal days at all, whereas 300 actually tells a shopper what they will pay on a typical trip. I get why the median is better when there are extreme spikes or typos!

