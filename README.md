# One Sky Rails Example

This example is intended to introduce you to how to integrate your Ruby on Rails web application with the
One Sky translation service.

We'll begin from a simple app, with a single page, in 3 languages, and cover;

1. Signing up to the One Sky platform

2. Installing the Gem

3. Creating the One Sky configuration file

4. Uploading your english strings.

5. Using the Platform to provide translations.

6. Downloading the translations.

## 1. Signing up to the One Sky Platform

Signing up to the One Sky Platform is a simple process.

1. Go to [One Sky homepage](http://oneskyapp.com)

![One Sky Home Page](https://github.com/thought-sauce/one_sky_rails_example/raw/master/readme/onesky-homepage.png)

2. Click on [Begin Free Trial](http://oneskyapp.com/sign-up)

3. You'll be required to enter the usual details, plus you will need to choose a subdomain for the app to run at.
(for the means of this tutorial we'll say you chose the domain myname.oneskyapp.com)

4. You'll receive an activation email, follow back to activate, and then set up your project.

5. Back on One Sky's Platform, it'll ask you to "Create New Project"

![One Sky New Project](https://github.com/thought-sauce/one_sky_rails_example/raw/master/readme/onesky-new-project.png)

6. We're going to create a project named "example_app", with the base language "English (US)", and with a single platform "Website"

7. We're done for now!

## 2. Installing the Gem

Simply open up the Gemfile and add in the line

    gem 'i18n-one_sky'
	
Do a quick `bundle install` and everything should be ready.

## 3. Creating the One Sky configuration file

For this we need four pieces of information;

1. The API Public Key

2. The API Secret Key

3. The Project Name

4. The Platform ID

For the API Keys go to the One Sky Platform, click on "Account & Settings", then click on "API Key"
It will display a "Public Key" and a "Secret Key".

![One Sky API Keys](https://github.com/thought-sauce/one_sky_rails_example/raw/master/readme/onesky-api-keys.png)

In this case the "Public Key" is "publicpublicpublicpublicpublic"
and the "Secret Key" is "secretsecretsecretsecretsecret"

The Project Name in our example is "example_app"

The Platform ID is shown on the One Sky Platform, just look where it says "Website (#123)".

![One Sky Platform ID](https://github.com/thought-sauce/one_sky_rails_example/raw/master/readme/onesky-platform-id.png)

In this case the "Platform ID" is 123.

We run the rails generate command with the arguments as follows

    rails generate one_sky:init publicpublicpublicpublicpublic secretsecretsecretsecretsecret example_app 123
	
You should now see a file in the config directory named "one_sky.yml".

The contents should look like

    api_key: publicpublicpublicpublicpublic
    api_secret: secretsecretsecretsecretsecret
    project: example_app
    platform_id: 123
    
## 4. Uploading your English strings

With One Sky setup correctly this should just be a matter of running the rake task.

    rake one_sky:upload

Back on the One Sky Platform you should be able to see all of your strings uploaded (in this case there are 9)

![One Sky All Strings](https://github.com/thought-sauce/one_sky_rails_example/raw/master/readme/onesky-all-strings.png)

## 5. Using the Platform to provide translations

We have to do two things;

1. Enable extra languages.
2. Add the translations.

To enable extra languages, go back to the One Sky Platform, click on the application, and click on the "languages" button.

For our example we want to enable the following languages;

1. French

2. Chinese (Simplified)