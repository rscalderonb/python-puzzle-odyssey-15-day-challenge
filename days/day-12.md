# Day 12 – Working with dates and time

## Exercise 1: Days between dates

**Question**  
Write a function `days_between(d1, d2)` that takes two date strings in `YYYY-MM-DD` format and returns the absolute number of days between them.

**Hints**  
Use the `datetime` module.

**Solution**
```python
from datetime import datetime

def days_between(d1, d2):
    date1 = datetime.strptime(d1, "%Y-%m-%d")
    date2 = datetime.strptime(d2, "%Y-%m-%d")
    return abs((date2 - date1).days)
```

---

## Exercise 2: Next weekday

**Question**  
Write a function `next_weekday(date_str, weekday)` that returns the next date (as `YYYY-MM-DD`) that falls on the given weekday (0 = Monday ... 6 = Sunday), starting from the day after the given date.

**Solution**
```python
from datetime import datetime, timedelta

def next_weekday(date_str, weekday):
    date = datetime.strptime(date_str, "%Y-%m-%d")
    days_ahead = weekday - date.weekday()
    if days_ahead <= 0:
        days_ahead += 7
    next_date = date + timedelta(days=days_ahead)
    return next_date.strftime("%Y-%m-%d")
```

---

## Exercise 3: Age in years

**Question**  
Write a function `age_in_years(birthdate)` that takes a birthdate string `YYYY-MM-DD` and returns the current age in completed years.

**Solution**
```python
from datetime import datetime, date

def age_in_years(birthdate):
    born = datetime.strptime(birthdate, "%Y-%m-%d").date()
    today = date.today()
    age = today.year - born.year
    if (today.month, today.day) < (born.month, born.day):
        age -= 1
    return age
```

---

## Exercise 4: Format duration

**Question**  
Write a function `format_duration(seconds)` that converts a number of seconds into a human-readable string such as `"2h 15m 30s"`. Omit zero units except when the total is zero.

**Solution**
```python
def format_duration(seconds):
    if seconds == 0:
        return "0s"
    hours, remainder = divmod(seconds, 3600)
    minutes, secs = divmod(remainder, 60)
    parts = []
    if hours:
        parts.append(f"{hours}h")
    if minutes:
        parts.append(f"{minutes}m")
    if secs or not parts:
        parts.append(f"{secs}s")
    return " ".join(parts)
```
