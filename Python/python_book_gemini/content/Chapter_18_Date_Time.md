# Chapter 18: Date & Time Handling

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: `datetime` module (`datetime`, `date`, `time`, `timedelta`), `time` module (`sleep`, `monotonic`, `perf_counter`), `calendar`, `zoneinfo`, Aware vs Naive objects, Formatting codes (strftime/strptime), ISO 8601.

---

**Q18.1: Basic - [Datetime Now]**

How do you get the current local date and time?

A) `datetime.now()`
B) `datetime.datetime.now()`
C) `time.now()`
D) `date.today()`

**Answer: B**

**Explanation:**
`datetime` is the module, and `datetime` is also a class inside it. So the full path is `datetime.datetime.now()`.

---

**Q18.2: Intermediate - [Timedelta]**

`d = datetime.date(2023, 1, 1) + datetime.timedelta(days=10)` results in:

A) `datetime.date(2023, 1, 11)`
B) `datetime.date(2023, 1, 10)`
C) Error.
D) A string.

**Answer: A**

**Explanation:**
`timedelta` adds a duration to a date/datetime object.

---

**Q18.3: Advanced - [Aware vs Naive]**

A "naive" datetime object:

A) Contains no timezone information.
B) Contains timezone information.
C) Is incorrect.
D) Cannot be compared.

**Answer: A**

**Explanation:**
Naive objects do not have enough info to locate themselves relative to other timezones unambiguously. Aware objects have `tzinfo`.

---

**Q18.4: Basic - [Sleep]**

`time.sleep(2.5)`:

A) Pauses execution for exactly 2.5 seconds.
B) Pauses execution for *at least* 2.5 seconds.
C) Pauses for 2.5 milliseconds.
D) Pauses only the current function, not the thread.

**Answer: B**

**Explanation:**
It's "at least" because the OS scheduler may take slightly longer to resume the thread.

---

**Q18.5: Intermediate - [Strftime]**

To convert a datetime object `dt` to a string like "YYYY-MM-DD", use:

A) `dt.format("%Y-%m-%d")`
B) `dt.strftime("%Y-%m-%d")`
C) `dt.strptime("%Y-%m-%d")`
D) `str(dt, "%Y-%m-%d")`

**Answer: B**

**Explanation:**
`strftime` = String Format Time (Object -> String).

---

**Q18.6: Advanced - [Monotonic Time]**

`time.monotonic()` is preferred over `time.time()` for measuring duration because:

A) It is faster.
B) It is not affected by system clock updates (e.g., NTP adjustments or user changing time).
C) It returns an integer.
D) It provides date info.

**Answer: B**

**Explanation:**
`time.time()` returns wall-clock time which can jump backwards. `monotonic` only ever moves forward.

---

**Q18.7: Basic - [Date Today]**

To get just today's date (no time):

A) `datetime.date.today()`
B) `datetime.datetime.today()`
C) `datetime.today()`
D) `date.now()`

**Answer: A**

**Explanation:**
`datetime.date.today()` returns a `date` object. `datetime.datetime.today()` returns a `datetime` object (with time).

---

**Q18.8: Intermediate - [Date Arithmetic]**

`date1 - date2` returns:

A) An integer (days).
B) A `timedelta` object.
C) A float.
D) A string.

**Answer: B**

**Explanation:**
Subtracting two date/datetime objects yields the duration between them.

---

**Q18.9: Advanced - [ZoneInfo]**

Introduced in Python 3.9, `zoneinfo.ZoneInfo("America/New_York")`:

A) Returns the current time in NY.
B) Returns a `tzinfo` object representing the IANA time zone.
C) Deprecates `pytz`.
D) Is a string.

**Answer: B**

**Explanation:**
It is the modern, standard library way to handle timezones, replacing the need for third-party `pytz` for most cases.

---

**Q18.10: Expert - [Fold Attribute]**

The `fold` attribute (0 or 1) in a datetime object helps resolve ambiguity during:

A) Leap years.
B) Daylight Saving Time (DST) transitions (specifically the "fall back" hour where clocks repeat).
C) Time/Date separation.
D) Formatting.

**Answer: B**

**Explanation:**
When clocks go back 1 hour, the time 1:30 AM happens twice. `fold=0` is the first occurrence, `fold=1` is the second.

---

**Q18.11: Basic - [Importing]**

Standard import for datetime:

A) `import datetime`
B) `from time import datetime`
C) `include datetime`
D) `import date`

**Answer: A**

**Explanation:**
The module is named `datetime`.

---

**Q18.12: Intermediate - [Strptime]**

`datetime.datetime.strptime("2023-01-01", "%Y-%m-%d")` returns:

A) A string.
B) A `datetime` object.
C) A `date` object.
D) A tuple.

**Answer: B**

