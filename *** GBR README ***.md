## Complete Botpress installation using Yarn and NodeJS
### I. First delete files/folders metioned in the below path:
1) C:\Program Files\Nodejs
2) C:\Users\bhargava\AppData\Roaming\npm do the same for admin folder also(if you opened cmd as admin while installing yarn)
3) C:\Users\bhargava\AppData\Roaming\npm-cache 
4) C:\Users\.npmrc or delete any yarn or npm or node related files and folders
5) C:\Users\bhargava\AppData\local\temp\ delete any yarn or npm or node related files and folders
6) Delete recycle bin files and delete %temp% files from RUN cmd
7) Restart your PC
8) Check wheather all the mentioned files are deleted or not from the path

### II. Install node 12.18.1 MSI file [Click to download](https://nodejs.org/download/release/v12.18.1/) <br/>
**Note :** To install specific version or to "Downgrade" existing node version > Open windows cmd > write "npm i -g node@version" > check node version with "node -v"

### III. Open windows cmd prompt(opening as administrator is not mandatory & below cmds won't work in powershell) and enter below cmds
 - npm -v
 - node -v
 - npm i --global yarn@1.22.18
 - Close the terminal and re-open it to check yarn version
 - yarn --version <br>
**Note :** Prefer installing yarn using npm rather than installing via yarn.exe file

### IV. Now we need to clone botpress from official botpress git repository
 - To clone git, we need "git" installed in your PC [Click to download](https://git-scm.com/downloads)
 - Command to confirm git installed or not "git --version"
 - Goto folder where you want to clone botpress folder
 - Paste the cmd "git clone https://github.com/botpress/botpress.git" and press enter, It'll clone botpress folder from official botpress github site
 - cd botpress
 - yarn cache clean
 - yarn
 - yarn build 
 - In this step you may suggested to run "caniuse-lite", don't press any key until it finished all installations by showing a msg "finished in 14 min"(it took 14mins to install all the resources)
 - Once installed it'll show you the path of current folder where you can type the below step cmd
 - You can type the cmd "npx browserslist@latest --update-db" after completion of previous step (don't forcely close).
 - yarn start <br/>
 
 <b>You can run above methods in single line :</b> yarn cache clean && yarn && yarn build && yarn start

**Note :** It'll take 20-30 mins for this entire process of yarn installation depending on internet speed and Don't close forcely assuming that terminal is struck <br/>
Versions at the time of project upload:
1) git : git version 2.36.1.windows.1
2) npm : 6.14.5
3) node : v12.18.1
4) yarn : 1.22.18

### V. Zip & Deploying Botpress
1) Zip the folder using 7zip After Ignoring "nodemodules" folder from botpress folder
2) Share the zipped file with cloud
3) Unzip the file using 7zip 
4) Open the unzipped folder in vscode
5) Use command "yarn install" to install nodemodules
6) Start the botpress server using "yarn start"

### VI. Installing MySQL in Botpress
1) "yarn add mysql" (may show some warnings)
2) Run if step-1 fails "yarn add mysql -W"
3) yarn start
4) For some mysql versions it may display authentication error in console while fetching/accessing data from database
5) To resolve this issue..goto mysql workbench/commandLine > type "ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_new_password';" and press ctrl+enter to run the command.
6) Refer [this page](https://www.codegrepper.com/code-examples/sql/ER_NOT_SUPPORTED_AUTH_MODE%3A+Client+does+not+support+authentication+protocol+requested+by+server%3B+consider+upgrading+MySQL+client) for more information

### VII. Creating custom nodejs project(to use botpress in this website)
1) In console it'll display botpress server is exposed at "http://localhost:3000"
2) On clicking the host link, you will be redirected to botpress studio registration page.
3) Upon successful registration, click on "create bot" > New bot > give a name to the bot(you can give custom botId).
4) On successful bot creation, click on the "bot name" where it'll display a emulator.
5) Train your bot by clicking on "train bot" button present at the bottom right corner of botpress studio window.
6) You can check the progress of bot training in the terminal from where you started the botpress.
7) With this we've successfully started our server, We've to integrate this server in our website using <script> tag.
8) Integrating chatbot in our custom website <br/>
       a) Create a package structure using the following npm cmds
   - Open npm command prompt
   - npm install express<space>-g
   - npm install express-generator -g
   - cd desktop
   - express --view=pug projectName
   - to install html as frontend engine > express --view=ejs projectName
   - cd projectName
   - npm install
   - npm start <br/>
  
   b) Copy and paste following code into your index.pug file after body tag<br/>
      - <script src="http://localhost:3000/assets/modules/channel-web/object_assign.js"></script>
      - <script src="http://localhost:3000/assets/modules/channel-web/inject.js"></script>
      - <script>
      -   window.botpressWebChat.init({
      -    host: 'http://localhost:3000/',
      -    botId:"brh-bot",
      -    extraStylesheet: '/assets/modules/channel-web/spinebot-style-sheet.css',
      -   })
      - </script>
  
   c) Change your default port number of your website from bin/www folder of nodejs application in-order to avoid overlapping default port of botpress server(3000)<br/>
  
   d) Start your website using cmd "npm start" from the terminal.
 
