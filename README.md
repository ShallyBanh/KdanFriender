# KdanFriender

A sample web server, written in Ruby, showing how to create/modify/integrate wallet cards into apple wallet and how to set up push notifications when data on the wallet card changes.

## Usage 

Well tbh i don't really expect anyone to use this code since it was made as a meme demo that i'm doing for work. But hopefully someone can take a look at the code and reuse some of the stuff i did or see how i did certain things and maybe find it helpful in integrating their own wallet card.

So in order to run this code a couple of ruby gems are required so run these commands in the "backend" directory

```
> sudo gem install sinatra rack sequel sqlite3 json rubyzip zip-zip
> sudo gem install lib/sign_pass-1.0.0.gem
```

Next you need to add your own certificates in the Certificate Folder more specifically two certs. One for the pass type id (which you can create in the apple developer portal) export that as a .p12 file and a Apple Worldwide Developer Relations Certification Authority certificate (.pem file). You need this in order to compress your wallet card file which needs to be signed. 

Next you can configure your own settings in the backend/config.ru file. You should set your own pass type id, team id, and hostname of your server. You can also modify the pass.json file under backend/data/passes/template to style the wallet card the way you want it to look.

Next run these line in the backend folder in order to set up your database

```
> ruby lib/pass_server_ctl.rb --setup
```

Now we can finally start the server using:

```
> rackup -p <portnumber>
```
You can now go to your localhost:portnumber and create a new wallet card and integrate it into apple wallet. If you edit the card on the frontend a notification should be sent to your phone regarding the change to the wallet card. 

Also you want to have a secure connection to talk to your server so https so i would suggest to use ngrok which will create a secure tunnel to your localhost. More info here: https://ngrok.com/ but you can just run

```
npm install ngrok -g
ngrok http <whatever port number you want a secure tunnel to>
```

![ScreenShot](https://github.com/ShallyBanh/KdanFriender/blob/master/images/1.png)
![ScreenShot](https://github.com/ShallyBanh/KdanFriender/blob/master/images/2.png)

**Note**: This code is just used for a demo of the capabilities of apple wallet and is not intended be used for production
 
## Apple Sample Code

The server implementation is based on Apple's own reference server implementation for Apple wallet and therefore contains extensive amounts of Apple sample code that Apple provides under the following license:

> Apple grants you a personal, non - exclusive license, under Apple's copyrights in this original Apple software ( the "Apple Software" ), to use, reproduce, modify and redistribute the Apple Software, with or without modifications, in source and / or binary forms; provided that if you redistribute the Apple Software in its entirety and without modifications, you must retain this notice and the following text and disclaimers in all such redistributions of the Apple Software.

^ don't sue me

## Credits

This code was created by following the guides of:
* https://oleb.net/blog/2013/02/passbook-tutorial/
* https://developer.apple.com/library/archive/documentation/PassKit/Reference/PassKit_WebService/WebService.html
* https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/PassKit_PG/Updating.html#//apple_ref/doc/uid/TP40012195-CH5-SW1
