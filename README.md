
<br/>
<p align="center">
  <h3 align="center">Send mail notification to GitHub last committer email using Jenkins.</h3>

  <p align="center">
    <a href="https://github.com/ShaanCoding/ReadME-Generator/issues">Report Bug</a>
    .
    <a href="https://github.com/ShaanCoding/ReadME-Generator/issues">Request Feature</a>
  </p>
</p>

![Contributors](https://img.shields.io/github/contributors/ShaanCoding/ReadME-Generator?color=dark-green) ![Stargazers](https://img.shields.io/github/stars/ShaanCoding/ReadME-Generator?style=social) ![Issues](https://img.shields.io/github/issues/ShaanCoding/ReadME-Generator) 

## Table Of Contents

* [About the Project](#about-the-project)
* [Built With](#built-with)
* [Getting Started](#getting-started)
  * [Prerequisites](#prerequisites)
  * [Installation](#installation)
* [Usage](#usage)
* [Roadmap](#roadmap)
* [Contributing](#contributing)
* [License](#license)
* [Authors](#authors)
* [Acknowledgements](#acknowledgements)

## About The Project

Jenkins is a self-contained, open source automation server which can be used to automate all sorts of tasks related to building, testing, and delivering or deploying software.

In this project, we will integrated Github repository with Jenkins and send mail automatically to Github committer if build failed.

## Built With

To do it we need to install Jenkins in our local Machine.

## Getting Started

First we need to go the Dashboard of Jenkins and click New Item option:

![DashBoard](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/94acc698-315f-4bea-855d-5c9a9cc19286)

Then gave the name of the project, select FreeStyle project and hit Ok.

![FreeStyleProject](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/1a84d7ad-f485-4868-83ee-36c1a1ac3771)

Then navigate through Configure -> Source Code Management and select Git.
Give the Repository URL(if needed give credential also. As it is a public project so no credential is needed).

![SourceCodeManagement](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/7f5ce0c7-4883-4b18-9428-214b46f6d602)

After that, under Build Triggers options select Poll SCM and in Schedule box write * * * * * which is an expression that specifies the schedule for the job run. 
The five fields in the expression represent, in order, the minutes (0-59), hours (0-23), days of the month (1-31), months (1-12), and days of the week (0-7, where both 0 and 7 represent Sunday).

So, * * * * * means every minute, every hour, every day of the month, every month, and every day of the week.

![BuildTriggers](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/9d3a0817-6004-4398-9a01-a21ffeba4150)

Then under Build Steps option select Execute Windows batch command
from drop down options and run the following Script:
for /f "usebackq delims=" %%a in (`git log -1 "--pretty=format:%%ae"`) do set COMMITTER_EMAIL=%%a
echo The committer email is %COMMITTER_EMAIL%
setx MAIL_RECIPIENT "%COMMITTER_EMAIL%"

this runs a for loop to extract the email address of the last committer using the git log command and setx command makes the variable available to other processes

![BuildSteps](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/c3265f4e-afa2-4f54-9c6d-f00eb1be4a67)

Then Post-build Actions select Editable Email Notification from dropdown. Under Project Recipient List write $MAIL_RECIPIENT which store the email address. Under Default Subject and Default Content options set required data to be mailed.
![ProjectReciepientList](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/02cd0727-8082-48a0-af65-6bb4a726c8c0)
![DefaultSubjectAndContent](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/e9738bd8-5afe-4ac1-82fe-5189fed97b95)




### Prerequisites

This is an example of how to list things you need to use the software and how to install them.

* npm

```sh
npm install npm@latest -g
```

### Installation

1. Get a free API Key at [https://example.com](https://example.com)

2. Clone the repo

```sh
git clone https://github.com/your_username_/Project-Name.git
```

3. Install NPM packages

```sh
npm install
```

4. Enter your API in `config.js`

```JS
const API_KEY = 'ENTER YOUR API';
```

## Usage

Use this space to show useful examples of how a project can be used. Additional screenshots, code examples and demos work well in this space. You may also link to more resources.

_For more examples, please refer to the [Documentation](https://example.com)_

## Roadmap

See the [open issues](https://github.com/ShaanCoding/ReadME-Generator/issues) for a list of proposed features (and known issues).

## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.
* If you have suggestions for adding or removing projects, feel free to [open an issue](https://github.com/ShaanCoding/ReadME-Generator/issues/new) to discuss it, or directly create a pull request after you edit the *README.md* file with necessary changes.
* Please make sure you check your spelling and grammar.
* Create individual PR for each suggestion.
* Please also read through the [Code Of Conduct](https://github.com/ShaanCoding/ReadME-Generator/blob/main/CODE_OF_CONDUCT.md) before posting your first idea as well.

### Creating A Pull Request

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

Distributed under the MIT License. See [LICENSE](https://github.com/ShaanCoding/ReadME-Generator/blob/main/LICENSE.md) for more information.

## Authors

* **Shaan Khan** - *Comp Sci Student* - [Shaan Khan](https://github.com/ShaanCoding/) - *Built ReadME Template*

## Acknowledgements

* [ShaanCoding](https://github.com/ShaanCoding/)
* [Othneil Drew](https://github.com/othneildrew/Best-README-Template)
* [ImgShields](https://shields.io/)