### VIII. Ngrok Installation
 - Goto ngrok.com and signup
 - In dashboard.ngrok.com/get-started/setup click on download for windows
 - Unzip the file & open ngrok.exe
 - Now to authenticate our account, goto step-1 link
 - In section 2 connect your a/c by copying the cmd from 'ngrok authtoken...' & paste in command prompt that was running in background & click Enter
 - Start your localhost:3000 using npm via vscode
 - To make localhost available on server by typing the cmd 'ngrok auth 3000' click Enter
 - Now copy the forwarding link & paste it in botpress 'bot.config.json' file under 'configuratinos' section using 'keyId' & 'secret'
 - Goto sandbox website & check whatsapp integration in botpress using smooch/sandbox

### VIII. Modifying botpress src folder
   #### 1) Adding CSS to chatbot
    Goto botpress folder/modules/channel-web/assets/default.css
	
    Note - 1 : Folders in modules/channel-web are permanent memory & folders in bp/package are temporary i.e; erased on server restart
	Note - 2 : default-emulator.css(botpress/modules/channel-web/assets/default-emulator.css) is for modifying "emulator" in admin panel
   #### 2) Modifying UI (CSS) of Botpress Studio
	- To change width of bot widget > hide width & height in inject.css of class name ".bp-widget-widget" and specify height for class ".bpw-widget-btn" in default.css
    - You can provide custom CSS for Botpress-Studio by going to the path: botpress/packages/bp/dist/admin/ui/public/static/js/main.b025657d.chunk.js/search the class name & change the existing css code there itself > Restart botpress server to apply changes
    - Colors used => Orange: #F36C30 || Blue: #1A125A
    - For admin colors Goto botpress/data/assets/modules/hit/next/webchat-theme.css & botpress/modules/channel-web/assets/default-emulator.css > :root
    - Colors.scss file is in botpress/packages/ui-shared/src/theme/common/-colors.scss\
    - To change login page logo in admin panel Goto botpress/packages/bp/dist/admin/ui/public/static/js/main.b02564d.chunk.js.mp and check class name ".style_logo__21TBr{your code}"
    - To hide "powered by botpress" footer in admin login Goto css and add "display:none" to class ".bpw-powered"
    - To add "We're powered by Spinebiz" footer inside chatbot Goto C:\Users\bhargavarg\Desktop\Spinebot_Chatbot\botpress
	  v12.28.0\modules\channel-web\assets\web\lite.bundle.js search for link
      react_1.default.createElement(
       'a',
       { href: 'https://botpress.com', target: '_blank' },
       'botpress'
      )		
	  
    change href from 'https://botpress.com' to 'https://spinebiz.com', change text from botpress to Spinebiz(you can hide this from css file)
	  and search for "footer.poweredBy": in the same folder and change the name accordingly
					
    - Alerting in chatbot
      goto global botpress.config.json from admin panel
      set "enabled": true at line no : 129
    - To change login/signup button of admin panel > Goto botpress/packages/bp/dist/admin/ui/public/static/js/main.b022.chunk.js/.bp3-button.bp3-intent-primary{your code}
    - Path for images in botpress folder > a) botpress/modules/channel-web/assets/images/ <br/> b) botpress/packages/bp/dist/data/assets/modules/channel-web/images
   #### 3) Changing mailId from src folder(only mail not pwd)
    - You can change mail Id from the path botpress/packages/bp/dist/data/global/botpress.config.json > "superAdmins": <br/>
   #### 4) To change default botpress server port number
    - Goto botpress/packages/bp/dist/data/global/botpress.config.json > "port":3000 <br/>
   #### 5) To change the name of the bot in the chat emulator
    - Open botpress studio(admin panel) > Click config button of your bot > Change the name from the name section
    - Changing name will instantly reflect in your website bot
    - Sometimes restarting the npm and bot server is needed
   #### 6) To change or modify code (eg:API)
    - Open botpress studio(admin panel) > Click on code editor from sidebar menu > In the Actions section, open the file in Bot <bot name> folder
    - Change the code or API that you want and finally click on Save icon present at bottom-left
   #### 7) To change MySQL user, pwd from src code
    - Goto botpress/packages/bp/dist/data/bots/brh-hot/actions/botDB.js(file name where db connection code present)
   #### 8) To add current bot info as an "i" icon in chatbot
    - Goto botpress v12.28.0\packages\bp\dist\data\global\config\channel-web.json
    - make  "showBotInfoPage": true instead of false
   #### 9) To make bot to start conversation first when user opens the chat bot - Add the following script in your index.html
    - window.addEventListener("message", function (event) {
    -  if (event.data.name === "webchatReady") {
    -   window.botpressWebChat.sendEvent({
    -    type: "proactive-trigger",
    -    channel: "web",
    -    payload: { text: "fake message" },
    -   })
    -  }
    - })
   #### 10) Path to Reset, Close, Etc SVG icons in chatbox 
    - botpress/modules/channel-web/src/views/lite/icons/close.tsx etc..
   #### O) Others
    - You can increase "AUTO LOGOUT" time of admin panel for current bot by going to admin panel > code editor > configurations > bot.config.json > and paste the code in "dialog":{"timeoutInterval": "3000 week", "sessionTimeoutInterval": "3000 week"} (or) goto botpress.config.json and paste the above code to apply changes globally
  