**Explanation:**
`strptime` = String Parse Time (String -> Object). Note it returns a `datetime` even if only date fields are parsed (time defaults to 00:00:00).

---

**Q18.13: Advanced - [Weekday]**

`dt.weekday()` returns:

A) The name of the day (e.g. "Monday").
B) An integer 0 (Monday) to 6 (Sunday).
C) An integer 1 (Monday) to 7 (Sunday).
D) An integer 0 (Sunday) to 6 (Saturday).

**Answer: B**

**Explanation:**
Python's `datetime` uses 0=Monday. `isoweekday()` uses 1=Monday.

---

**Q18.14: Basic - [Epoch]**

UNIX timestamp 0 corresponds to:

A) Jan 1, 1900.
B) Jan 1, 1970 00:00:00 UTC.
C) Dec 31, 1999.
D) The start of the computer.

**Answer: B**

**Explanation:**
The standard UNIX epoch.

---

**Q18.15: Intermediate - [Combining Date Time]**

To create a `datetime` from a `date` object `d` and a `time` object `t`:

A) `datetime.combine(d, t)`
B) `d + t`
C) `datetime(d, t)`
D) `d.append(t)`

**Answer: A**

**Explanation:**
`datetime.combine(date, time)` allows merging separate components.

---

**Q18.16: Advanced - [Perf Counter]**

`time.perf_counter()` includes:

A) Only time spent in the process.
B) Time elapsed during sleep and system-wide delays (wall time), with the highest available resolution.
C) CPU time only.
D) Network time.

**Answer: B**

**Explanation:**
Ideally suited for benchmarking execution time.

---

**Q18.17: Expert - [Fromtimestamp]**

`datetime.datetime.fromtimestamp(ts)` assumes `ts` is in:

A) UTC.
B) Local system timezone (unless tz is specified).
C) GMT.
D) Arbitrary.

**Answer: B**

**Explanation:**
Without a `tz` argument, it converts the timestamp to the platform's local datetime. Use `fromtimestamp(ts, tz=timezone.utc)` for UTC.

---

**Q18.18: Intermediate - [Timedelta Seconds]**

`td = timedelta(days=1)`. `td.total_seconds()` returns:

A) 1.
B) 86400.0
C) 24.
D) 1440.

**Answer: B**

**Explanation:**
86400 seconds in a day. `td.seconds` only returns the seconds part (< 1 day), `total_seconds()` converts days + seconds + microseconds to total seconds.

---

**Q18.19: Basic - [Calendar Module]**

`calendar.isleap(2024)`:

A) Checks if 2024 is a leap year.
B) Checks if a frog jumps.
C) Returns the number of days in 2024.
D) Prints a calendar.

**Answer: A**

**Explanation:**
Simple boolean check for leap years.

---

**Q18.20: Advanced - [UTC Now]**

Correct way to get current UTC datetime (modern Python):

A) `datetime.utcnow()`
B) `datetime.now(datetime.timezone.utc)`
C) `time.utc()`
D) `date.utc()`

**Answer: B**

**Explanation:**
`utcnow()` creates a *naive* datetime (which is often confusing). `now(timezone.utc)` creates an *aware* datetime, which is best practice. `utcnow()` is deprecated in 3.12+.

---

**Q18.21: Expert - [ISO Format]**

`dt.isoformat()` produces string like:

A) "YYYY-MM-DDTHH:MM:SS..."
B) "MM/DD/YYYY"
C) "DD-Mon-YYYY"
D) UNIX timestamp.

**Answer: A**

**Explanation:**
International standard format. E.g. `2023-01-01T12:00:00`.

---

**Q18.22: Intermediate - [Replace Method]**

`dt.replace(year=2025)`:

A) Modifies `dt` in place to 2025.
B) Returns a new datetime object with year set to 2025, keeping other fields same.
C) Raises error.
D) Returns a string.

**Answer: B**

**Explanation:**
Datetime objects are immutable. `replace` returns a copy with updated fields.

---

**Q18.23: Basic - [Time Module]**

`time.time()` returns:

A) Current time as string.
B) Current time as a datetime object.
C) Seconds since the Epoch (float).
D) Milliseconds since boot.

**Answer: C**

**Explanation:**
Standard timestamp format.

---

**Q18.24: Advanced - [Timezone Fixed Offset]**

To create a timezone that is 5 hours and 30 minutes ahead of UTC (e.g., IST) without `zoneinfo`:

A) `datetime.timezone(datetime.timedelta(hours=5, minutes=30))`
B) `datetime.timezone(5.5)`
C) `datetime.tzinfo(5, 30)`
D) It is impossible without libraries.

**Answer: A**

**Explanation:**
`datetime.timezone` takes a timedelta offset.

---

**Q18.25: Intermediate - [Timedelta Arithmetic]**

`timedelta(hours=1) + timedelta(minutes=60)` equals:

