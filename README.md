# Overview

I evaluated the application’s OAuth account linking functionality to determine whether it was vulnerable to cross-site request forgery. During testing, I identified a forced OAuth profile linking flaw caused by the absence of CSRF protections in the OAuth flow. By capturing and reusing a valid authorization code, I was able to trick a privileged user into linking my social media account to their profile. This allowed me to authenticate as the admin and perform privileged actions, including deleting user accounts. This project demonstrates how insecure OAuth linking implementations can lead to full account takeover.

# Methodology

Step 1: Linked a personal social media account to a low-privilege user account and intercepted the OAuth flow.

Step 2: Analyzed the authorization request and confirmed that the state parameter was missing, indicating a lack of CSRF protection.

Step 3: Captured a valid OAuth authorization code and prevented it from being consumed.

Step 4: Crafted a malicious request that reused the stolen authorization code.

Step 5: Delivered the request to the admin via a CSRF vector, causing their browser to complete the OAuth linking flow.

Step 6: Logged in using the linked social media account and verified access to the admin panel.

Step 7: Performed privileged actions to confirm full account compromise.

# Conclusion

This assessment confirmed a high-severity forced OAuth profile linking vulnerability caused by missing CSRF defenses in the OAuth implementation. The findings highlight the importance of enforcing state validation, single-use authorization codes, and robust protections around third-party account linking to prevent account takeover through OAuth abuse.
