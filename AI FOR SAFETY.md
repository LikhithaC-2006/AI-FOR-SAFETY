# AI-FOR-SAFETY

# 🧾 Problem Statement:

<P>With the increasing number of phishing attacks and malicious websites, users often struggle to determine whether a URL is safe to click or visit. Many phishing URLs are designed to mimic legitimate websites, using misleading keywords, insecure protocols, or suspicious domain structures.</P>
<br>

# solution

The goal is to create a simple, no-library URL analyzer in Python that helps users identify potential red flags in a given URL. The script should:

Detect the presence and type of protocol (http or https)

Extract and display the domain, path, and query parameters

Check for the presence of suspicious keywords commonly used in phishing (e.g., "login", "secure", "bank")

Verify if the domain has a valid top-level domain (TLD)

Highlight if the domain uses an IP address or lacks a "www" prefix

Provide clear, user-friendly feedback without relying on external libraries

This tool aims to assist non-technical users or learners in understanding basic URL structures and identifying potentially unsafe links.<br><br>

# Code

    def analyze_url(url):
    
       print("\n🔍 Analyzing your URL...\n")

    suspicious_keywords = ["login", "secure", "verify", "update", "bank", "confirm"]
    valid_tlds = [".com", ".org", ".net", ".edu", ".gov", ".io", ".co"]

    # Add scheme if missing
    if not url.startswith("http://") and not url.startswith("https://"):
        print("ℹ️  No protocol found. Assuming 'http://'")
        url = "http://" + url

    # Identify protocol
    if url.startswith("https://"):
        protocol = "https"
        print("✅ Secure connection: HTTPS detected.")
    elif url.startswith("http://"):
        protocol = "http"
        print("⚠️  Insecure connection: Using HTTP.")
    else:
        protocol = "unknown"
        print("❌ Unknown protocol.")
    
    # Strip protocol from the URL
    address = url.split("://")[1]

    # Split domain and path
    if "/" in address:
        domain_and_portion = address.split("/", 1)
        domain = domain_and_portion[0]
        path = "/" + domain_and_portion[1]
    else:
        domain = address
        path = ""

    # Extract query params if any
    query = ""
    if "?" in path:
        path, query = path.split("?", 1)
        print(f"🧩 Query parameters found: {query}")
    else:
        print("ℹ️  No query parameters found.")

    # Display path
    if path:
        print(f"📂 Path detected: {path}")
    else:
        print("📁 No path in the URL.")

    # Check if domain looks valid
    has_tld = any(domain.endswith(tld) for tld in valid_tlds)
    if domain:
        print(f"🔸 Domain detected: {domain}")
        if has_tld:
            print(f"✅ Domain has a valid top-level domain.")
        else:
            print(f"⚠️  Domain may not have a valid top-level domain.")
    else:
        print("❌ No domain found.")

    # Check if "www" is included
    if "www." in domain:
        print("✅ 'www' prefix found in domain.")
    else:
        print("⚠️  'www' not found — might be a subdomain or custom domain.")

    # Check for suspicious keywords
    found_sus = []
    for word in suspicious_keywords:
        if word in url.lower():
            found_sus.append(word)
    if found_sus:
        print(f"🚨 Suspicious keywords found in URL: {', '.join(found_sus)}")
    else:
        print("✅ No suspicious keywords found in the URL.")

    print("\n🔎 URL Analysis Complete!\n")
    # Entry point
    print("🌐 Welcome to the Advanced URL Analyzer (No Libraries Edition) 🌐")
    user_input = input("Enter the URL to analyze: ").strip()
    analyze_url(user_input)


<br>
<br>

# example of secured output

![Screenshot 2025-04-16 235904](https://github.com/user-attachments/assets/6c781225-1953-498a-bf60-d7217d6679af)
<br>
<br>

# example of unsecured output

![Screenshot 2025-04-16 235930](https://github.com/user-attachments/assets/c3472a4b-6827-4f56-8d92-45e2981386cb)
