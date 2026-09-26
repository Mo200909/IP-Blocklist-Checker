# IP Blocklist Checker

A script that checks IP addresses from log lines against a known blocklist and reports which ones are blocked.

## What it does

1. Takes log lines (each starting with an IP address)
2. Extracts the IP from each line
3. Checks it against a hardcoded blocklist
4. Prints only the blocked IPs, plus a total/blocked count summary

## Run it

```bash
python IP-Blocklist-Checker.py
```

No arguments, no setup. It runs against a built-in sample log so you can see it work immediately.

## Sample output

```
===IP Blocklist Checker===
203.0.113.99: is blocked
45.83.65.12: is blocked

Total checked: 4 | Blocked: 2
```

## How the code works (step-by-step)

1. `BLOCKLIST` — a `set` of known-bad IPs. Set lookup is O(1), which is why this isn't a list.
2. `sample_log` — fake log lines standing in for real log data.
3. First loop — splits each line on whitespace and grabs the first token (the IP).
4. Second loop — checks each IP against `BLOCKLIST`, stores `(ip, is_blocked)` tuples.
5. Third loop — prints only the blocked ones (the `continue` skips printing for non-blocked IPs), tracks a running count.

## To adapt this for a real log file

Replace `sample_log` with:

```python
with open("your_log_file.txt") as f:
    sample_log = f.readlines()
```

## Known limitations

- Blocklist is hardcoded — no external feed or file
- No IP format validation (a malformed IP just won't match, silently)
- Assumes IP is always the first whitespace-separated token in the line
