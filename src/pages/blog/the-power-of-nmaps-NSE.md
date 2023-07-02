---
layout: '../../layouts/Post.astro'
title: Unleashing the Power of Nmap's NSE - A Practical Guide
image: /images/sat-dish
publishedAt: "07-02-23"
category: 'Tools'
---

## What is NSE?

The Nmap Scripting Engine (NSE) is one of Nmap's most versatile and powerful features. It allows users to write (and share) simple scripts to automate a wide variety of networking tasks. Those scripts are written in Lua programming language. The scripts are used for more advanced network discovery, information gathering, and vulnerability detection.

## Practical Commands and Their Explanation

Before we dive into the practical commands, it's important to note that Nmap and its NSE should be used responsibly and ethically. Always ensure you have permission to scan the network or system you're targeting.

1. Basic NSE Usage: The basic syntax for running a script is nmap --script [script.nse] [target]. For example, to run the ssl-enum-ciphers script against the target example.com, you would use the command nmap --script ssl-enum-ciphers example.com. This script checks which SSL ciphers are supported by a server.

2. Using Multiple Scripts: You can specify multiple scripts by separating them with a comma: nmap --script [script1.nse],[script2.nse] [target]. For instance, nmap --script ssl-enum-ciphers,http-title example.com would run both the ssl-enum-ciphers and http-title scripts against example.com.

3. Script Categories: NSE scripts are divided into several categories, such as safe, intrusive, vuln, and exploit. To run all scripts in a category, use nmap --script "[category]" [target]. For example, nmap --script "vuln" example.com would run all scripts in the vuln category against example.com.

4. Script Arguments: Some scripts accept arguments for more specific tasks. These can be passed using --script-args. For example, nmap --script http-enum --script-args http-enum.displayall=true example.com runs the http-enum script with the displayall argument set to true.

![image](https://images.unsplash.com/photo-1483817101829-339b08e8d83f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1104&q=80)

## Use Cases

Let's look at a few practical use cases of NSE:

Detecting Vulnerabilities: The vuln category contains scripts that check for specific vulnerabilities. For example, to check if a server is vulnerable to the infamous Heartbleed bug, you could use nmap -p 443 --script ssl-heartbleed example.com.

Advanced Version Detection: While Nmap's -sV option can detect service versions, NSE can often provide more detailed information. For instance, nmap --script banner example.com will grab and display the banner of any services running on example.com.

Checking for Default Credentials: The http-default-accounts script checks for default web server credentials. For example, nmap --script http-default-accounts --script-args http-default-accounts.fingerprintfile=http-default-accounts-fingerprints.lua example.com would check example.com for default credentials.


## Advanced NSE Commands and Suggested Scripts

As you become more comfortable with Nmap and NSE, you can start to explore some of the more advanced commands and scripts that are available. Here are a few examples:

Running Scripts Against Multiple Targets: You can run scripts against multiple targets by specifying them in a text file (one target per line) and using the -iL option. For example, nmap --script ssl-enum-ciphers -iL targets.txt would run the ssl-enum-ciphers script against all targets listed in targets.txt.

Running Scripts with Timing Templates: Nmap offers six timing templates (from -T0 to -T5) that control the speed of your scan. For example, bash nmap --script ssl-enum-ciphers -T4 example.com would run the ssl-enum-ciphers script against example.com at a faster speed (but potentially less accurately).

Running Scripts with Output Files: You can save the output of your scan to a file using the -oN (normal), -oX (XML), -oG (grepable), or -oA (all) options. For example, nmap --script ssl-enum-ciphers -oN output.txt example.com would save the output of the scan to output.txt.

![image](https://images.unsplash.com/photo-1610457642191-05328cdf34ff?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTJ8fGFudGVubmF8ZW58MHx8MHx8fDA%3D&auto=format&fit=crop&w=500&q=60)

## More Suggested Scripts

The NSE library contains over 600 scripts, and more are being added all the time by the community. Here are a few notable scripts that you might find useful:

http-sql-injection.nse: This script checks if GET parameters in URLs are vulnerable to SQL injection. Use it with the command nmap --script http-sql-injection example.com.

http-vuln-cve2014-3704.nse: This script checks for the Drupalgeddon vulnerability (CVE-2014-3704) in Drupal sites. Use it with the command nmap --script http-vuln-cve2014-3704 example.com.

smb-vuln-ms17-010.nse: This script checks for the EternalBlue vulnerability (MS17-010) in Microsoft Windows. Use it with the command nmap --script smb-vuln-ms17-010 example.com.


Remember, these scripts are powerful tools, but they should be used responsibly and ethically. Always ensure you have permission to scan the network or system you're targeting.


Thanks for reading.