coinSigner
==========

An open source hardware device support bitcoin signature with secure access.
How the device work?
1. User feed content to it, content could be bitcoin transaction information.
2. User select already imported key.
3. User input pin on phone or pc.
4. Device  check pin, if pin matched, continue to 5, reboot when not matched
5. Device read encrypted private key from flash to ram
6. Device decrypted content to private key with user's pin
7. Device sign the content with private key and output result to user

How to make it secure
1. Private key is encrypted with user's pin and saved in MCU internal flash.
2. The content on internal flash is hardware encrpyted by NXP.
3. All input from phone or pc have fixed length to avoid input overflow.
4. All input has crc.
5. All external intterupt is disable when MCU decrypt private key and signature content.
6. Private key is cleared after signature finished.
7. 4 time wrong pin match will cause device locked.
8. Strongger secure can be supported by check input data signature with ECDSA pub key.



The device has different life circle.
1. Vergin status
   No user data saved inside device.
   You can set a pin for it when device in this status. The device will enter Protected status after you set a pin.

2. Protected status
   You have to input pin before your any action include import your first private key and sign a content
   

ECDSA Algorithm is based on https://github.com/kmackay/micro-ecc
Hardware design follow http://www.lpcware.com/content/project/smartphone-quick-jack-solution
