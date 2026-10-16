# Experiment 9: Password Hashing and Salting

| Detail | Information |
|---|---|
| Student | P Ganesh |
| Course | Cryptography — CSL0509 |
| Programme | B.Tech AIML, V Semester |
| Faculty | Mr. Hirendra Singh Sengar |
| Academic year | 2026–27 |

**Evidence status:** All three methods and a small dictionary comparison executed. VS Code screenshots are pending.

## Aim

Compare unsalted SHA-256, salted SHA-256 and a password-specific derivation function, scrypt, using synthetic passwords.

## Run

```powershell
python Exp09_Password_Hashing/main.py
```

This experiment only needs Python's standard library. Run it in VS Code for the assignment's environment evidence.

## Procedure and algorithm

1. Hash the same sample password for two accounts with SHA-256; the hashes match.
2. Generate two independent 16-byte random salts and hash `salt || password`; the hashes differ.
3. Try a five-entry synthetic dictionary against both hash methods. The correct weak password is recovered in both cases because the salt is public and does not stop guessing.
4. Derive a 32-byte scrypt hash with N=16384, r=8, p=1. Store the parameters and salt with the hash in a real application.
5. Verify the correct password using a constant-time comparison and reject a wrong password.
6. Repeat the small dictionary experiment with scrypt, and measure the local time.

## Observations

- Unsalted equality leaks password reuse and permits reuse of precomputed guesses.
- Unique salts prevent identical passwords from yielding identical stored values and require per-salt work.
- Fast salted SHA-256 is still unsuitable as a password storage design.
- Scrypt makes guesses costlier through CPU and memory work, but a weak password in the dictionary was still found.
- A second synthetic sample was not in the five-entry dictionary. That result does not measure its overall strength or prove resistance to larger attacks.

Timing values in `summary.json` are local observations, not universal cracking-time estimates. The selected scrypt cost is a lab parameter; production systems must choose and benchmark a current password-storage policy.

## Required screenshots to finish the submission

These are the captures still needed from the specified tool. Do not rename a rendered log image as a tool screenshot.

- [ ] `01_VSCode_Hashing.png` — source and interpreter
- [ ] `02_Salt_Comparison.png` — same password with/without distinct salts
- [ ] `03_Dictionary_Comparison.png` — dictionary results, scrypt cost and verification

Store the captures in a `screenshots` subfolder and add relative image links after the actual files exist.

## Recorded execution evidence

[Full execution log](results/execution.txt) · [Machine-readable results](results/summary.json)

The image below is a **rendered extract of the actual execution log**, not a screenshot of CrypTool, VS Code, Kali or Wireshark.

![Rendered execution log](results/execution_log.png)

## References

- [Python hashlib key derivation](https://docs.python.org/3/library/hashlib.html#key-derivation)
- [scrypt specification](https://www.rfc-editor.org/rfc/rfc7914)