A) `timedelta(hours=2)`
B) `2`
C) `timedelta(hours=1, minutes=60)` (unnormalized)
D) `timedelta(days=1)`

**Answer: A**

**Explanation:**
It normalizes inputs. 60 minutes = 1 hour. Result is 2 hours.

---

**Q18.26: Expert - [Min/Max Year]**

What are `datetime.MINYEAR` and `datetime.MAXYEAR`?

A) 1 and 9999.
B) 1970 and 2038.
C) 0 and 9999.
D) 1900 and 2100.

**Answer: A**

**Explanation:**
The library supports years 1 through 9999.

---

**Q18.27: Basic - [Parse ISO]**

`datetime.date.fromisoformat("2023-01-01")`:

A) Returns a date object.
B) Error.
C) Returns a string.
D) Returns a timestamp.

**Answer: A**

**Explanation:**
Inverse of `isoformat()`.

---

**Q18.28: Advanced - [Total Seconds Resolution]**

Does `timedelta.total_seconds()` lose precision for very large intervals?

A) No.
B) Yes, because it returns a float, and floats lose precision for very large numbers (microsecond accuracy might be lost for intervals > 270 years).
C) Yes, it truncates to integer.
D) It depends on the CPU.

**Answer: B**

**Explanation:**
Standard floating point limitations apply.

---

**Q18.29: Intermediate - [Process Time]**

`time.process_time()` measures:

A) Wall clock time.
B) CPU time consumed by the current process (system + user).
C) Time since boot.
D) Time spent in I/O.

**Answer: B**

**Explanation:**
Does not include sleep time. Useful for profiling CPU usage.

---

**Q18.30: Expert - [Timezone ASTimezone]**

`dt_aware.astimezone(new_tz)`:

A) Changes the stored time to the new timezone (e.g. converting UTC to local time).
B) Just changes the tzinfo tag without adjusting the hour.
C) Errors if `dt` is aware.
D) Returns naive object.

**Answer: A**

**Explanation:**
It calculates the same point in time as represented in the new timezone, adjusting hour/minute/day as needed.

---

**Q18.31: Intermediate - [Parse Dateutil]**

When standard `strptime` is too rigid, which third-party library is commonly used to parse messy date strings (e.g. "Next Monday", "Jan 1st")?

A) `datetime.parser`
B) `dateutil.parser`
C) `pytz`
D) `numpy`

**Answer: B**

**Explanation:**
`dateutil` is a powerful extension to the standard `datetime` module. (Though this book focuses on standard lib, `dateutil` is universally used alongside it).

---

**Q18.32: Advanced - [Timezone Name]**

`dt.tzname()` returns:

A) The name of the timezone (e.g. "EST", "UTC") or None if naive.
B) The offset.
C) The region string "America/New_York".
D) An integer.

**Answer: A**

**Explanation:**
Returns the time zone name corresponding to the `datetime` as a string.

---

**Q18.33: Basic - [Leap Year Days]**

A leap year has:

A) 366 days.
B) 365 days.
C) 364 days.
D) 365.25 days.

**Answer: A**

**Explanation:**
Feb 29th is added.

---

**Q18.34: Expert - [Timezone Transmogrification]**

If you mistakenly created a datetime as UTC but it represents Local time (e.g. 5PM local marked as 5PM UTC), how do you fix it without changing the hour?

A) `dt.astimezone(local_tz)`
B) `dt.replace(tzinfo=local_tz)`
C) `dt - timedelta(hours=5)`
D) Impossible.

**Answer: B**

**Explanation:**
`replace(tzinfo=...)` changes the timezone constraint attached to the timestamp *without* converting the numerical time values. `astimezone` converts the time instant (changing the numbers).

---

**Q18.35: Intermediate - [Time Struct]**

`time.localtime()` returns:

A) A `datetime` object.
B) A `struct_time` named tuple (tm_year, tm_mon, ...).
C) A string.
D) A float.

**Answer: B**

**Explanation:**
The low-level `time` module often uses `struct_time`.

---

**Q18.36: Advanced - [ISO Week]**

`dt.isocalendar()` returns a tuple:

A) `(year, month, day)`
B) `(ISO_year, ISO_week_number, ISO_weekday)`
C) `(year, week, day)`
D) `(hour, minute, second)`

**Answer: B**

**Explanation:**
ISO years can differ from calendar years at the start/end of the year (e.g., Jan 1st might belong to the previous year's last ISO week).

---

**Q18.37: Basic - [Time Sleep Float]**

Can `time.sleep()` accept partial seconds (floats)?

A) Yes (e.g., 0.1).
B) No, only integers.
C) Only in Python 2.
D) Only `time.usleep`.

**Answer: A**

**Explanation:**
Sub-second precision is supported.

---

**Q18.38: Intermediate - [Datetime Comparison]**

