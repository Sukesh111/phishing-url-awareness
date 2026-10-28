# Test Results

Python version used: 3.15.2  |  Operating system: Windows |  Date: 28-10-2026

| # | Input | Expected result | Actual result | Pass/Fail |
|---|-------|-----------------|---------------|-----------|
| 1 | https://www.example.com/login | No listed warning signs | No listed warning signs found. This does NOT prove safety. | PASS |
| 2 | http://192.0.2.10/account | IP address + HTTP | Uses an IP address instead of a familiar domain. / Uses HTTP. HTTPS alone does not prove trust. | PASS |
| 3 | http://example.com@sample.invalid/login | @ symbol + HTTP | Contains an @ symbol; inspect carefully. / Uses HTTP. HTTPS alone does not prove trust. | PASS |
| 4 | https://a.b.c.d.e.example.invalid/path | Many hostname segments | Contains many hostname segments/subdomains. | PASS |
| 5 | https://xn--example.invalid/ | Punycode-style hostname | Contains a punycode-style hostname. | PASS |

## Bonus Checks

| Typed | Expected result | Actual result | What it teaches |
|-------|-----------------|---------------|-----------------|
| Just pressed enter | No URL entered. | No URL entered. | The program handles empty input. |
| www.example.com | Uses HTTP. HTTPS alone does not prove trust. | Uses HTTP. HTTPS alone does not prove trust. | Missing scheme is treated as http:// |
| https://secure-login.example.invalid | No listed warning signs found. | No listed warning signs found. This does NOT prove safety. | A tricky name can slip through. No signs does not mean safe! |
| http://[bad | Program stops with ValueError: Invalid IPv6 URL | ValueError: Invalid IPv6 URL (program crashed) | A real gap in the starter code |

## Notes

This was my first time building a security tool, and I learned that a URL has different parts (scheme, hostname, path) and the hostname is the part that really matters. I was surprised by test 3 (http://example.com@sample.invalid/login) the link looks like it goes to example.com, but the real hostname is sample.invalid because the browser ignores everything before the @. I was also surprised that test 1 showed no warnings, because that does NOT mean the link is safe. My tool only checks six clues, so a dangerous link can still pass. In the bonus checks, typing http://[bad made the program crash with a ValueError, which showed me that my code needs to handle bad input safely.