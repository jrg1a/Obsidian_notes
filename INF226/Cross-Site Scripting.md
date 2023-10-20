Cross-Site Scripting (XSS) is a common web application security vulnerability that allows attackers to inject malicious scripts into web pages viewed by other users. XSS occurs when an application fails to properly sanitize user-supplied input, allowing untrusted data to be included in web pages without proper validation.

There are three main types of XSS attacks:
1. Stored XSS:
    - In a stored XSS attack, the malicious script is permanently stored on the target server, such as in a database or a message board.
    - When a user accesses the affected page, the script is served along with the legitimate content and executed in the user's browser.
    - This type of attack can have long-lasting effects as the malicious script is served to every user who visits the compromised page.
2. Reflected XSS:
    - Reflected XSS attacks occur when the malicious script is embedded within a URL or another input field and is immediately returned to the user by the server.
    - The user's browser then executes the script as part of the page rendering process.
    - These attacks often involve social engineering techniques to trick users into clicking a specially crafted link.
3. DOM-based XSS:
    - DOM-based XSS attacks exploit vulnerabilities in the Document Object Model (DOM) of a web page.
    - The attack occurs when the client-side JavaScript code manipulates the DOM in an unsafe way, allowing the injection and execution of malicious scripts.
    - Unlike stored and reflected XSS attacks, DOM-based XSS attacks do not involve server-side vulnerabilities.

The impact of XSS attacks can vary depending on the attacker's objectives, ranging from stealing sensitive user information to defacing websites, spreading malware, or hijacking user sessions. The consequences can include data breaches, compromised user accounts, and reputational damage to organizations.

## Samy Worm
The Samy worm, also known as JS.spacehero, was a notable cross-site scripting (XSS) attack that targeted the social networking site MySpace in 2005. It was created by a programmer named Samy Kamkar and quickly became one of the most widespread and fastest-spreading worms in the history of the internet.

- The attack exploited a vulnerability in MySpace's implementation of user profiles and JavaScript functionality. By injecting malicious code into his own profile, Samy Kamkar was able to exploit the trust relationship between users on MySpace and propagate the worm to other user profiles.
- When a user visited Samy's infected profile, the worm's script executed and automatically added Samy as a friend. It also inserted a snippet of code into the user's profile that replicated the worm and spread further when other users visited their profiles. This self-replicating behavior allowed the worm to rapidly spread across the MySpace network.
- The Samy worm had a significant impact due to its ability to propagate itself to millions of users within a short period of time. It overwhelmed the MySpace infrastructure and caused disruptions to the site's functionality. MySpace had to temporarily shut down to contain the spread and remove the malicious code from affected profiles.
- The Samy worm highlighted the dangers of XSS vulnerabilities and the potential for widespread damage. It demonstrated the impact that a single user's malicious action could have on a large-scale social networking platform.
- Following the Samy worm incident, MySpace and other websites implemented stricter security measures and improved their handling of user-generated content to mitigate XSS attacks. It served as a wake-up call for the importance of secure coding practices, input validation, and output encoding to prevent such vulnerabilities.
- The Samy worm stands as a notable example of the potential harm that can arise from XSS attacks and emphasizes the ongoing need for robust security practices to protect web applications and user data.
- MySpace had some protections against this:
	- Only allow: ``<a>, <img> and <div>``
	- Strip out any occurrence of the word ``javascript``
- But JavaScript in CSS style attributes meant any tag could be used:
	- ``<div style="background:url('javascript:alert(1)')">``
- And: Browsers will actually also accept ``java\nscript:``
	- ``<div style="background:url('javascript:alert(1)')">``
