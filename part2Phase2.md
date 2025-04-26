# Phase 2 - Part 2 Report

## 1. Performing a Dictionary Attack via a Web Interface

### 🔹 Using Burp Suite

A dictionary attack was performed against the login page at `http://localhost:8000/login` using Burp Suite Intruder.

- A small custom wordlist containing common passwords such as `123456`, `password`, and `abc123` was used.
- The attack simulated how weak or common passwords could be exploited to gain unauthorized access.
- The login responses varied slightly in content length and status codes, indicating possible success/failure conditions.
- No valid credentials were obtained during the Burp Suite dictionary attack attempt, but the system showed susceptibility to automated login attacks without rate-limiting or account lockout protections.

---

### 🔹 Using Hydra

**Command used:**

```bash
hydra -L users.txt -P /usr/share/wordlists/rockyou.txt -s 8000 localhost http-post-form "/login:username=^USER^&password=^PASS^:Invalid credentials"
```

**Result:**

- The Hydra dictionary attack was successful.
- 160 valid username and password matches were found within approximately 6 seconds.
- This demonstrated that dictionary attacks with widely available wordlists such as rockyou.txt can easily compromise systems relying on weak password policies.

---

## 2. Performing a Non-Dictionary Attack via a Web Interface

### 🔹 Using Burp Suite

A non-dictionary brute-force attack was conducted using Burp Suite Intruder by generating numeric payloads (from 0000 to 9999).

- The payloads simulated brute-force attempts by incrementing numeric values for passwords.
- The attack was considerably slow, demonstrating that brute-force methods without optimization are not practical for strong passwords.
- No successful credentials were obtained, reinforcing the importance of implementing strong password policies and account lockout mechanisms to mitigate brute-force attempts.

---

### 🔹 Using Hydra

**Command used:**

```bash
hydra -L users.txt -x 4:6:1 -s 8000 localhost http-post-form "/login:username=^USER^&password=^PASS^:Invalid credentials"
```

**Result:**

- The non-dictionary brute-force attempt using numeric passwords between 4 to 6 digits was initiated.
- However, the application server failed to handle the concurrent login attempts and returned multiple connection errors.
- This outcome highlights that brute-force attacks without targeted optimization are resource-intensive, and server-side protections (such as connection throttling and session management) can effectively limit the success of such attacks.

---

## 3. Conclusion

Phase 2 Part 2 introduced more advanced attack simulations compared to previous exercises.

**Key observations:**

- Dictionary attacks using precompiled wordlists like rockyou.txt are extremely effective against systems using weak passwords.
- Non-dictionary brute-force attacks are inefficient without optimization and require significant computational resources.
- Real-world penetration testing must balance attack feasibility against system limitations and defenses.

**Recommendations for Developers:**

- Enforce complex password policies requiring a mix of characters and sufficient length.
- Implement account lockout mechanisms after several failed login attempts.
- Introduce CAPTCHA or other challenge-response tests to prevent automated attacks.
- Monitor and log authentication attempts for early detection of brute-force or credential stuffing activities.

By applying these countermeasures, systems can significantly reduce their exposure to dictionary and brute-force attacks.

