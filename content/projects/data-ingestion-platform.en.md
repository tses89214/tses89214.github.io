+++
title = 'Data Ingestion Platform: Letting Non-Technical Teams Contribute Data'
date = '2025-03-11'
draft = false
description = 'Marketing, sales and operations upload CSVs; the platform validates them against schemas the data team maintains.'
tags = ['Data Engineering', 'Data Quality', 'Docker']
+++

**The problem:** departments without technical staff have data, but no simple, reliable way to hand it to the data team. The usual result is inconsistent formats and wrong columns, and a lot of back and forth.

**What I built:** a web interface where a department uploads a CSV. The data team maintains the expected schema for each table; the platform validates the upload, shows a preview, and reports success or failure clearly. Different tables can have different schemas, and the whole thing starts with one Docker Compose command.

**Limits (listed honestly in the README):** this is a proof of concept. It currently validates only the first ten rows, supports a limited set of types (str, int, float, datetime, date), stores files locally, and has no account management. Next steps would be full-file validation, cloud storage and access control.

Stack: Python, Docker Compose.

**Links:** [GitHub repo](https://github.com/tses89214/Data-Ingestion-Platform)
