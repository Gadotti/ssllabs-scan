# SSL Labs Scan

[![githubactions](https://github.com/kyhau/ssllabs-scan/workflows/Build-Test/badge.svg)](https://github.com/kyhau/ssllabs-scan/actions)
[![travisci](https://travis-ci.org/kyhau/ssllabs-scan.svg?branch=master)](https://travis-ci.org/kyhau/ssllabs-scan)
[![codecov](https://codecov.io/gh/kyhau/ssllabs-scan/branch/main/graph/badge.svg)](https://app.codecov.io/gh/kyhau/ssllabs-scan/tree/main)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](http://en.wikipedia.org/wiki/MIT_License)

Support Python 3.7, 3.8, 3.9, 3.10.

This tool calls the SSL Labs [API v3](https://github.com/ssllabs/ssllabs-scan/blob/master/ssllabs-api-docs-v3.md) to do SSL testings on servers.

ℹ️ Please note that the SSL Labs Assessment API has access rate limits. You can find more details in the sections "Error Response Status Codes" and "Access Rate and Rate Limiting" in the official [SSL Labs API Documentation](https://github.com/ssllabs/ssllabs-scan/blob/master/ssllabs-api-docs-v3.md). Some common status codes are:
- 400 - invocation error (e.g., invalid parameters)
- 429 - client request rate too high or too many new assessments too fast
- 500 - internal error
- 503 - the service is not available (e.g., down for maintenance)
- 529 - the service is overloaded

---
## Input and Output

Sample input: [sample/SampleServerList.txt](sample/SampleServerList.txt)

1. summary.html (sample output: [sample/summary.html](https://kyhau.github.io/ssllabs-scan/sample/summary.html))
1. summary.csv (sample output: [sample/summary.csv](sample/summary.csv))
1. _hostname_.json (sample output: [sample/google.com.json](sample/google.com.json))

**Sample html output:**
![alt text](sample/SampleHtmlOutput.png "Sample html output")

You can change the report template and styles in these files:
- [ssllabsscan/report_template.py](./ssllabsscan/report_template.py)
- [ssllabsscan/styles.css](./ssllabsscan/styles.css)


---
## Build and Run

### Linux
```
# Create and activate a new virtual env (optional)
virtualenv env
. env/bin/activate

# Install and run
pip install -e .
ssllabs-scan sample/SampleServerList.txt
```

### Windows
```
# Create and activate a new virtual env (optional)
virtualenv env
env\Scripts\activate

# Install and run
pip install -e .
ssllabs-scan sample\SampleServerList.txt
```

### Example console output
```
$ ssllabs-scan sample/SampleServerList.txt
Start analyzing duckduckgo.com...
Status: DNS, StatusMsg(Resolving domain names): waiting 30 secs until next check...
Status: IN_PROGRESS, StatusMsg(None): waiting 30 secs until next check...
Status: IN_PROGRESS, StatusMsg(None): waiting 30 secs until next check...
Start analyzing google.com...
Status: DNS, StatusMsg(Resolving domain names): waiting 30 secs until next check...
Status: IN_PROGRESS, StatusMsg(None): waiting 30 secs until next check...
Status: IN_PROGRESS, StatusMsg(None): waiting 30 secs until next check...
Status: IN_PROGRESS, StatusMsg(None): waiting 30 secs until next check...
Status: IN_PROGRESS, StatusMsg(None): waiting 30 secs until next check...
Status: IN_PROGRESS, StatusMsg(None): waiting 30 secs until next check...
Status: IN_PROGRESS, StatusMsg(None): waiting 30 secs until next check...
Creating summary.html ...
```

## Tox Tests and Build the Wheels

```
pip install -r requirements-build.txt
tox -r
```
