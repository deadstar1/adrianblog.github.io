---
layout: post
title: Flowdock XSS or RCE(malicious file upload)
---

One day I accidentally uploaded a `.pdf` filetype on https://www.flowdock.com/oauth/applications page. it was sucessfuly uploaded. So I tried to upload some arbitary filetype, But flowdock rejected it.
Flowdock backlisted all arbirtary content-type such as `text/html,pplication/x-asp,pplication/x-perl. ... etc..` and flowdock also checked the signature of a file that used to identify if the file is real image or not.

**Error message when I tried to upload a shell!**

![ohh](http://2.bp.blogspot.com/-P21qQh5Oytc/U9NgEyXweRI/AAAAAAAAAPg/EnoMY0H5CXw/s1600/1.png)


If we want to upload our shell or html-xss poc we need upload a real image that contain our xss/rce payload. I changed the exif header of the image and upload the file.

![ohh](http://1.bp.blogspot.com/-gsbzUjnYGmY/U9NgGaYF46I/AAAAAAAAAPo/hB4MN-rQCBc/s1600/2.png)

### RESULT:

![ohh](http://2.bp.blogspot.com/-mnaUU_-6PTU/U9NgG4o4c-I/AAAAAAAAAP0/oDSsBwRqDTM/s1600/3.png)

![ohh](http://1.bp.blogspot.com/-bpdH-nN4tYk/U9NgKLSwt1I/AAAAAAAAAP8/hGoi7rihJN0/s1600/4.png)
## YEHH!