**Note :** If you make any modifications using yarn start cmd, please restart your server for each modification you've made.
  
### IX. Reference Links
  #### 1) Installation guide
    - Yarn package installation site : https://classic.yarnpkg.com/lang/en/docs/install/#windows-stable, https://yarnpkg.com/
    - Alibaba Botpress Tutorial : https://www.alibabacloud.com/blog/advanced-concepts-in-botpress-a-crash-course_596225
    - Npm package : https://socket.dev/npm/package/@botpress/channel-web
    - Botpress examples : https://github.com/botpress/botpress-examples/blob/master/motivation-bot/index.js
    - Botpress email sending : https://www.youtube.com/watch?v=IVLLHU4MANM
    - Connecting with mysql : https://www.youtube.com/watch?v=a5aqiMQc9Uk , https://aabingunz.com/how-to-connect-to-mysql-database-using-botpress/ <br/>
  #### 2) API Integration links
    - https://www.adenin.com/blog/botpress-work-chatbot-tutorial/ <br/>
    - https://www.youtube.com/watch?v=rju2Fg9fg4I <br/>
    - https://www.youtube.com/watch?v=pw6CUtJ_8w0 <br/>
  #### 3) Displaying image via API
    - https://www.youtube.com/watch?v=zaVwJ8j8cZI
  #### 4) Free API's 
    a) OMDB(Movie Details) : https://www.omdbapi.com/ <br/>
    b) Online Shopping : https://fakestoreapi.com/ <br/>
    c) Countries Data : https://apis.ccbp.in/countries-data <br/>
    d) Makeup Items Shopping : http://makeup-api.herokuapp.com/api/v1/products.json?brand=maybelline <br/>
    e) Breweries (Beers) : https://api.openbrewerydb.org/breweries <br/>
    f) License on Food Court : https://api.fda.gov/food/enforcement.json?limit=10 <br/>
    g) Gaming : https://api.opensea.io/api/v1/assets?format=json <br/>
    h) Public API Entries : https://api.publicapis.org/entries <br/>
    i) Beers Review : https://api.punkapi.com/v2/beers <br/>
    j) Techcrunch : https://techcrunch.com/wp-json/wp/v2/posts?per_page=100&context=embed
  #### 5) Whatsapp Integration using smooch
    - https://app.smooch.io/
   
### X. Handling Errors & Some Imp points in Botpress
  - If any new/existing module got corrupted, remove it from npm by using the command "npm uninstall <module name>", Don't restart botpress by typing "yarn start", Type "npm i" to install fresh modules/packages, Yarn will automatically build required packages, Once installed check by typing "yarn start" <br/>
  - Showing text in studio as developer mode eg: studio.admin.login for login text, To resolve this issure jst press "ctrl+q" from your chrome window, Try resetting the chrome setting if the issue not solved
  - The engine "node" is incompatible with this module. Expected version "^12.20.0 || >=14". Got "12.18.1". Type this command in terminal "yarn install --ignore-engines"
  
  
### XI. To hide left side menu in studio press ctrl+b, do the same to unhide it
