# Globomantics Vulnerable App

A deliberately vulnerable Express.js application designed for testing and demonstrating CodeQL security queries. This repo demonstrates how a project can consume a centrally governed CodeQL query pack from GitHub Container Registry.

## ⚠️ WARNING

This application contains **INTENTIONAL SECURITY VULNERABILITIES** for educational purposes. **DO NOT** deploy in a production environment.

## 🔍 Purpose

This app serves as a test bed for the [Globomantics JavaScript Security Query Pack](https://github.com/timothywarner-org/globomantics-secure-scan), showcasing how CodeQL can identify common security issues in JavaScript applications.

The project demonstrates a complete security scanning solution:
1. The vulnerable app with intentional security flaws
2. A GitHub Actions workflow that uses a custom CodeQL query pack from GHCR
3. Scripts to run CodeQL analysis locally

## 🔐 Vulnerabilities

This application contains the following intentional vulnerabilities:

1. **Code Injection (CWE-94)**: The `/calculate` endpoint uses `eval()` to execute user-provided JavaScript code without proper validation.

2. **HTTP Header Injection (CWE-113)**: The `/redirect` endpoint places user input directly into HTTP headers without sanitization.

3. **Insecure Randomness (CWE-338)**: The `/generate-token` endpoint uses `Math.random()` for security-sensitive operations like token generation.

4. **Information Exposure (CWE-200)**: The error handler exposes sensitive stack traces to users.

5. **Hard-coded Secrets (CWE-798)**: The session configuration uses a hard-coded secret key.

## 📋 Installation

```bash
# Clone the repository
git clone https://github.com/timothywarner-org/globomantics-vulnerable-app.git

# Change to the project directory
cd globomantics-vulnerable-app

# Install dependencies
npm install

# Start the application
npm start
```

## 🚀 Usage

The application runs on `http://localhost:3000` by default and provides an interactive web interface to test the vulnerabilities:

- **Code Injection**: Try entering JavaScript expressions in the calculator form
- **HTTP Header Injection**: Test the redirect functionality with header injection attempts
- **Insecure Randomness**: Generate tokens using insecure randomness methods

## 🔎 Testing with CodeQL

### Automated Analysis with GitHub Actions

This repository includes a GitHub Actions workflow that automatically runs the custom CodeQL queries against the codebase. The workflow:

1. Uses the GitHub CodeQL action to initialize a CodeQL environment
2. Pulls the custom query pack from the GitHub Container Registry
3. Runs the analysis and uploads results to GitHub Advanced Security

### Local Testing

For local testing, use the provided scripts:

```bash
# On Linux/macOS
./test-codeql.sh

# On Windows
test-codeql.bat
```

These scripts:
1. Create a CodeQL database for the application
2. Run each query individually to detect specific vulnerabilities
3. Run the complete security suite
4. Generate SARIF files with the results

## 📚 Educational Purpose

This repository is part of the GitHub Enterprise Cloud training materials created by Tim Warner for Pluralsight. It showcases how organizations can leverage GitHub Advanced Security with custom CodeQL query packs to enhance their security posture.

## 📄 License

MIT 