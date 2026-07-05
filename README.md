# APIX

> API Security Testing Toolkit — endpoint fuzzing, method checks, authentication probes, and JSON-aware reporting.

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)
![Category](https://img.shields.io/badge/Category-API%20Testing-8b5cf6?style=flat-square)
![Status](https://img.shields.io/badge/Interface-Direct%20CLI-brightgreen?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)

---

## Overview

APIX helps test APIs during authorized assessments.

It focuses on discovery and validation rather than exploitation. The direct CLI interface replaces old interactive flows and provides consistent output for reports.

---

## Features

- Endpoint fuzzing.
- HTTP method testing.
- Authentication header checks.
- JWT metadata inspection.
- CORS checks.
- JSON response analysis.
- Rate-limit observations.
- Clean console output.
- JSON/TXT report support.

---

## Installation

```bash
git clone https://github.com/NeiveZ/APIX.git
cd APIX
chmod +x apix.sh
./apix.sh --install
```

Validate:

```bash
./apix.sh --check
```

Run tests if available:

```bash
python3 -m pytest -q
```

---

## Usage

```bash
./apix.sh <command> [options]
```

Help:

```bash
./apix.sh --help
```

---

## Commands

### Endpoint fuzzing

```bash
./apix.sh fuzz -u https://api.example.com -w wordlists/api.txt
```

With methods:

```bash
./apix.sh fuzz -u https://api.example.com -w wordlists/api.txt --methods GET,POST,PUT,DELETE
```

### Authentication check

```bash
./apix.sh auth -u https://api.example.com/me --token "$TOKEN"
```

### CORS check

```bash
./apix.sh cors -u https://api.example.com
```

### JWT inspection

```bash
./apix.sh jwt --token "$JWT"
```

### Full API review

```bash
./apix.sh full -u https://api.example.com -w wordlists/api.txt --json --txt --out reports/api_review
```

---

## Recommended Procedure

1. Identify base URL:

```bash
./apix.sh probe -u https://api.example.com
```

2. Fuzz endpoints:

```bash
./apix.sh fuzz -u https://api.example.com -w wordlists/api.txt
```

3. Test methods on discovered endpoints:

```bash
./apix.sh methods -u https://api.example.com/users
```

4. Test authentication behavior:

```bash
./apix.sh auth -u https://api.example.com/me --token "$TOKEN"
```

5. Save evidence:

```bash
./apix.sh full -u https://api.example.com -w wordlists/api.txt --json --txt --out reports/apix
```

---

## Output Example

```text
APIX Assessment Summary

Target       https://api.example.com
Command      fuzz
Endpoints    128
Findings     6

Severity     Endpoint              Check             Detail
INFO         /health               Status            200 OK
LOW          /debug                Exposure          Endpoint exists
MEDIUM       /admin                Auth              401 without token
```

---

## Reports

```bash
--json
--txt
--out <path_without_extension>
```

Example:

```bash
./apix.sh full -u https://api.example.com --json --txt --out reports/api
```

---

## Troubleshooting

### SSL issues

```bash
./apix.sh probe -u https://api.example.com --insecure
```

### Timeout

```bash
./apix.sh fuzz -u https://api.example.com -T 15
```

### Rate limits

Use delay:

```bash
./apix.sh fuzz -u https://api.example.com --delay 250
```

---

## Ethics

Use only against APIs you own or are authorized to test.

---

## License

MIT License.
