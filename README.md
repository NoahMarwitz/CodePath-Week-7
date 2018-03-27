# Project 7 - WordPress Pentesting

Time spent: **4** hours spent in total

> Objective: Find, analyze, recreate, and document **three vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. (Required) File Too Large XSS
  - [ ] Summary: 
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.7.5
  - [ ] GIF Walkthrough: <img src="https://i.imgur.com/XFMu1k0.gif" width="800">
  - [ ] Steps to recreate: 
    1) Create a file over 20MB in size
    2) Name it with an <img src=a onerror=alert(1)>.jpg ending.
    3) Get an admin or anyone with media upload access to attempt to upload file.
    4) Script triggers on fail to upload.
  - [ ] Affected source code:
    - [link1](https://core.trac.wordpress.org/browser/branches/4.2/src/wp-admin/load-scripts.php)  
    -CVE: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-9061
2. (Required) Unauthenticated XSS in Comment
  - [ ] Summary: 
    - Vulnerability types: XSS. Buffer Overflow
    - Tested in version: 4.2 
    - Fixed in version: 4.2.1
  - [ ] GIF Walkthrough: <img src="https://i.imgur.com/dtYnB6F.gif" width="800">
  - [ ] Steps to recreate: 
    1) Construct a message over 64kb in size. 
    2) Use `<a title='x onmouseover=alert(unescape(/hello%20world/.source)) style=position:absolute;left:0;top:0;width:5000px;height:5000px  AAAAAAAAAAAA...[64 kb]..AAA'></a>` where the `...[64 kb]..` is replaced with the contents of the message over 64kb in size. 
    3) Post the payload as a comment anywhere on the wordpress site. 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/branches/4.2/src/wp-comments-post.php)
3. (Required) YouTube embed XSS
  - [ ] Summary: 
    - Vulnerability types: XSS via failed sanitization
    - Tested in version: 4.2 
    - Fixed in version: 4.7.3
  - [ ] GIF Walkthrough: <img src="https://i.imgur.com/8VbNnRg.gif">
  - [ ] Steps to recreate: 
    1) Construct the embed src "http://youtube.com/embed/{VIDEO ID}\x3csvg onload=alert(1)\x3e"
    2) Put in a post the src above as an embed.
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/branches/4.2/src/wp-admin/admin-post.php)
    - CVE: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-6817

## Assets

Only file of note is "LotsofAs.txt", which contained 82kb of "AAAA"

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

If running Vagrant without opening VirtualBox in Administrator mode, Vagrant would fail and lose all connections to Ruby, which required reinstalling Vagrant to fix. 

## License

    Copyright 2018 Noah

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
