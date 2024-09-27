# Email Analysis Lab: The Planet's Prestige

## Project Overview

This lab focuses on analyzing a phishing email from a Capture The Flag (CTF) scenario called "The Planet's Prestige" on Blue Team Cyber Range. We will investigate the email headers, extract attachments, and identify indicators of compromise (IOCs) to understand the nature of the phishing attempt.

## Setup

1. **Create an Account on Blue Team Labs Online:**
   - Go to [Blue Team Labs Online](https://blueteamlabs.online).
   - Create an account if you haven't already.
   - Navigate to the "Challenges" section and search for "Planet."
   - Select the challenge: **The Planet's Prestige**.

2. **Download and Extract the Email File:**
   - Download the email file provided in the challenge.
   - Extract it using the password `BT` (all lowercase):
     ```bash
     unzip email.zip -P BT
     ```
   - Verify the extracted file:
     ```bash
     ls
     # Output: email.eml
     ```

3. **Tools Used:**
   - **Notepad++**: For viewing and editing the email file.
   - **CyberChef**: For decoding and analyzing encoded email content.
   - **HxD**: For viewing files in hexadecimal format.
   - **7-Zip**: For extracting compressed files.

## Email Header Analysis

1. **Open the Email File:**
   - Use Notepad++ to open and view the email headers:
     ```bash
     notepad++ email.eml
     ```

2. **Analyze Key Header Fields:**
   - **Received Fields:** Trace the path the email took from the sender to the recipient.
   - **Return Path:** Check the address used if the email fails to send.
   - **Authentication Results:** Verify SPF, DKIM, and DMARC status to identify potential spoofing.
   - **Reply-To:** Verify if the `Reply-To` address matches the `From` address, indicating potential phishing attempts.

3. **Extract Encoded Content:**
   - Copy the Base64 encoded content found in the email body and decode it using CyberChef:
     ```bash
     # Use CyberChef's 'From Base64' function to decode the content.
     ```
   - Save the decoded content as a `.txt` file for further analysis.

## Attachment Analysis

1. **Identify and Extract Attachments:**
   - Locate the attachment in the email (e.g., `puzzle_to_canda.pdf`) and verify its file type using CyberChef or HxD.

2. **Analyze File Signature:**
   - Check the file signature to confirm the file type. For example:
     ```bash
     # First few bytes of the file: 50 4B 03 04 (indicating a .zip file)
     ```

3. **Rename and Extract Attachments:**
   - Rename and extract files from the attachment:
     ```bash
     # Rename file to .zip and extract using 7-Zip or similar tools.
     ```
   - Analyze the extracted files for hidden content or additional indicators.

4. **Examine Extracted Files in Hex Format:**
   - Use HxD to view the first few bytes of each file and identify the correct file type.

## File Metadata Analysis

1. **Analyze File Metadata with ExifTool:**
   - Check for author and modification details in the file metadata:
     ```bash
     exiftool -a -u -g1 email.eml
     ```
   - Look for potential clues left by the attacker, such as author names or timestamps.

## Findings

1. **Email Analysis Summary:**
   - The email originated from a fake mailer service `mk.cz` and was sent to the recipient `major.onar@gmail.com`.
   - **Reply-To:** The email had a different `Reply-To` address (`pastor.com`), indicating a potential phishing attempt.

2. **Attachment Analysis Summary:**
   - The attached file was a `.zip` file containing three items: a JPEG image, a PDF, and an Excel file.
   - The Excel file contained a hidden Base64 encoded message revealing the attacker's location.

3. **Indicators of Compromise (IOCs):**
   - **Sender Domain:** `mk.cz` (Fake email service).
   - **Phishing Domain:** `pure.com` (Potential Command and Control).
   - **Malicious File:** `puzzle_to_canda.zip` containing hidden messages.

## Conclusion

This lab demonstrated the process of analyzing a phishing email by examining email headers, extracting and analyzing attachments, and identifying IOCs. Understanding email analysis techniques is crucial for SOC analysts to detect and mitigate phishing attacks.

## Resources

- [Blue Team Labs Online](https://blueteamlabs.online)
- Tools used: `Notepad++`, `CyberChef`, `HxD`, `ExifTool`
- [VirusTotal](https://www.virustotal.com)

## Notes

Always conduct email analysis in a controlled environment. Do not open or interact with suspicious emails or attachments on your local machine.

---

Simply copy and paste this content into a `README.md` file in your GitHub repository. Adjust any sections as needed based on your specific findings or personal preferences.
