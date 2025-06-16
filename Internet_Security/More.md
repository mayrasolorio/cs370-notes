# More Web Security

## Same-Origin Policy
- **Definition**: Prevents one origin (scheme + host + port) from accessing data from another.
- **Purpose**: Stops malicious sites from reading sensitive data (cookies, DOM, etc) from other sites.
- **Exceptions**: 
    - **Cross-Origin Writes**: Like form submissions are allowed accross websites, but **reads are blocked** unless permission is given.
    - **Cross-Origin Resource Sharing**: Servers can explicitly allow specific servers to access data.
    - **postMessage**: Allows safe, explicit cross-origin communication. (safe way for websites to TALK to each other, but only if both parties agree)


## Content Security Policy (CSP)
- **Definition**: Browser feature that controls what content (scripts, images, etc) can be loaded/executed using HTTP headers. (Rules for what your site is allowed to load)
- **Goal**: Prevent XSS and code injection by creating an allow-list for sources. (Stop hackers from sneaking in bad stuff)
- **Example**: Only allow scripts from Google and your own domain. (You make a guest list, browser blocks everyone else)
- **Key Directives**: `script-src` (controls what scripts can run), `img-src` (controls what images can load), `frame-ancestors` (controls who can frame your site), etc.
- **Challenges**:
    - Legacy code may use inline scripts or `eval()`, which need to be removed or refactored.
    - Use `Report-Only` mode to test before enforcing.
- **Avoid Using**: `unsafe-inline`, `unsafe-eval` -- they weaken security.


## iframe Sandboxing
- **Why it matters**: Embedding untrusted content, (e.g. ads, videos) in iframes can be risky.
- **`sandbox` attribute**: Restricts iframe behavior (scripts, forms, popups, etc)
- **Tokens to selectively allow**: `allow-scripts`, `allow-forms`, `allow-same-origin`, `allow-popups`.
- **Without `allow-same-origin`**: iframe is treated as if it's from a unique origin (strong isolation).
- **CSP `sandbox` directive**: Enforces sandboxing even if iframe tag doesn't include it.


## Clickjacking Protection
- **X-Frame Options Header**:
    - `DENY`: Page can't be framed at all
    - `SAMEORIGIN`: Only your site can frame it
- **Alternative**: `frame-ancestors` in CSP (more flexible)
- **Use-Case**: Present invisible overlays that trick users into clicking things (common in banking/phishing attacks).


## Other Important Security Headers
