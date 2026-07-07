# Claude Code — References

A small, curated library of guides for working with [Claude Code](https://claude.com/claude-code),
published as a password-protected static site.

**Live site:** https://egongmidd.github.io/claude-code-references/

> 🔒 **The pages are encrypted.** Every page is protected with client-side AES encryption
> ([StatiCrypt](https://github.com/robinmoisson/staticrypt)) and only decrypts in the browser
> after the correct password is entered. The repository is public so GitHub Pages can serve a
> shareable link, but the **content is not readable without the password** — a visitor (or a
> search engine) sees only ciphertext. The access password is shared privately and is **not**
> stored in this repository.

## Contents

| Page | Path | What it is |
| --- | --- | --- |
| Library home | `index.html` | Landing page listing every guide. Share **this** link. |
| A Quick Start for New Faculty | `quickstart.html` | Setting up Claude Code + eight real teaching use cases. |

Hand out the **root link** (the library home), not a deep link to an individual page — that way
readers always land on the hub and see anything added later.

## How it works

- Each page is a self-contained HTML file (all CSS inline; no external dependencies).
- Files are encrypted in place with StatiCrypt, using a shared salt (`.staticrypt.json`) so a
  single unlock covers every page in the library.
- `.nojekyll` tells GitHub Pages to serve the files as-is.
- Editable **plaintext sources** are kept privately outside this repo; only the encrypted
  output is committed here.

## Maintaining the library

Adding or updating a resource (run from the repo root; replace `<password>` with the shared one):

```bash
# 1. Add the new plaintext page as e.g. new-resource.html, and add a card linking
#    to it on the library home (index.html).

# 2. Re-encrypt every page with the shared password (shared salt = one unlock for all):
npx staticrypt index.html quickstart.html new-resource.html \
  -p "<password>" --short --remember 30 -d .

# 3. Publish:
git add -A && git commit -m "Add <resource>" && git push origin main
```

GitHub Pages rebuilds automatically after each push (usually within a minute).

### Rotating the password

Re-run the StatiCrypt command above with a new password, commit, and push. Then share the new
password with readers. (The old password stops working once the re-encrypted pages are live.)

---

Maintained by [@egongmidd](https://github.com/egongmidd). Access is by password only.
