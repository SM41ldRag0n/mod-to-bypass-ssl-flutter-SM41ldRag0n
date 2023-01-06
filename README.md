# mod-to-bypass-ssl-flutter-SM41ldRag0n
Flutter SSL pinning bypass using mod installed app and iphone

This is a tip to Bypass SSL Pinning for:
- A Iphone Jailbreak
- A Flutter App Mobile
- A Api Server accept all request to it (if not, you have to export cert from app)
- Localtunnel
- Burpsuite

Idea: SSL Pinning will protect connect from Client to Api victim Server (domain/api/....), 
and SSL Pinning don't know Whose domain. 

SSL Pinning only protect domain which hardcode or get from somewhere, trust 100% what domain client using
 
So that, let change domain client using by mod app
With Flutter, we can mod app without re-sign, we will mod main file, after installed, after unzip

Ex: App call https://yourfakedomain.tunnel.com/api => Tunnel service Forward  to Burpsuite on your computer => Forward to Real domain 
=> Get response => Send response to client auto
SSL pinning will protect yourfakedomain and NSAppTransportSecurity will not check hash of yourfakedomain

And this is how to:

1. Find where is App installed
To Jailbreak, you can use Unc0vert or Checkra1n 
https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/FileSystemOverview/FileSystemOverview.html
Ex: /private/var/containers/Bundle/Application/random ID/Runner.app/Frameworks/App.framework/App
You can easy find app by SSH to Iphone with 3u Tool and Usb cable, and sort by created day or modified day
Or realtime log or objection to get path in memory app

2. Find where is domain setting:
If very lucky, app will use domain from config.xml. Just change to your domain and forward
else you can use strings.exe from Sysinternals on App file. You should see https://real_domain.com/api/... or only real_domain
Just change all real_domain.com to fake_domain

3. Edit Binary App with HxD
To edit a binary file, require is len(real_domain.com) === len(fake_domain.com)
You can use ngrok with paid to have custom subdomain, or npm Localtunnel to get a custom subdomain free
lt --port 443 --subdomain fake_domain123 => https://fake_domain123.loca.lt (123 is padding)
Replace all and Save file and ssh to Replace file
If victom app can open normaly and only disconnect, that is OK

4. Setting Burpsuite
Install Burp cert on phone
Open proxy 443, setting Invisible, redicect to real_domain and force to 443
Setting Match and Replace to Match fake_domain and replace to real_domain

5. Go to fake_domain on phone, to confim use fake_domain

6. Open App and have fun

7. If app check jailbreak, unjailbreak easy and have fun



If not, read orther post :( Like reflutter or iptables frida

From SM41ldRag0n
