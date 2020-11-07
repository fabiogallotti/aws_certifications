# AWS CLI & SDK #

In order to use them, you need to enable **Programmatic Access** for the user, so you have an Access Key and a Secret Access Key, and store them in `~/.aws/credentials`. You can store multiple profiles (AWS accounts).

## Command Line Interface (CLI) ##

* Allow you to control multiple AWS services from the command line and automate them through scripts
* Let's you interact with AWS from anywhere using a command line
* It's installed via a Python script
* Important flags:
  * `--profile`, to switch between AWS accounts
  * `--output`, to change output in text, json, table

## Software Development Kit (SDK) ##

* Allow you to control multiple AWS services using popular programming languages
* It's a set of API libraries to integrate AWS services in your app
