## Credits
* [CoreUI Template](http://coreui.io)
* [MSAL for JS](https://github.com/AzureAD/microsoft-authentication-library-for-js/)
* [Stack Overflow thread on the integration](https://stackoverflow.com/questions/52944052/creating-a-single-instance-of-a-class-within-a-vue-application)
* [Sunil Bandla's previous example](https://github.com/sunilbandla/vue-msal-sample)

## Status

One time fork of a cleaned project I was working on to help everyone who has been cursing on getting the integration working like me. ;-)

## Things changed
* src/main.js
* msal/*
* config/*
* router/*
* containers/DefaultHeaderDropdownAccnt.vue
* views/auth/*

## What to expect
### Testing
Browsing to URI/auth/test will give you an isolated testing page

### Header
The header will provide you with a typical flow on how to do a login (redirect method) and logout (redirect to home page)

## Challenges
As the Stack Overflow thread states... Sharing the data/objects across components isn't always easy (understatement). Leveraging the vue root/parent/base instance itself was key to getting everything working. In essence it's providing a wrapper class for the library and initilizing it on the root/parent/base instance.
