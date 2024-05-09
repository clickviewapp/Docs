# Plugin Security

## iframe Sandbox Attribute
If you require the use of [iframe sandbox attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe#sandbox) on your iframes, below is the list of tokens that our plugin requires, both for video selection and playback.

|Token|Description|Reason|
|---|---|---|
|`allow-scripts`|Allows the page to run scripts (but not create pop-up windows). If this keyword is not used, this operation is not allowed.|Our application requires scripts for basic operation.|
|`allow-forms`|Allows the page to submit forms. If this keyword is not used, form will be displayed as normal, but submitting it will not trigger input validation, sending data to a web server or closing a dialog.|Allows the user to fill our the login form to sign in.|
|`allow-popups`|Allows popups (like from Window.open(), target="_blank", Window.showModalDialog()). If this keyword is not used, that functionality will silently fail.|Because we allow our users to authenticate via 3rd party identity providers, which quite often lock down frame ancestors, our authentication must happen within a popup.|
|`allow-same-origin`|If this token is not used, the resource is treated as being from a special origin that always fails the same-origin policy (potentially preventing access to data storage/cookies and some JavaScript APIs).|This is required for us to be able to set authentication cookies once the user has signed in.|

### Example

```
<iframe sandbox="allow-popups allow-scripts allow-same-origin allow-forms" {...otherAttributes}></iframe>
```


## Content Security Policy
If your site requires the use of a [Content Security Policy (CSP)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP). Here are the sources that you will need to include:

|Source|
|---|
|`https://*.clickview.net`|
|`https://*.clickviewapp.com`|
|`https://online.clickview.com.au`|
|`https://online.clickview.co.uk`|
|`https://online.clickview.co.nz`|
|`https://online.clickview.us`|

### Example

```
Content-Security-Policy: frame-src https://*.clickview.net https://*.clickviewapp.com https://online.clickview.com.au https://online.clickview.co.uk https://online.clickview.co.nz https://online.clickview.us;
```