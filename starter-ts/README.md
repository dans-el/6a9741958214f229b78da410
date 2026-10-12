# TypeScript starter

Use Node.js 24.13 or newer and pnpm 10. From this folder:

```sh
pnpm install --frozen-lockfile
pnpm check
pnpm start
```

`src/index.ts` is blank apart from a comment, so running it initially produces no output. Build your solution here or choose another structure. The input and JSON requirements are in [TASK.md](../TASK.md). The vocabulary is `../vocabulary/loinc.sqlite` after unpacking it as described in the root README.

## Optional Gemini access

The Google Gen AI SDK is installed for convenience if you choose Gemini. Ask the interviewer for an interview-only key or a prepared `.env` file. If `.env` does not already exist, copy `.env.example` to `.env` and fill in the key. `pnpm start` loads the local `.env` when present. Keep it out of Git.

Choose your extraction libraries, program structure, and tests. No extraction or matching implementation is supplied.