- More data could be hidden in other attributes:
```CSS
<div id="mycode"  
expr="alert('hah!')"  
style="background:url('javascript:eval(document.all.mycode.expr)')">
```
- The whole code of ``JS.spacehero``, with explanation can be found [here](https://samy.pl/myspace/tech.html)

## Same-Origin Policy
The Same-Origin Policy (SOP) is a security mechanism implemented in web browsers to prevent web pages from accessing data or interacting with resources from different origins. It is a fundamental security concept in web applications and helps protect user data and prevent cross-site scripting (XSS) attacks.

The SOP defines that a web page can only access resources (such as JavaScript objects, cookies, or HTML content) from the same origin. An origin consists of three components: the protocol (e.g., HTTP or HTTPS), the domain (e.g., example.com), and the port number. For example, if a web page is loaded from `https://www.example.com`, it can only interact with resources from the same origin, such as `https://www.example.com/some-page` or `https://www.example.com/api`.

The Same-Origin Policy ensures that malicious scripts or web pages cannot access sensitive data or perform unauthorized actions on behalf of the user by manipulating resources from different origins. It prevents cross-site scripting attacks where an attacker injects malicious code into a trusted website and steals user data or performs malicious actions.

However, there are some exceptions and techniques that allow controlled communication between different origins, such as Cross-Origin Resource Sharing (CORS) and server-side proxies. These mechanisms provide controlled access to resources from different origins while maintaining security.

Adhering to the Same-Origin Policy is crucial for web application security. Developers need to be aware of its implications when designing and implementing web applications, ensuring that sensitive data and functionality are protected from unauthorized access or manipulation. Additionally, web browser vendors continually improve and enforce the Same-Origin Policy to enhance the security of web browsing experiences.

- The same-origin policy restricts scripts run in the browser to only access resources from the same origin.
- Example:
	- A script can only access the DOM for pages in the same origin.
	- A script can only access local storage from the same origin.
	- A script can only send ``XMLHttpRequest`` [[WEB Requests#General Headers|GET/POST requests]] to the same origin.
- Exception:
	- Cookies are actually **not covered** by same origin policy by default. 
	- Cookies from https://example.com/ will be sent to http://example.com/.
- The following URLs have the same origin:
	- http://www.geocites.com/bob/index.html
	- http://www.geocites.com/eve/script.html

## XSS Examples
Cross-site scripting (XSS) is a type of security vulnerability where an attacker injects malicious code (usually JavaScript) into a trusted website. When users visit the compromised website, their browsers unknowingly execute the injected code, which gives the attacker access to sensitive data or enables them to perform malicious actions on behalf of the user.
- Web browser insulate resources, such as cookies or JavaScript, from different origins
- Cross-site scripting (XSS) occurs when a web-server unintentionally serves JavaScript from an attacker to client browsers.
- This allows attacker code to access resources from victim server origin.

In an XSS attack, the attacker's goal is often to bypass the Same-Origin Policy by tricking the victim's browser into executing their malicious code in the context of the victim's trusted website. By doing so, the attacker's code can access resources from the victim's server origin, potentially compromising sensitive data or performing unauthorized actions.

**Example:**
```php
$username = $_GET['username'];  
echo '<div class="header"> Welcome, ' . $username . '</div>';
```
- In this code, the value of the `username` parameter is directly used to generate HTML output without any validation or sanitization. This can lead to a cross-site scripting (XSS) vulnerability if an attacker manipulates the `username` parameter to include malicious JavaScript code.
- Here's how an attacker could exploit this vulnerability:
	1. Stealing session cookies: The attacker can inject JavaScript code that captures the user's session cookies and sends them to an external server. This allows the attacker to impersonate the user and perform actions on their behalf.
	2. Fake login screen: The attacker can inject JavaScript code that creates a fake login screen overlaying the current page. When the user enters their credentials, the code captures the input and sends it to the attacker. This can trick users into disclosing their passwords or other sensitive information.
	3. Mining bitcoins: The attacker can inject JavaScript code that uses the user's computing resources to mine cryptocurrencies, such as Bitcoin, without their knowledge or consent. This can slow down the user's device and consume their resources.
- To prevent XSS attacks, it's crucial to properly validate and sanitize user input before using it in dynamically generated HTML content. In the given example, you should sanitize the `username` input to ensure that it doesn't contain any HTML or JavaScript code that could be executed.
- One way to mitigate this vulnerability is by using output encoding or escaping techniques. In PHP, you can use functions like `htmlspecialchars` or `htmlentities` to encode special characters and prevent them from being interpreted as HTML or JavaScript code.
- Here's an updated version of the code with proper output encoding:
```PHP
$username = $_GET['username'];
echo '<div class="header"> Welcome, ' . htmlspecialchars($username) . '</div>';
```
- By using `htmlspecialchars`, any HTML special characters in the `username` value will be converted to their corresponding HTML entities, ensuring that the output is displayed as plain text and not interpreted as code.
- It's essential to always validate and sanitize user input, especially when it is used in dynamically generated HTML content, to prevent XSS attacks and protect users from potential harm.

## Vectors
A common way in which attackers can inject scripts or exploit vulnerabilities in web applications. Let's explore each of them:
1. User data visibility: In certain scenarios, user data that is intended to be private or limited to a specific user can become visible to other users. This can occur due to improper access controls, misconfigurations, or flaws in the application logic. Attackers can manipulate user data to inject malicious scripts that can be executed by unsuspecting users. 
2. URL variables: Web applications often use URL parameters to pass data between different pages or to retrieve specific content. If the application fails to properly validate and sanitize the URL parameters, an attacker can manipulate them to inject malicious scripts. This can be particularly dangerous if the injected scripts are executed within the context of the affected page. 
3. User data from [[WEB Requests#Entity Headers|POST Requests]]: Web forms that allow users to submit data via POST requests are also potential sources of script injection. If the application does not validate or sanitize user input before processing it, an attacker can submit specially crafted data containing malicious scripts. This can lead to script execution within the application's context and potential exploitation.
4. Evaluating user data in client-side scripts: Many modern web applications rely on client-side scripts, such as JavaScript, to enhance interactivity and functionality. However, if the application blindly evaluates user-supplied data in client-side scripts without proper validation and sanitization, it can introduce security vulnerabilities. Attackers can exploit this by injecting malicious scripts that are executed by the user's browser.

To mitigate these risks and prevent script injection attacks, it is crucial to implement proper input validation and output encoding. Input validation ensures that user-supplied data meets the expected format and constraints, while output encoding ensures that any data displayed to users is properly encoded to prevent script execution.

Additionally, employing security measures such as Content Security Policy (CSP) can help mitigate the impact of script injection attacks. CSP allows web developers to define a whitelist of trusted sources for scripts, stylesheets, and other resources, effectively limiting the potential sources of injected scripts.

By adopting secure coding practices, performing input validation and output encoding, and staying updated on security best practices, developers can help protect their web applications against script injection attacks and safeguard user data.

## XML HttpRequest
```JavaScript
var xhttp = new XMLHttpRequest();  
xhttp.onreadystatechange = function() {  
	if (this.readyState == 4 && this.status == 200) {  
		// Replace the content of "example" element  
		// with HTML received from reqest:  
		document.getElementById("example").innerHTML = xhttp.responseText;  
	}  
};  
xhttp.open("GET", "newcontent", true);  
xhttp.send();
```
- This demonstrates the usage of XML HttpRequest (XHR) in JavaScript to make an HTTP request to the current origin. XHR is commonly used in web development to fetch data from a server without requiring a page reload. However, it is important to note that XHR requests are subject to the same-origin policy, which restricts requests to the same origin (protocol, domain, and port) as the page making the request.
- In the given example, the XHR object is created using `new XMLHttpRequest()`. An event handler is assigned to the `onreadystatechange` event, which triggers whenever the state of the XHR changes. The function inside the event handler is executed when the XHR reaches the `readyState` 4 (indicating that the request has been completed) and the `status` 200 (indicating a successful response).
- In the code, upon a successful response, the content of the element with the ID "example" is replaced with the response received from the server using `xhttp.responseText`. This enables dynamic updating of content on the web page without a full page reload.
However, it is important to understand that if an attacker successfully injects a script into a vulnerable page, they can make use of XHR or similar techniques to perform various actions on behalf of the user. This includes making [[WEB Requests#Entity Headers|GET]] and [[WEB Requests#Entity Headers|POST]] requests to interact with the server, potentially causing [[Authentication|unauthorized]] actions or data manipulation.

The Samy worm example you mentioned exploited this capability by using XHR to send POST requests to update the user's profile and add the user "samy" as a friend. The worm was able to propagate and spread by injecting itself into user profiles, taking advantage of the trust associated with user-generated content.

To prevent such attacks, it is crucial to implement proper input validation, output encoding, and server-side security measures. Input validation should be performed to ensure that user-supplied data is within the expected boundaries and does not contain malicious content. Additionally, server-side controls should be in place to authenticate and authorize user actions, preventing unauthorized or malicious requests from being processed.

Overall, understanding the capabilities and limitations of XHR requests, as well as implementing appropriate security measures, is essential to mitigate the risks associated with script injection attacks and protect web applications and their users.

## XSS Prevention Strategies
XSS Prevention Strategies involve a combination of input filtering, output encoding, and following specific best practices. Here are some strategies to mitigate XSS vulnerabilities:

### Filtering Input:
- Use a whitelist approach to validate and sanitize user input. Only allow specific characters, patterns, or data types based on expected values.
- Perform server-side input validation to ensure that input adheres to the expected format and reject any malicious or unexpected data.
- Sanitize user-generated content by removing or encoding potentially dangerous characters or HTML tags.

### Escaping Output
- Properly encode or escape user-generated data before displaying it in HTML, JavaScript, CSS, or other contexts.
- HTML encoding: Convert special characters to their HTML entities using functions like `htmlspecialchars()` in PHP or equivalent methods in other languages.
- JavaScript encoding: Use functions like `encodeURIComponent()` or libraries like OWASP Java Encoder to encode user data within JavaScript code.
- CSS encoding: Ensure that user input is properly escaped when used as part of CSS styles or selectors.

### The Don'ts
- Avoid inserting untrusted data directly into HTML tags, attribute names, scripts, or CSS styles.
- Example of a vulnerable code snippet:
```HTML
<div class="<?php echo $_GET['classname']; ?>">Content</div>
```
- Instead, sanitize the input and validate against a whitelist of allowed values before using it in HTML.

### Context-Specific Best Practices
- Avoid inserting untrusted data directly into JavaScript code:
```javascript
var userInput = '<?php echo $_GET['input']; ?>';
```
- Instead, encode the data properly using functions like `json_encode()` or use a data attribute to pass user input.
- Avoid inserting untrusted data directly into CSS styles:
```html
<div style="background: <?php echo $_GET['color']; ?>"></div>
```
- Instead, validate and sanitize user input before using it in CSS styles.

### More Gotchas
- Be cautious when formatting user-generated content. Certain formatting techniques may inadvertently introduce XSS vulnerabilities. For example, using `eval()` or `new Function()` to process user input as code can lead to code injection vulnerabilities.
- ``{ background-url : "javascript:alert(1)"; }``
- ``{ text-size: "expression(alert('XSS'))"; }``
- [OWASP XSS Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)


Remember, the key is to implement multiple layers of defense. Always validate and sanitize input, encode output in the appropriate context, and follow best practices specific to each usage scenario. Additionally, keeping software and libraries up to date, implementing a content security policy (CSP), and conducting regular security assessments can help strengthen the overall security posture of web applications.

## Markup injection
also known as HTML injection, is a web security vulnerability that occurs when untrusted user input is included in a web page without proper validation or sanitization. It allows an attacker to inject malicious markup code into the rendered page, potentially leading to various attacks or unwanted behavior.

The attacker may exploit the vulnerability by injecting HTML, XML, or other markup tags, along with attributes and event handlers. This can result in several adverse consequences, such as:
1. Cross-Site Scripting (XSS): The injected markup can contain JavaScript code that executes in the context of the victim's browser, leading to XSS attacks. For example, the attacker could inject a `<script>` tag to execute arbitrary code. 
2. Phishing Attacks: By injecting HTML forms or links, the attacker can trick users into revealing sensitive information or performing unintended actions.
3. Malicious Redirects: The attacker can inject HTML elements such as `<meta>` tags or JavaScript-based redirects to redirect users to malicious websites or perform unauthorized actions.
4. Defacement: The attacker can modify the appearance or content of the web page by injecting unwanted markup, potentially damaging the website's reputation or causing confusion for users.

To prevent markup injection, it is crucial to implement proper input validation and output encoding practices:
- Input Validation: Validate and sanitize user input to ensure it adheres to the expected format and restrict any potentially malicious markup. Use whitelisting approaches to validate input against an allowed set of characters or patterns.
- Output Encoding: Properly encode user-generated content before displaying it in HTML, XML, or other markup languages. Encode special characters using entity encoding or other appropriate encoding methods. For example, `<` becomes `&lt;` and `>` becomes `&gt;`.

HTML templating systems can provide an extra layer of protection against markup injection. Templating engines allow separating code logic from presentation, reducing the risk of mixing untrusted user input with markup. Templating systems often have built-in mechanisms for context-aware output encoding, automatically escaping user input to prevent markup injection vulnerabilities.

By implementing strong input validation, output encoding, and utilizing secure templating systems, developers can mitigate the risk of markup injection attacks and ensure the integrity and security of their web applications.

## Content Security Policy
Content Security Policy (CSP) is a security mechanism that helps protect web applications from various types of attacks, such as Cross-Site Scripting (XSS) and data injection vulnerabilities. It provides a way for web developers to define a set of policies that control which types of content and sources are allowed to be loaded and executed on a web page.

CSP works by allowing web developers to specify a Content-Security-Policy HTTP header or a `<meta>` tag within the HTML document. The policy consists of directives that define the allowed sources for various types of content, such as scripts, stylesheets, images, fonts, and more. These directives define the whitelist of trusted sources from which the browser can load resources.

Some common directives used in CSP include:
- `default-src`: Specifies the default source for all content types if a more specific directive is not defined.
- `script-src`: Specifies the allowed sources for JavaScript code.
- `style-src`: Specifies the allowed sources for CSS stylesheets.
- `img-src`: Specifies the allowed sources for images.
- `font-src`: Specifies the allowed sources for fonts.
- `connect-src`: Specifies the allowed sources for network connections, such as AJAX requests or WebSockets.
- `frame-src`: Specifies the allowed sources for embedding frames or iframes.
- `object-src`: Specifies the allowed sources for embedded objects, such as Flash or Java applets.
- `media-src`: Specifies the allowed sources for media elements, such as audio or video.

By defining strict CSP policies, web developers can prevent the execution of malicious scripts or the loading of unauthorized resources from untrusted sources. If a web page attempts to load content from a source not specified in the CSP policy, the browser will block the request and prevent potential security vulnerabilities.

CSP can also provide additional security features, such as reporting mechanisms that allow developers to receive reports when a policy violation occurs. This helps in monitoring and identifying potential security threats or misconfigurations.

Implementing CSP requires careful consideration of the specific needs and requirements of the web application. Developers should thoroughly test and validate the policy to ensure it does not inadvertently block legitimate content or disrupt the functionality of the web application.

Overall, CSP is a powerful security measure that helps enhance the security posture of web applications by mitigating the risks associated with content injection and unauthorized resource loading. It provides an additional layer of defense against common web vulnerabilities and helps protect users from malicious attacks.

Here are some examples of CSP directives:
- Allowing content from specific sources:
```CSS
Content-Security-Policy: default-src 'self' example.com
```
- Allowing inline scripts and styles:
	- This directive allows inline scripts and styles to be executed from the same origin (`'self'`). Note that using `'unsafe-inline'` should be done cautiously as it increases the risk of XSS vulnerabilities.
```css
Content-Security-Policy: script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'
```
- Restricting the use of eval and inline event handlers:
	- This directive prevents the use of `eval` and inline event handlers (`'none'`) and restricts the base URI to the same origin (`'self'`).
```css
Content-Security-Policy: script-src 'self'; object-src 'none'; event-source 'none'; base-uri 'self'
```
- Allowing content from multiple sources:
	- This directive allows scripts to be loaded from the same origin (`'self'`) and from the CDN domain `cdn.example.com`, and allows inline styles from the same origin and the CDN domain.
```css
Content-Security-Policy: script-src 'self' cdn.example.com; style-src 'self' 'unsafe-inline' cdn.example.com
```
- Using a report-uri for policy violations:
	- This directive sets the policy for the default sources to the same origin (`'self'`) and specifies the URL where policy violation reports should be sent (`/csp-report-endpoint`).
```css
Content-Security-Policy: default-src 'self'; report-uri /csp-report-endpoint
```

These examples demonstrate how CSP directives can be used to define the allowed sources for different types of content. The specific directives and their values will depend on the requirements and security considerations of the web application. It is important to carefully craft the CSP policy to strike a balance between security and the functionality of the application.

## Summary
Cross-Site Scripting (XSS) is a web security vulnerability that allows attackers to inject malicious scripts into web pages viewed by other users. It occurs when a web application does not properly validate or sanitize user-generated input, allowing unauthorized execution of scripts in a victim's browser. XSS attacks can have various consequences, such as stealing sensitive information, hijacking user sessions, defacing websites, or spreading malware.

Preventing XSS requires a multi-layered approach. Input validation and sanitization techniques should be employed to ensure that user-generated data is properly handled. Output encoding or escaping should be applied to prevent the execution of injected scripts. Content Security Policy (CSP) can be implemented to define a set of security policies that restrict the sources of content that a browser can load. Regular security testing and code reviews are also crucial to identify and fix potential vulnerabilities.

To mitigate XSS attacks, it is essential to educate developers about secure coding practices, implement security controls at different levels of the application stack, and stay updated with the latest security patches and best practices. By addressing XSS vulnerabilities, organizations can enhance the security and trustworthiness of their web applications, protecting both users and sensitive data from potential exploits.