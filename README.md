----
----
#  AqaraPOST-Homeassistant addon #

Add-on HomeAssistant with automatic config scripts!!
 
 * only Username/Password Aqara required
 
 * [AqaraPost_[Node-RED]](https://github.com/sdavides/AqaraPOST-Homeassistant/tree/main/addon-AqaraPost/README.md)

05/01/2025 🚨 Drop support for ARMv7 ([#2016](https://github.com/hassio-addons/addon-node-red/pull/2016))

----

----

#  AqaraPOST-Homeassistant #

Goal: Replace Post request "Aqara Home" app on HomeAssistant

  * note: 
	* this flow is example and was developed for Aqara Hub G3 camera *( lumi1.xxxx )*
  		* for Aquara FP2 see [Darafei Praliaskouski page](https://www.patreon.com/posts/connecting-fp2-107200167)

## Requirement ##
* Your value from POST Request Aqara app:
  * appid  ( XXXXXXAPPIDXXXXXXXXXXX )
  * token ( XXXXXXTOKENXXXXXXXXXXX )
  * subjectId ( lumi1.XXXXXXXXXXXX ) *usually MAC-ADDRESS*
  * aqara url ( rpc-ger.aqara.com ) *host*
    * [list aqara url](https://github.com/sdavides/AqaraPOST-Homeassistant/blob/main/generatejson/list_aqara_url.txt)
  * timezone ( it-IT ) *-> es-ES/en-UK/de-DE/it-IT/pt-PT/en-US...*
  * userid *( automatic, enter manual if not work )*
	
## Method ##
* Method 1 NodeRed (recommended, required NodeCompanion):
	* Install Add-on
              [AqaraPost_[Node-RED]](https://github.com/sdavides/AqaraPOST-Homeassistant/tree/main/addon-AqaraPost/README.md)

* Method 2 NodeRed (recommended, required NodeCompanion):
	* Import flow Aqara_G3_nodered.json 
	* Replace your value "config" node 
	* Deploy
		* note: you can use the script to generate your NoderRed json
		* [generatejson](https://github.com/sdavides/AqaraPOST-Homeassistant/blob/main/generatejson/README.md)
    
 * Method 3 RestFul (without NodeRed - few functions):
	* Replace your value Aqara_G3_without_nodered.txt
	* Copy and paste Aqara_G3_without_nodered.txt on configuration.yaml
	* Restart HomeAssistant
   
## Find your Value ##
* Method 1 Python script:

	from [Wh1terat](https://gist.github.com/Wh1terat/c4a4c665d692af461796e5eee9f5461d)'s python script
	you can find your values ​​from your username and password Aqara account
	 * [GenerateToken](https://github.com/sdavides/AqaraPOST-Homeassistant/tree/main/generatejson#generate-token-from-username-and-password)

* Method 2 Use BurpSuite or ZAP or similar:
	* Follow [BurpSuite Guide](https://github.com/sdavides/AqaraPOST-Homeassistant/blob/main/Burp%20Suite%20Guide.pdf)
 	* Follow [ZAP Guide](https://github.com/sdavides/AqaraPOST-Homeassistant/blob/main/ZAP%20Guide.pdf)
         * [free dowload](https://www.zaproxy.org/download)
	* Download AqaraHome apk mod:
 		* [AqaraHome 3.0.6](https://github.com/sdavides/AqaraPOST-Homeassistant/blob/main/apk/Aqara%203.0.6_mod_network.apk) (old Android)
 		* [AqaraHome 4.0.2](https://github.com/sdavides/AqaraPOST-Homeassistant/blob/main/apk/Aqara%204.0.2_mod_network.apk)
 
## Why? ##
I have an Aqara Hub G3 camera on HomeAssistant but I can't control it, with the homekit connection I only have the alarm function.

## Info ##
This is the beauty of it: no modifications to the device are necessary.

You can delete AqaraHome_mod app it without logging out, otherwise the token values ​​​​are expired.

AqaraHome apk mod includes acceptance of the user-installed certificate, (to see the http requests in burp).


## Install ##
![immagine](https://github.com/sdavides/AqaraPOST-Homeassistant/assets/31100253/a7c093f9-c383-451d-b452-828d5d4b03af)

![319800579-a36eb9e9-8a0c-480c-82db-3def3f8d51a9](https://github.com/sdavides/AqaraPOST-Homeassistant/assets/31100253/2ea10616-0af3-4a10-84f7-d5cebd9b0435)


## Update data ##
* add automation every 1 minute:

	  
		description: Update Aqara G3
		mode: single
		trigger:
 		 - platform: time_pattern
 		   minutes: /1
		condition: []
		action:
		  - service: button.press
		    metadata: {}
		    data: {}
		    target:
		      entity_id: button.camera_g3_log
	  
	or change inject node:

	![immagine](https://github.com/sdavides/AqaraPOST-Homeassistant/assets/31100253/ebf6ebad-bdb0-427e-add6-d8a3dcb8caa6)

## Update flow ##

for a successful update of the existing flow without changing the entities in HomeAssistant, follow the steps:
  * import new json
    
    ![immagine](https://github.com/sdavides/AqaraPOST-Homeassistant/assets/31100253/75ce29e0-e829-417c-bd2c-0db5ced8199a)

  * delete old flow (complete flow card)

    ![immagine](https://github.com/sdavides/AqaraPOST-Homeassistant/assets/31100253/b7db7bc7-5a7a-4fc9-bd1b-1899e8977b5a)

  * deploy  
!! do not deploy without deleting the old !!


---

## TIPS Hub G3 ##

* Turns the camera into an NGINX-cgi PHP server and much more...:
    * [AqaraG3-armv7-binary](https://github.com/sdavides/AqaraG3-armv7-binary)
      
      ![immagine](https://github.com/sdavides/AqaraPOST-Homeassistant/assets/31100253/555c0f99-d010-4323-b365-070d26e4ad7f)

 
---

* HomeKit alarm function HomeAssistant:
    * autodiscovery, insert qrcode number
    
  		port change every reboot of device, replace into 
  
  		"/config/.storage/core.config_entries"

  		![4](https://github.com/sdavides/AqaraPOST-Homeassistant/assets/31100253/f26c6a0c-6b96-4c41-b0ce-50332f542e87)

---

* Live video:
   * hack G3 (delete authentication rtsp):
     * Manual downgrade firmware [3.3.4](https://github.com/niceboygithub/AqaraCameraHubfw/blob/main/stock/G3) (post_init.sh enable)
     * Open telnet QR method [aQRootG3](https://github.com/Wh1terat/aQRootG3) (create post_init.sh)
     * Manual update firmware [3.3.9](https://github.com/niceboygithub/AqaraCameraHubfw/blob/main/stock/G3) (post_init.sh enable)
     * Update last firmware from command [custom firmware](https://github.com/niceboygithub/AqaraCameraHubfw/tree/main/modified/G3#flash-g3-custom-firmware-method)
         * hack done! (post_init.sh enable)
     * Add *vi /data/scripts/post_init.sh* *( from telnet )*
        ```
		killall -9 rtsp && rtsp >/dev/null 2>&1 &
		```
          or you can see rtsp user/pass (change every boot)

          from telnet command:
	  	```bash
	  	agetprop sys.camera_rtsp_url  # agetprop full (list all prop.)
	  	```
	  	![immagine](https://github.com/sdavides/AqaraPOST-Homeassistant/assets/31100253/f4a401f3-f9f0-4fd3-a9f8-ea8605c8bba9)


	 	 rtsp://192.168.1.4:8554/360p (/720p /1080p /1296p)

	 	 rtsp://USER:PASS@192.168.1.4:8554/360p (/720p /1080p /1296p)

    ```bash
    command_line:
      - sensor:
          name: aqara_rtsp_telnet
          command: "apk -q add inetutils-telnet && ( sleep 3; printf 'root\n'; sleep 1; printf 'clear\n'; sleep 1; printf 'agetprop sys.camera_rtsp_url\n'; sleep 1; ) | telnet 192.168.1.4 | sed '1,8d' | sed '$d'"
          value_template: "{{ value_json['720p'] }}"
          json_attributes:
            - 360p
            - 720p
            - 1080p
            - 1296p
     ```


---

* Sensor telnet command:
   * example "date"
 
```bash
command_line:
  - sensor:
      name: aqara_test
      command: "apk -q add inetutils-telnet && ( sleep 3; printf 'root\n'; sleep 1; printf 'clear\n'; sleep 1; printf 'date\n'; sleep 1; ) | telnet 192.168.1.4 | sed '1,8d' | sed '$d'"
      value_template: "{{ value }}"
```

 ![immagine](https://github.com/user-attachments/assets/1712abb3-1867-47ff-b352-063665389d68)



---

## Support me ##

**ko-fi.com** https://ko-fi.com/davide70304

---

## See also ##

[AqaraG3-armv7-binary](https://github.com/sdavides/AqaraG3-armv7-binary) AqaraG3 extra command

[AqaraCameraHubfw](https://github.com/niceboygithub/AqaraCameraHubfw) HACK 

[m3u8-HLS-Homeassistant](https://github.com/sdavides/m3u8-HLS-Homeassistant) Player m3u,mpd,mp4 playlist

[NginxReverse-Homeassistant](https://github.com/sdavides/NginxReverse-Homeassistant) ReverseProxy on HA

[go2rtc](https://github.com/AlexxIT/go2rtc) RTSP Proxy (HomeKit supported)
     
[WebRTC](https://github.com/AlexxIT/WebRTC) Card RTSP 

[EPGItaly-Homeassistant](https://github.com/sdavides/EPGItaly-Homeassistant)
