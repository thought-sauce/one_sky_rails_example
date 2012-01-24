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

![One Sky Enable Languages](https://github.com/thought-sauce/one_sky_rails_example/raw/master/readme/onesky-enable-languages.png)

For our example we want to enable the following languages;

1. French

2. Chinese (Simplified)

For each of these we're going to set the "Solo" package.

We're going to Translate our strings for each language using Google Translate.

So we go back to the language list and select "Chinese (Simplified)" and click "Translate Now"

![One Sky Translate Now](https://github.com/thought-sauce/one_sky_rails_example/raw/master/readme/onesky-translate-now.png)

We're then going to choose "Machine" translation, select "Google Translate" and click "Translate immediately".

![One Sky Translate Now](https://github.com/thought-sauce/one_sky_rails_example/raw/master/readme/onesky-google-translate.png)

Then go and do the same for "French".

In a few minutes we should receive an email saying;

    Your request for project example_app translate into Chinese Simplified is complete,
	total 9 phrases, 9 successes and 0 failures.
	
![One Sky Translations Complete](https://github.com/thought-sauce/one_sky_rails_example/raw/master/readme/onesky-translations-complete.png)

We can follow the link in the email to see the translations as they are. They are not perfect, but they'll do for now.

## 6. Downloading the translations

This is now super-easy.

We use the second rake task

    rake one_sky:download
	
This will add to our application the files;

* config/locales/fr_FR_one_sky.yml
* config/locales/zh_CN_one_sky.yml

Taking a peek at one of these files, we'll see;

	# PLEASE DO NOT EDIT THIS FILE.
	# This was downloaded from OneSky. Log in to your OneSky account to manage translations on their website.
	# Language code: zh_CN
	# Language name: 简体中文
	# Language English name: Chinese Simplified
	---
	"zh_CN":
	  "content":
	    "home": "尝试改变语言。"
	  "heading":
	    "sidebar":
	      "debug": "调试"
	    "home": "一空示例应用程序"
	  "link":
	    "french": "法国"
	    "english": "英语"
	    "chinese": "中国"
	  "title":
	    "home": "一空Rails的范例"
  
## 7. Improving Translations
  
As expected Google Translate is fine,
But a few of the translations are a bit dodgy.

Let's go back to the One Sky Platform and change some of them.

For consistency we'll make each translation refer to the written language, thereby we will change;

1. "French" to "法文"
2. "English" to "英文"
3. "Chinese" to "中文"

![One Sky Improve Translation](https://github.com/thought-sauce/one_sky_rails_example/raw/master/readme/onesky-improve-translation.png)

Go back to the One Sky Platform, select "Chinese (Simplified)", select "all strings", and find the strings we want to change.

To make the change click "Suggest a new translation".

We come back to the application, and do the same again;

    rake one_sky:download

Now the translations will be updated.