Can you compare (`<`, `>`) an aware datetime with a naive datetime?

A) Yes, naive is assumed UTC.
B) Yes, naive is assumed Local.
C) No, raises `TypeError`.
D) Yes, result is random.

**Answer: C**

**Explanation:**
To prevent bugs, Python forbids comparing mixed aware/naive datetimes. You must convert one to match the other.

---

**Q18.39: Advanced - [Mixed Interval]**

`datetime.timedelta(days=1, seconds=1)` is equal to:

A) `86401 seconds` duration.
B) `1` day.
C) `1` second.
D) Error.

**Answer: A**

**Explanation:**
Timedelta components are summed up to form the total duration.

---

**Q18.40: Expert - [UTC Timestamp]**

`dt.timestamp()` works for naive datetimes by assuming:

A) They are UTC.
B) They are Local system time.
C) They are invalid.
D) They are GMT.

**Answer: B**

**Explanation:**
If the instance is naive, it calls `mktime()` which interprets the time as local time. This often leads to subtle bugs if the naive time was intended to be UTC.

---

**Q18.41: Intermediate - [String to Date]**

To parse "15-Jan-2023":

A) `%d-%b-%Y`
B) `%d-%B-%Y`
C) `%D-%m-%y`
D) `%x`

**Answer: A**

**Explanation:**
`%d`=Day(15), `%b`=Abbreviated Month(Jan), `%Y`=Year(2023). (`%B` is full month name).

---

**Q18.42: Basic - [Max Timedelta]**

Can `timedelta` represent negative durations?

A) No.
B) Yes.
C) Only days.
D) Only seconds.

**Answer: B**

**Explanation:**
e.g. `date1 - date2` where date1 is before date2.

---

**Q18.43: Advanced - [Invariant]**

`dt == datetime.fromtimestamp(dt.timestamp())` is true:

A) Always.
B) Only for UTC aware datetimes or consistent local times (ignoring microseconds precision loss).
C) Never.
D) Only for naive.

**Answer: B**

**Explanation:**
Rounding errors (float conversion in timestamp) can make them unequal. Also, naive -> local interpretation changes if TZ settings change.

---

**Q18.44: Expert - [Platform Y2K38]**

`datetime` objects (pure Python) are limited by the 2038 problem (32-bit integer overflow)?

A) Yes.
B) No.
C) Only on Windows.
D) Only `time` module.

**Answer: B**

**Explanation:**
`datetime` objects store year/month/day as fields, supporting up to year 9999. However, `datetime.timestamp()` (creating a float/int timestamp) might be limited by the underlying C library or OS if it uses 32-bit `time_t`.

---

**Q18.45: Intermediate - [Format Codes]**

`%p` in strftime stands for:

A) PM/AM.
B) Percentage.
C) Padding.
D) Precision.

**Answer: A**

**Explanation:**
Locale-appropriate AM or PM.

---

**Q18.46: Basic - [Date Init]**

`datetime.date(2023)`:

A) Created Jan 1, 2023.
B) Raises Error (missing month/day).
C) Created Today 2023.
D) Created 2023-12-31.

**Answer: B**

**Explanation:**
Constructor requires `year`, `month`, `day`.

---

**Q18.47: Advanced - [Timezone UTC]**

Which is the correct singleton for UTC in Python 3.2+?

A) `datetime.UTC` (3.11+) or `datetime.timezone.utc`.
B) `pytz.utc`.
C) `datetime.timezone(0)`.
D) `None`.

**Answer: A**

**Explanation:**
`datetime.timezone.utc` is the standard library instance. Python 3.11 introduced the alias `datetime.UTC`.

---

**Q18.48: Expert - [Strftime Thread Safety]**

Is `datetime.strftime` thread-safe?

A) No, it uses global locale settings.
B) Yes.
C) Only in multiprocessing.
D) Only for UTC.

**Answer: A**

**Explanation:**
It calls the C library `strftime`, which might depend on `setlocale`. If one thread changes the locale while another formats a date, the result might be mixed/incorrect.

---

**Q18.49: Intermediate - [Naive Arithmetic]**

`naive_dt - aware_dt`:

A) Returns result assuming naive is UTC.
B) Returns result assuming naive is Local.
C) Raises `TypeError`.
D) Returns timedelta.

**Answer: C**

**Explanation:**
Cannot mix naive and aware.

---

**Q18.50: Basic - [Time Module Purpose]**

The `datetime` module is distinct from `time` because:

A) `time` wraps C library functions (epoch based), `datetime` implies Object Oriented interface.
B) `time` is newer.
C) `datetime` is deprecated.
D) `time` cannot handle dates.

**Answer: A**

**Explanation:**
`time` exposes platform C functions (mostly using timestamps or tuples). `datetime` provides high-level objects.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
