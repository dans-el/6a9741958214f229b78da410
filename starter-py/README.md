# Python starter

Use Python 3.11 or newer. From this folder:

```sh
python3 main.py
```

`main.py` is blank apart from a comment, so running it initially produces no output. Build your solution here or choose another structure. The input and JSON requirements are in [TASK.md](../TASK.md). The vocabulary is `../vocabulary/loinc.sqlite` after unpacking it as described in the root README. Python's standard library includes SQLite support.

## Optional Gemini access

If you choose Gemini, install the optional SDK and environment-file dependency:

```sh
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -e ".[gemini]"
```

Ask the interviewer for an interview-only key or a prepared `.env` file. If `.env` does not already exist, copy `.env.example` to `.env` and fill in the key. The optional `python-dotenv` dependency can load it in your code; the blank entry point does not load it automatically. Keep it out of Git.

Choose your extraction libraries, program structure, and tests. No extraction or matching implementation is supplied.
