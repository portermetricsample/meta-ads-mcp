# Security policy

## Reporting a vulnerability

**Do not open a public issue for a security problem.**

Email **security@portermetrics.com** with:

- What you found
- How to reproduce it
- What an attacker could do with it

You will get an acknowledgement within two business days.

## What belongs here

This repository contains documentation only — no executable code ships from it. Security reports that belong here are:

- A configuration example in `configs/` that would expose a credential
- Documentation that instructs a reader to do something unsafe
- A link in these files pointing somewhere it should not

## What belongs to Porter

Anything about the hosted MCP server itself — authentication, the OAuth flow, data access between accounts, the API — goes to **security@portermetrics.com** directly, not through this repository.

## Credentials

Nothing in this repository should ever contain an API key, access token, account identifier tied to a real business, or ad account data. If you find one, report it as above and we will rotate and remove it.
