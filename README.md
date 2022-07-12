Hi everyone, here's a way to quickly get a react app up and running using Netlify, and then some flags to create in LaunchDarkly to test and demo with.

1. Fork this repo to your account
2. Go to your LaunchDarkly Instance
3. In LD, go to Account settings > Projects > Create Project
	- Give it a name, check the SDKs using Client-Side ID box
	- Details on creating project: https://docs.launchdarkly.com/home/organize/projects#creating-new-projects

# Connecting Netlify
1. Create a https://www.netlify.com/ account if you don't have one yet
2. Add new Site, Import Existing Project
  - It's easiest to sync directly with your Github, and you have the ability to control what repos Netlify has access to
3. Select the ld-demo-app repo and branch
4. Lets give it an appropriate name.
	- In site settings > general > site details > site information > change site name
	- this will also be the domain name
5. Next, go to Build and Deploy Tab
	- Build & Deploy > Continuous Deployment > Build Settings > Build Command
	- Change Command to CI=false npm run build
6. Next scroll down to Environment variables
	- Add a new variable - REACT_APP_LD_SDK_KEY
7. Add your SDK key from LaunchDarkly as the value
		- In LaunchDarklyD, go to the environment you want to test from
		- Press CMD+K (Mac) or CTRL+K (PC)
		- Click Copy SDK Key for the environment
		- Click Client-side-id
    - Add copied sdk-key value in Netlify
    - Save
 
# Creating the flags in LaunchDarkly
 - Go to Test Environment. Now, lets create some flags:
	1. Create a Feature Flag - QR Code
		- name: qrcode
		- key: qrcode
		- description: "This flag enables the view of the QR Code on our application canvas for mobile device viewing"
		- variations: true: qrcode on, false: qrcode off
	2. Create a Feature Flag - Logo Version
		- name: logoversion
		- key: logoversion
		- description: "This flag controls which logo is visible within the application"
		- variations: true: Show Toggle Logo , false: Default LaunchDarkly Logo
	3. Create a Feature Flag - Card Show
		- name: cardshow
		- key: cardshow
		- description: "This flag controls the visibility of the release cards on the bottom of the UI "
		- variations: true: Show Release Cards, false: Disable Card Views
	4. Create a Feature Flag - Upper Image
		- name: upperimage
		- key: upperimage
		- description: "Show the upper image on page"
		- variations: true: Show Image, false: Disable Image
	5. Create a Feature Flag - Login
		- name: login
		- key: login
		- description: "Show the login box for user targeting"
		- variations: true: Login enabled, false: Login Disabled
	6. Create a Feature Flag - Production Header
		- name: prodHeader
		- key: prodHeader
		- description: "Enables the production header view in the UI"
		- variations: true: "Show New Header Design" , false: Show Old Header Design
