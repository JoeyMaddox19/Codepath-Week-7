# Project 7 - WordPress Pentesting

Time spent: 8 hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. (Required) Vulnerability Name or ID: Unauthenticated Stored Cross-Site Scripting (XSS)
  - [ ] Summary: Made a comment that was very long (>64 kb). The length caused the comment to be truncated when inserted into the database. This truncation lead to a malformed HTML generated on the page. For demonstration purposes, I created a simple alert pop up on the page. 
    - Vulnerability types: Cross-Site Scripting (XSS)
    - Tested in version: 4.2
    - Fixed in version: 4.2.1
  - [ ] GIF Walkthrough: ![Alt Text](https://github.com/JoeyMaddox19/Codepath-Week-7/blob/master/Vuln_3.gif)
  - [ ] Steps to recreate: View the webpage as an unauthorized user. Enter a comment with an XSS alert followed by  AAAAAAAAAAAA...[64 kb]..AAA where the AAAAAAAAA is repeated for at least 64kb. Upon entering the comment, an alert box will pop up. 
  - [ ] Affected source code:
    - [Link 1](https://wpvulndb.com/vulnerabilities/7945)

2. (Required) Vulnerability Name or ID: Authenticated Cross-Site Scripting (XSS)
  - [ ] Summary: As an editor, it is possible to create an XSS attack against other users by saving a post containing an XSS attack as a draft. When other users attempt to preview this draft, the Javascript in the post will run the XSS attack.
    - Vulnerability types: Cross-Site Scripting (XSS)
    - Tested in version: 4.2
    - Fixed in version: 4.2.6
  - [ ] GIF Walkthrough: ![Alt Text](https://github.com/JoeyMaddox19/Codepath-Week-7/blob/master/Vuln_1.gif)
  - [ ] Steps to recreate: Login to the admin portion of of the WordPress as an editor. Create a post containing an XSS attack such as:  <img src=1 onerror=alert('XSS')>. Save this post as a draft. When another user previews this post, and the image fails to load, an alert will be triggered.  
  - [ ] Affected source code:
    - [Link 2](https://github.com/WordPress/WordPress/commit/7ab65139c6838910426567849c7abed723932b87)

3. (Required) Vulnerability Name or ID: Authenticated Stored Cross-Site Scripting (XSS) in YouTube URL Embeds
  - [ ] Summary: Simple comments alone often are altered before they are actually posted (WordPress protects against basic Cross-Site Scripting attacks). However, embedded comments are not monitored as closely. The embedded comments are checked with many regular expressions to find out what the proper handling method is. Sucuri blog found that the youtube url has vulnerabilities. The handler takes the youtube URL and simply concatenates the rest of the embedded text. Since the autoembed function is unable to create a link, it returns the URL as typed. However, due to the sanitization property of the parsing function, the returned URL will be cleaned. However, the shortcode parsing function has escape functions, and thus, the attack uses the required XSS attribute values and then an escape function to escape from the parsing method. 
    - Vulnerability types: Cross-Site Scripting (XSS)
    - Tested in version: 4.2
    - Fixed in version: 4.2.13
  - [ ] GIF Walkthrough: ![Alt Text](https://github.com/JoeyMaddox19/Codepath-Week-7/blob/master/Vuln_2.gif)
  - [ ] Steps to recreate: Log in to the admin page as an editor. Edit one of the pages to include the embedded youtube url link: [embed src='https://youtube.com/embed/test\x3csvg onload=alert(1)\x3e'][/embed]
  - [ ] Affected source code:
    - [Link 3](https://github.com/WordPress/WordPress/commit/419c8d97ce8df7d5004ee0b566bc5e095f0a6ca8)


## Assets

List any additional assets, such as scripts or files

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

Describe any challenges encountered while doing the work: 
Takes a lot of memory to host all of the VMs. 

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
