# Data and backend engineering interview

Start with [TASK.md](TASK.md). The exercise is PDF in, JSON out, using synthetic PDFs and a real measurement vocabulary. The [glossary appendix](TASK.md#appendix-glossary) explains the terms needed for extraction.

## Setup

From the repository root, unpack the vocabulary once:

```sh
unzip -o vocabulary/loinc.zip -d vocabulary
```

Choose a starter:

- [TypeScript](starter-ts/README.md): Node.js 24.13 or newer and pnpm 10.
- [Python](starter-py/README.md): Python 3.11 or newer; the core starter uses only the standard library.

Both provide project configuration and a blank entry point. Choose your program structure, libraries, and input handling. You may use another language or setup. If you want Gemini access, ask the interviewer for an interview-only environment file.

The compressed vocabulary is about 3 MB; the extracted SQLite is about 11 MB and is ignored by Git. The source version and LOINC notice are in [vocabulary/README.md](vocabulary/README.md).

## Files

- `TASK.md`: task, output contract, interview format, and glossary appendix.
- `pdfs/`: three visible synthetic PDFs and their identifier manifest.
- `vocabulary/`: compressed SQLite and source notice.
- `starter-ts/`: minimal TypeScript environment and blank entry point.
- `starter-py/`: minimal Python environment and blank entry point.
