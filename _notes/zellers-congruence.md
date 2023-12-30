---
title: Zeller's Congruence
summary: Given a date, what is the day?
publish_date: 2023-12-30
---

Recently, I came across an interesting application of modular arithmetic which is used to calculate the day of the week from the exact date in the Gregorian calendar with ease. The formula is called Zeller's Congruence. 

The formula is as follows (uses decimal arithmetic)
$$h = (q + \lfloor \frac{13(m + 1)}{5} \rfloor + K + \lfloor \frac{K}{4} \rfloor + \lfloor \frac{J}{4} \rfloor - 2J)\ mod\ 7$$
Nuances: $m$ is shifted by 12 for the months of January and February. This is to account for February's fault of being short. $J$ is basically the first two digits of the year, like 19 for 1987, 20 for 2011. It's sort of like the century count. $K$ is $year\ mod\ 100$, measuring what year it is in the century. 

The $h$ serves as an index for the weekday lookup that begins with Saturday for 0, Sunday for 1, and progresses to Friday for 6. 

Computer based implementation in Rust: 
```rust
// Uses Zeller's congruence to calculate the weekday of a particular date 
fn which_weekday(date: usize, month: usize, year: usize) -> usize {
  (date + (13 * (month + 1)) / 5 + year + (year / 4) - (year / 100) + (year / 400)) % 7
}

if month <= 2 {
	weekday = which_weekday(1, month + 12, year - 1);
} else { 
	weekday = which_weekday(1, month, year);
}
```

Understanding the congruence: 
Note: So, the formula basically dumbs down the shifting effect days of the week have. It is sort of like a system of gears with individual RPMs based on the number of teeth they have. Month gear has 12 for each month, and months have the number of days determine their teeth, whereas week gear has 7 for the days. 
- The basic effect on the weekday trickles down on the basis of four variables, day of the month, month of the year and the year of the century and the century itself.  
- For the day of the month, it is straightforward, since each day results in a linear increase for the week count. The increase however is circled back as discussed earlier by the modulo which is cool. 
- For the year, we have a different scenario because we have leap years and normal years. Leap years push the days after the month of February by an extra 1. Normal years push the days by 1 since 365 % 7 is 1 and 366 % 1 is 2. This is handled by $K$ and $\lfloor \frac{K}{4} \rfloor$ in the formula. 
- For the century, a similar effect can be observed. Century divisible by 400 has 36525 days and others have 36524 days. The term $\lfloor \frac{J}{4} \rfloor - 2J$ accounts for this. 
- The term $\lfloor \frac{13(m + 1)}{5} \rfloor$ where $m$ has been adjusted accounts for the shifts in the days of each month. 
  Number of days in each month: (31, 28/29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31)
  Variations as calculated by modulo: (3, 0/1, 3, 2, 3, 2, 3, 3, 2, 3, 2, 3)
  Every 5 months, we have 31, 31 coming together. (Dec-Jan, Jul-Aug)
  /5 takes care of that. As per the effect of leap years, it is already taken care of. For the short count, January becomes the 13th month and February becomes the 14th month. 

For computers the formula is simple as long as you handle the cases for January and February separately. The month and year here are as is. 
$$h = (q + \lfloor \frac{13(m + 1)}{5} \rfloor + Y + \lfloor \frac{Y}{4} \rfloor - \lfloor \frac{Y}{100} \rfloor + \lfloor \frac{Y}{400} \rfloor)\ mod\ 7$$
In the months of January and February, the modifications are $m = m + 12$, and $Y = Y - 1$. 

