## What?
This allows to extract urls from the url page of [**Remote Devices**](chrome://inspect/#devices)       (chrome://inspect/#devices) for Chrome  and copy it to your clipboard.
I can then import them in a Chrome's backup tabs extension ( I use [*Session Buddy*](https://chrome.google.com/webstore/detail/session-buddy/edacconmaakjimmfgnblocblbcdcpbko?hl=en) ).


## Why?
From time to time I do need to *sync* my tabs from my phone (Android) to my Desktop and this is not really feasible even with the "tabs from other devices" features of chrome which is not very accurate or sync in real time.


## How?
 **Part of the steps below are explained [there](https://maemol.github.io/2019-04-15-Android-Export-chrome-tabs/)**
 
 1. Go to the Remote Devices of Chrome (full explanation [here](https://maemol.github.io/2019-04-15-Android-Export-chrome-tabs/))  
 *Go to `chrome://inspect/#devices`
  or  press  `ctrl+shift+j` or `F12` to open developer pane then go to the `3 dots` => `more tools` => `remote devices`*

2. When you are on the script part, use this script instead 

``` js
var tabsNodes = document.querySelectorAll('.browser>.list.pages>.row')
var tabsAsText = Array.from(tabsNodes).map((t) => t.querySelector(".name").innerText + "\n" + t.querySelector(".url").innerText + "\n")
copy(tabsAsText.join("\n"))
```
3. (optional) If you have url with more than 100 characters, you might try this as mentionned [here](https://gist.github.com/codebling/3b7bfdbfbabf7bc17d8566b92854b4c3#comments) by [7UR7L3](https://github.com/7UR7L3) :
>Version for **Chrome 81.\*** still works on **Chrome 83.\*** but note that the `.url` divs are capped to 100 chars.
>
> If you open the dev console -> sources -> page/top/inspect/inspect.js
> and `ctrl+f` for 100 you should be able to comment out these lines
> (select and `ctrl+/`)
> ```js
> if (text.length > 100) {
>     text = text.substring(0, 100) + '\u2026';
  > }
> ```
> 
> Either do this shortly after a page reload (you have plenty of time)
> or just unplug and replug the phone and the list will update with the
> full urls.
> 
> Edit: see Ben J's comment on this answer here
> https://android.stackexchange.com/a/193858/326682 .


