# LCC Designer setup/installation

The reason for creating a separate designer process from the standard ALM process was to provide the ability for designers to quickly respond to needed UI changes.  At present, when a UI change is needed it would take the UI designer a significantly shorter time than was needed to get the changes into Live.  For example, a change may take the designer a day to implement but due to that change having to go through the normal ALM process, it could at least take around 3 weeks to make it into Live, which is certainly not ideal, especially when dealing with a diverse array of devices and short-lived campaign sites, such as the German Christmas Market.  Furthermore, at present it is difficult to test the design on mobile devices until it has reached Live and then obviously go through the same process again to implement the fixes.

In order to contribute to the designer workflow, you’ll need to set-up and configure the following:

* VS Code
* Git 
* Node.js
* Ruby
* Travis CLI
* Heroku CLI
* LCC GitHub Access

## VS Code
Instead of using a fully-fledged IDE such as Visual Studio, we are using VS Code.  VS Code is a lightweight text editor that can be extended by installing a myriad of extensions that are available on the [Extension Marketplace](https://code.visualstudio.com/Docs/editor/extension-gallery).
To install VS Code visit the following link: [https://code.visualstudio.com/Download](https://code.visualstudio.com/Download)

In order to be able to download the extenstions, you'll need to add the corporate proxy in VS Code:

File -> Preferences -> User Settings

```bash
"http.proxy": "http://<domain>%5C<your username>:<your password>@<corporate-proxy>:<port>" 
```

## Git
We are using Git for our version control system.  Luckily, VS Code integrates quite nicely with Git straight out of the box, showing recent changes and being able to commit straight from the editor instead of having to use the command line.
 
To install Git for Windows: [https://git-scm.com/download/win](https://git-scm.com/download/win)

We use GitHub as our remote repository but in order for us to connect on the corporate network we need to add the following proxy settings in a command prompt:

```bash
git config --global http.proxy http://<corporate-proxy>:<port>/proxy.pac 
```

## Node.js
We use Node.js for some of our build scripts, such as in [lcc_templates](https://github.com/lccgov/lcc_templates) to compile and publish the templates and also use Node.js Express framework to create our prototypes hosted on Heroku.  Furthermore, we use the Node Package Manager (NPM) to publish our own common libraries so that they can be installed in any of our projects and also use it to install 3rd party NPM packages.

To install Node.js and in turn the NPM package manager: [https://nodejs.org/en/](https://nodejs.org/en/)

In order to be able to use NPM on the corporate network we need to add the following proxy settings:

```bash
npm config set proxy http://<corporate-proxy>:<port>
npm config set http_proxy http://<corporate-proxy>:<port>
```

## Ruby
The only reason we need to install Ruby is so that we can use the Travis CLI that is installed as a Ruby gem.

To install Ruby for Windows: [http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/)

## Travis CLI 
The Travis CLI allows us to interact with our [Travis CI builds](https://travis-ci.org/). However, most of the commonly used actions can be performed through the Web UI without having to use the CLI.  The only command that we use often that is unavailable in the Web UI is being able to encrypt passwords and API keys that are stored in the .travis.yml file. ** IMPORTANT: ALWAYS ENCRYPT API KEYS AND PASSWORDS AS THEY ARE STORED PUBLICALLY ON GITHUB. **

To install the Travis CLI, open up 'Command Line with Ruby' (which should have been installed when installing Ruby in previous section) and type the following:

```bash
gem install travis
```

## Heroku CLI
Heroku is a cloud platform that allows us to host our prototypes without having to worry about the infrastructure or DNS settings.  Heroku has a free account that allows you to host up to 5 apps, but obviously all functionality is not available such as scaling, but this is not an issue for our prototype deployments or POCs.  Anyone can register for a free account at: [https://signup.heroku.com/](https://signup.heroku.com/). 

Once you have registered for an account, it is worthwhile downloading the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) that enables you to access your account via the command line. 
In order to use the CLI, you’ll also need to set the proxy in the command prompt:

```bash
set HTTP_PROXY=http://<domain>%5C<your username>:<your password>@<corporate-proxy>:<port>
set HTTPS_PROXY=http://<domain>%5C<your username>:<your password>@<corporate-proxy>:<port>
```

The following Heroku commands are the ones that we use when deploying/debugging apps:

* In order do anything with Heroku via CLI, you’ll need to first log in with your credentials:
```bash
heroku login
```
* To create a new app, we can directly do it from the CLI:
```bash
heroku create <app name>
```
* The following command is handy when you are needing to debug an application:
```bash
heroku logs –-app <app name>
```
* In order to allow Travis CI build to deploy on your behalf, you’ll need to provide an API token and add it to your .travis.yml file. An example can be found in the [lcc_breeze_prototype repo](https://github.com/lccgov/lcc_breeze_prototype/blob/master/.travis.yml):
```bash
heroku auth:token
```
* To add config variables to an application:
```bash
heroku config:set USERNAME=<username> –-app <app name>
```

## LCC GitHub Access
You’ll be able to clone any of our repositories, but if you would like to push your changes back to one of them, you’ll need your GitHub account to be given collaborator rights to that repo.  In order for your account to be given collaborator rights, you’ll first need to create a GitHub account (if you don’t have one), which you can do by going to: [https://github.com/join](https://github.com/join).  Once you have an account, you’ll need to get one of the LCC GitHub administrators to give you collaborator rights to the repository.  The current administrators are:

* Catherine Elliott
* Ian Stafford
* Chris Wilson

That's it! You should be all set to contribute to the LCC Designer Workflow!