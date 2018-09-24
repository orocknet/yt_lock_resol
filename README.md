## mikrotik
/ip firewall raw
add action=drop chain=prerouting comment=drop-udp-Youtube-for-lock-resolution content=www.youtube.com dst-port=\
    443 in-interface=ether2-LocalNet protocol=udp src-address=192.168.1.0/24
add action=drop chain=prerouting content=s.ytimg.com dst-port=443 in-interface=ether2-LocalNet protocol=udp \
    src-address=192.168.1.0/24

## squid
acl en_annotations_modulejs url_regex -i (s.ytimg|www.youtube)\.com\/yts\/jsbin\/player.*\/en_US\/annotations_module.js
acl en_basejs url_regex -i (s.ytimg|www.youtube)\.com\/yts\/jsbin\/player.*\/en_US\/base.js
acl en_captionsjs url_regex -i (s.ytimg|www.youtube)\.com\/yts\/jsbin\/player.*\/en_US\/captions.js
acl en_endscreenjs url_regex -i (s.ytimg|www.youtube)\.com\/yts\/jsbin\/player.*\/en_US\/endscreen.js
acl en_remotejs url_regex -i (s.ytimg|www.youtube)\.com\/yts\/jsbin\/player.*\/en_US\/remote.js
acl id_annotations_modulejs url_regex -i (s.ytimg|www.youtube)\.com\/yts\/jsbin\/player.*\/id_ID\/annotations_module.js
acl id_basejs url_regex -i (s.ytimg|www.youtube)\.com\/yts\/jsbin\/player.*\/id_ID\/base.js
acl id_captionsjs url_regex -i (s.ytimg|www.youtube)\.com\/yts\/jsbin\/player.*\/id_ID\/captions.js
acl id_endscreenjs url_regex -i (s.ytimg|www.youtube)\.com\/yts\/jsbin\/player.*\/id_ID\/endscreen.js
acl id_remotejs url_regex -i (s.ytimg|www.youtube)\.com\/yts\/jsbin\/player.*\/id_ID\/remote.js

deny_info 301:https://orocknet.github.io/yt_locker/en_annotations_module.js en_annotations_modulejs
deny_info 301:https://orocknet.github.io/yt_locker/en_base360.js en_basejs
deny_info 301:https://orocknet.github.io/yt_locker/en_captions.js en_captionsjs
deny_info 301:https://orocknet.github.io/yt_locker/en_endscreen.js en_endscreenjs
deny_info 301:https://orocknet.github.io/yt_locker/en_remote.js en_remotejs
deny_info 301:https://orocknet.github.io/yt_locker/id_annotations_module.js id_annotations_modulejs
deny_info 301:https://orocknet.github.io/yt_locker/id_base360.js id_basejs
deny_info 301:https://orocknet.github.io/yt_locker/id_captions.js id_captionsjs
deny_info 301:https://orocknet.github.io/yt_locker/id_endscreen.js id_endscreenjs
deny_info 301:https://orocknet.github.io/yt_locker/id_remote.js id_remotejs

http_access deny en_annotations_modulejs
http_access deny en_basejs
http_access deny en_captionsjs
http_access deny en_endscreenjs
http_access deny en_remotejs
http_access deny id_annotations_modulejs
http_access deny id_basejs
http_access deny id_captionsjs
http_access deny id_endscreenjs
http_access deny id_remotejs
