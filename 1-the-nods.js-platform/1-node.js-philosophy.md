## Node.js Philosophy

- Every programming platform has its own **philosophy**.
- Node.js philosophy is a set of principles, guidelines, and ideas used by the community.
- These ideas come from:
  - the technology itself
  - the ecosystem
  - community trends
  - the larger JavaScript movement
- Some guidelines come from **Ryan Dahl**, others from core contributors and the community.
- These are not strict rules — use them with **pragmatism**.
- They can help when you design your software.

---

## Small Core

- Node.js keeps a **small core**.
- The core includes the runtime and built-in modules.
- Most extra features are left to **userland / userspace**.
- This allows the community to experiment and build new solutions quickly.
- A smaller core is easier to **maintain**.
- Recently, Node.js has added more built-in features as they became stable.
- Examples include **command-line argument parsing**, **WebSockets**, **unit testing**, **file watch**, **file globbing**, and **fetch API**.
- This change shows Node.js evolving while keeping the same core idea.

---

## Small Modules

- A **module** is the fundamental way Node.js structures code.
- Node.js encourages **small modules** with a limited scope.
- This idea comes from the **Unix philosophy**:
  - “**Small is beautiful**.”
  - “**Make each program do one thing well**.”
- Package managers like **npm**, **pnpm**, and **yarn** support this style.
- Node.js handles **dependency hell** by allowing different versions of the same package to coexist.
- Example:
  - `depA` depends on `depC@1.0.0`
  - `depB` depends on `depC@2.0.0`
  - Node.js installs both versions separately to avoid conflicts.
- Small modules are:
  - easier to **understand**
  - simpler to **test** and **maintain**
  - **lightweight** for browser and serverless use
- Small modules enable high levels of **reusability**.
- But more third-party dependencies can increase **supply chain risk**.
- Always check if a dependency is necessary and well-maintained.

---

## Small Surface Area

- Good Node.js modules expose a **small surface area**.
- A minimal API is clearer and less error-prone.
- Many modules expose only one thing: a **function** or a **class**.
- Prefer modules that are meant to be **used, not extended**.
- Hiding internals makes modules easier to implement and maintain.

---

## Simplicity and Pragmatism

- Node.js follows the **KISS** principle: Keep It Simple, Stupid.
- It also follows the idea of “**worse is better**.”
- Simple design is often better than trying to be perfect.
- Simple code usually:
  - takes less effort to implement
  - ships faster
  - is easier to adapt
  - is easier to maintain
  - is easier to understand
- JavaScript supports practical designs with **simple classes**, **functions**, and **closures**.
- Avoid overly complex class hierarchies.
- Practical solutions often work better than perfect abstractions.
- This is about balancing **complexity** and **clarity**.

---

## Takeaway

- Node.js philosophy values:
  - a **small core**
  - **small modules**
  - a **small API surface**
  - **simplicity**
  - **pragmatism**
- These ideas should guide your work, but not become strict rules.
