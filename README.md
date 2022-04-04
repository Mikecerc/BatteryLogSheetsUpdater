# Digital Battery Sign-out Sheet

Log battery sign-outs with the battery number, time signed out/in, and battery stats (rint and state of charge) before and after use, all with kiosk mode chromium running on xserver.

## Hardware

1. [Raspberry Pi 2/3 with internet access](https://www.raspberrypi.com/products/raspberry-pi-3-model-b/)
2. [Sunfounder 7" touchscreen display](https://www.sunfounder.com/collections/touchscreens/products/7inch-ips-touchscreen)

### Node Dependencies

* mongoose
* node-cron
* google-apis
* dotenv

### Setup

**Note**: These instructions are specifically for Ubuntu server 20.04.4LTS (64bit ARM64). For help on installing this operating system, please click [here](https://www.maketecheasier.com/install-ubuntu-on-raspberry-pi/).
> Warning: You MUST install the 64 bit version (ARM64 architecture) of Ubuntu server.


#### First clone the repository via HTTP

```bash
git clone https://github.com/Mikecerc/DigitalBatteryLog.git
```

#### To install all dependencies and create all configuration files, run the following to run the install script and follow any prompts given

```bash
sudo bash ./install.sh
```

### Next, you must create an app via Google Cloud Platform in order to use the Google Sheets API. Follow the steps below to successfully setup the application, Oauth2 and Google Sheets API

1. Using internet explorer, navigate to the [Google Cloud Platform](https://console.cloud.google.com)
2. agree to the terms of service and continue onto the master dashboard.
3. click on `IAM & Admin`\
![img](https://github.com/Mikecerc/DigitalBatteryLog/blob/master/.github/images/IAM-sc.png?raw=true)

4. Click "create a project"<br>
![img](https://github.com/Mikecerc/DigitalBatteryLog/blob/master/.github/images/createProj.png?raw=true)
5. Create a new Project by giving the project a name. Proceed by clicking create.<br>
![img](https://github.com/Mikecerc/DigitalBatteryLog/blob/master/.github/images/newProj.png?raw=true)
6. Return Back to the master dashboard of [Google Cloud Platform](https://console.cloud.google.com)
7. While on the dashboard, navigate to the `APIs & Services` tab and select `Library`.<br>
![img](https://github.com/Mikecerc/DigitalBatteryLog/blob/master/.github/images/ApiandSer.png?raw=true)
8. In the search bar, search "Google Sheets API"<br>
![img](https://github.com/Mikecerc/DigitalBatteryLog/blob/master~/.github/images/Api%20lib.png?raw=true)
9. Click on the result. It should be the only result.<br>
![img](https://github.com/Mikecerc/DigitalBatteryLog/blob/master/.github/images/SheetsApi.png?raw=true)
10. Click enable to enable the Google Sheets API.<br>
![img](https://github.com/Mikecerc/DigitalBatteryLog/blob/master/.github/images/EnableApi.png?raw=true)
11. Next we will have to create credentials. On the top of the page you are now at, you should see a button labeled `CREATE CREDENTIALS`. Click it.<br>
![img](https://github.com/Mikecerc/DigitalBatteryLog/blob/master/.github/images/SheetsApiManage.png?raw=true)
![img](https://github.com/Mikecerc/DigitalBatteryLog/blob/master/.github/images/createCredentials.png?raw=true)
12. You should now see a prompt labeled `Which API are you using?` Select User Data and then click next. <br>
![img](https://github.com/Mikecerc/DigitalBatteryLog/blob/master/.github/images/SelectApi.png?raw=true)
13. In the next section, name the app something you would recognize (Digital Battery Log) and enter the email address you are using in boxes labeled `User support email` and `Email addresses`. You do not need to submit an App logo. Click `save and continue` when done.
14. You should now be prompted with a section labeled `Scopes`. Click `Add and Remove scopes`. Navigate to the last page of the scopes menu and find the scope: `.../auth/spreadsheets`. Hit the check box next to it and scroll to the bottom of the page. click the `update` button. <br>
![img](https://github.com/Mikecerc/DigitalBatteryLog/blob/master/.github/images/scopes.png?raw=true)
![img](https://github.com/Mikecerc/DigitalBatteryLog/blob/master/.github/images/select%20scopes.png?raw=true)
15. At the bottom of the scopes page, click `SAVE AND CONTINUE`.
16. You should now see a tab labeled `OAuth Client ID`. Under the `Application type` dropdown, select `Desktop app`. Give the client a name you will remember. Click `Create`. <br>
![img](https://github.com/Mikecerc/DigitalBatteryLog/blob/master/.github/images/OAuth.png?raw=true)
17. The final tab should be labeled `Credentials`. Click the download button. Move the JSON file you downloaded into `[REPOSITORY-FOLDER]/config/auth` and rename the file to `credentials.json`.
18. Return to the `API & Services Tab` and navigate to the `OAuth consent screen` tab. <br>
![img](https://github.com/Mikecerc/DigitalBatteryLog/blob/master/.github/images/oauthconsent.png?raw=true)
19. Scroll down until you see the section labeled `Test Users`. Click the `Add Users` Button <br>
![img](https://github.com/Mikecerc/DigitalBatteryLog/blob/master/.github/images/testuser.png?raw=true)
20. add the email you will be using to edit your sheets <br>
![](https://github.com/Mikecerc/DigitalBatteryLog/blob/master/.github/images/addUser.png?raw=true)

> WARNING: The email address you enter MUST have edit permissions on the Google Sheets you are editing.

21. You may now close your internet explorer browser.

22. In order to use the Google Sheets API, you need an access token. To generate an access token, run the following command in the main folder of the repository:

```bash
node run getToken
```
