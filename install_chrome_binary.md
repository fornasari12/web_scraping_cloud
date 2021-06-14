# Install chromedriver binary version.
Downloads and installs the chromedriver binary version 92.0.4515.43 for automated testing of webapps. The installer supports Linux, MacOS and Windows operating systems.

1. Install [Certifi](https://pypi.org/project/certifi/):

Certifi provides Mozilla’s carefully curated collection of Root Certificates for validating the trustworthiness of SSL certificates while verifying the identity of TLS hosts. It has been extracted from the Requests project.

```python
pip install certifi
```

2. Set appropiate variables.

[StackOverflow tread](https://stackoverflow.com/questions/40684543/how-to-make-python-use-ca-certificates-from-mac-os-truststore/57795811#57795811)

Run this to set the appropriate variables. This is a combination of the answers that have already been given here. Put it in your ~/.bash_profile to make it permanent.

```shell
CERT_PATH=$(python -m certifi)
export SSL_CERT_FILE=${CERT_PATH}
export REQUESTS_CA_BUNDLE=${CERT_PATH}
```

3. Install chromedriver-binary

```python
pip install chromedriver-binary
```
