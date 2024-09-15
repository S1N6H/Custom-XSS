**Custom-XSS Tool**
Version: 1.2.0

**Author: Singh <3**

**Overview**
Custom-XSS is a Bash-based tool designed to automate XSS (Cross-Site Scripting) vulnerability hunting. The tool leverages multiple sources like Waybackurls, gau, and gf to collect URLs and identify potential XSS vulnerabilities. The tool can also integrate Blind XSS payloads for extensive testing and report generation.

**Features**
Fetch URLs from Wayback Machine and gau.
Filter and identify potential XSS vulnerable URLs using GF Patterns.
Support for Blind XSS payload injection.
Automate XSS scanning using Dalfox.
Save and organize results in structured directories.

Prerequisites
To run Custom-XSS, you need to have the following tools installed on your system:

Waybackurls-https://github.com/tomnomnom/waybackurls

gau-https://github.com/lc/gau

gf-https://github.com/tomnomnom/gf

Dalfox-https://github.com/hahwul/dalfox



**Installation**
Clone this repository:
git clone https://github.com/yourusername/Custom-XSS.git

Navigate to the project directory:
cd Custom-XSS

Make the script executable:
chmod +x Custom-XSS.sh

Install dependencies:
sudo apt-get install waybackurls gau gf dalfox



**Usage**
The tool provides flexibility in its usage by allowing the user to run various configurations based on the domain, output preferences, and Blind XSS payloads.

./Custom-XSS.sh -d <target.com>
./Custom-XSS.sh -d <target.com> -b <blindxss.xss.ht>
./Custom-XSS.sh -d <target.com> -o <outputfile.txt>
./Custom-XSS.sh -d <target.com> -b <blindxss.xss.ht> -o <outputfile.txt>


**Command-line Arguments**
Argument	Description
-d, --domain	The target domain to perform XSS scanning on. (required)
-b, --blind	The Blind XSS payload URL to be injected for testing. (optional)
-o, --output	The file to store results. Defaults to results.txt if not specified.
-h, --help	Display the help message.
-v, --version	Display the current version of the tool.



**Example**
./Custom-XSS.sh -d example.com -b blindxss.example.ht -o xss_results.txt
In this example:

The script scans example.com for potential XSS vulnerabilities.
It injects the provided Blind XSS payload (blindxss.example.ht) during the scanning process.
The results are saved in xss_results.txt.

How It Works
1. Directory Setup
The tool first creates a directory structure under the results/ folder to organize output. If a directory for the target domain already exists, the tool exits with an error message.

2. URL Collection
The tool fetches URLs using:

Waybackurls: Collects archived URLs from the Wayback Machine.
gau: Fetches URLs using Google Dorking and AlienVault data.
3. XSS Vulnerability Filtering
It applies gf patterns to filter and identify URLs that are potentially vulnerable to XSS. All the possible XSS endpoints are saved in a temporary file and deduplicated.

4. XSS Scanning
The tool uses Dalfox for scanning XSS vulnerabilities in the identified endpoints:

If a Blind XSS payload is provided, it injects the payload into the parameters and generates a report.
Otherwise, it performs a standard XSS scan using Dalfox.
5. Results
After completion, the final results are stored inside the results/<domain> directory. You can find the XSS findings in the specified output file or the default results.txt.
