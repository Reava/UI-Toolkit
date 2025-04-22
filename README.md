# VPM Package Template (Single)

Starter for making Packages, including automation for building and publishing them.
* This package requires you to follow a handful of steps and read through instructions at least once, please do it, **they are not the exact same as the default VRChat template!**

Once you're all set up, you'll be able to push changes to this repository and have .zip and .unitypackage versions automatically generated, and a listing made which works in the VPM for delivering updates for this package. If you want to make a listing with a variety of packages, check out VRChat's [template-package-listing](https://github.com/vrchat-community/template-package-listing) repo.

## ❓ Why this fork?

* With this, you can setup a new package in your existing dev project within a minute and get working straight on things without having to import and update various SDKs / dependencies.
* This fork was made to allow myself and others to make VPM packages without having to spin a new project per package, which is annoying for small, sometimes even single file packages.
* This also comes with an easy way to theme your "Add to VCC" button colors ! :3

## ▶ Getting Started

* Press [![Use This Template](https://user-images.githubusercontent.com/737888/185467681-e5fdb099-d99f-454b-8d9e-0760e5a6e588.png)](https://github.com/Reava/Template-Single-Package/generate)
to start a new GitHub project based on this template.
  * Choose a fitting repository name and description.
  * Set the visibility to 'Public'. You can also choose 'Private' and change it later.
  * You don't need to select 'Include all branches.'
* Clone this repository locally using Git into an adequately named package folder in the unity project of your choice (for ex: "com.yourname.template")
  * If you're unfamiliar with Git and GitHub, [visit GitHub's documentation](https://docs.github.com/en/get-started/quickstart/git-and-github-learning-resources) to learn more.
* Open the new folder in your file explorer
* Edit the source.json and package.json file with any text editor of your choice to fill in the info
* Edit the lines 7 to 9 in release.yml in the .GitHub/workflows folder of your new package with the same info

## 🚇 Migrating Assets Package
Full details at [Converting Assets to a VPM Package](https://vcc.docs.vrchat.com/guides/convert-unitypackage)

## ✏️ Working on Your Package

* Delete the "Runtime/Readme.txt" file or reuse it for your own package.
* Update the  file in the "Packages" directory to include your package.
* When you're ready, commit and push your changes.
* Once you've set up the automation as described below, you can easily publish new versions.

## 🤖 Setting up the Automation

Go to the "Settings" page for your repo, then choose "Pages", and look for the heading "Build and deployment". Change the "Source" dropdown from "Deploy from a branch" to "GitHub Actions".

That's it!
Some other notes:
* We highly recommend you keep the existing folder structure of this template.
  * The root of the project should be a Unity Package folder.
* If you want to store and generate your web files in a folder other than "Website" in the root, you can change the `listPublicDirectory` item [here in build-listing.yml](.github/workflows/build-listing.yml#L17).

## 🎉 Publishing a Release

You can make a release by running the [Build Release](.github/workflows/release.yml) action. The version specified in your `package.json` file will be used to define the version of the release.
(You can use -pre.1 at the end to mark it as a prerelease and only appear when users enable it in the VCC)

## 📃 Rebuilding the Listing

Whenever you make a change to a release - manually publishing it, or manually creating, editing or deleting a release, the [Build Repo Listing](.github/workflows/build-listing.yml) action will make a new index of all the releases available, and publish them as a website hosted fore free on [GitHub Pages](https://pages.github.com/). This listing can be used by the VPM to keep your package up to date, and the generated index page can serve as a simple landing page with info for your package. The URL for your package will be in the format `https://username.github.io/repo-name`.

## 🏠 Customizing the Landing Page (Optional)

You can edit the file 'Website/ColorScheme.css' and remove the comments on the theme color section you want to use for non-default buttons
* If you want to customize your buttons color on your default VRChat template, simply import [ColorScheme.css](https://github.com/Reava/Template-Single-Package/blob/main/Website/ColorScheme.css) to your Website folder, then add the line ```<link rel="stylesheet" href="ColorScheme.css">``` in the header of the 'Website/index.html' file of your own package!

The action which rebuilds the listing also publishes a landing page. The source for this page is in `Website/index.html`. The automation system uses [Scriban](https://github.com/scriban/scriban) to fill in the objects like `{{ this }}` with information from the latest release's manifest, so it will stay up-to-date with the name, id and description that you provide there. You are welcome to modify this page however you want - just use the existing `{{ template.objects }}` to fill in that info wherever you like. The entire contents of your "Website" folder are published to your GitHub Page each time.