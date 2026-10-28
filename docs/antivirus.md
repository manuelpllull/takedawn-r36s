# Antivirus warnings on Windows

Some antivirus tools flag the Windows download. This is a false positive. This page explains why it happens and how to check the file yourself.

## Why it happens

The Windows build is not code-signed. Code signing needs a paid certificate tied to a legal identity, and this project runs under a handle, so the binaries ship unsigned. The installer is also built with Inno Setup, which many machine-learning scanners treat as suspicious, because installers unpack and write files the way some malware droppers do.

An unsigned installer plus a freshly compiled binary on each release is enough for a few heuristic engines to guess "malicious", even when there is nothing malicious in the file. The guess shifts from build to build: one release scores clean, the next trips two or three engines.

## How to tell it is a false positive

- Most engines pass it. On the last release, 56 of 59 scanners on VirusTotal reported the file as clean, including every major signature-based product.
- The engines that flag it give generic machine-learning verdicts (names like "MALICIOUS" or "ML.Attribute.HighConfidence"), not a specific malware family.
- The code is open source. You can read it and build the same binaries yourself.

## What you can do

- Check the file's SHA-256 against the hash on the release page before you run it.
- If your scanner blocks it, allowlist the file or build from source.
- Report the false positive to your antivirus vendor. Those reports are what get the detection removed.

## What we do

We report the false positives to the flagging vendors after each release. Signing the Windows binaries would prevent most of these warnings; that is a separate decision, because of the certificate and identity it requires.
