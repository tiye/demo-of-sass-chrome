

Demo of SASS in Chrome
------

Tried like Paul Irish demostrated at Google IO:  
http://www.youtube.com/watch?v=x6qe_kVaBpg

I put this demo on Github Pages here:  
http://jiyinyiyong.github.io/demo-of-sass-chrome/html/  
You may open the debugger > Element to see SASS, if possible...  
OK,, the page looks really ugly...

A log here:

### Environment

first, install `sass` with Gem, I mean you need to install `gem` first:

```
gem install sass
```

also, `rb-inotify` is required by `sass` if you want to use `--watch`

```
gem install rb-inotify
```

Then install `gem install slim` for quick generating HTML.

Personally I will use my own commad to auto reload pages:  
https://github.com/jiyinyiyong/doodle  
https://github.com/jiyinyiyong/doodle-crx  
There are also tools from Ruby communities, I'll try later.

Create a file structure like:

```
➤➤ tree
.
|-- css
|   `-- style.css
|-- html
|   `-- index.html
|-- sass
|   `-- style.sass
`-- slim
    `-- index.slim
```

So you can use it to generae HTML

```
slimrb -p slim/index.slim > html/index.html
```

Things just like Jade and Stylus, who copied from Ruby Community.  
Quick starts of SASS and Slim here:  
http://sass-lang.com/tutorial.html  
http://rdoc.info/gems/slim/frames  

------

Looks like Chrome 26 supports the experiments quite bad,  
trying to upgrade it to `google-chrome-dev` 28

Here's a guide about workspaces in Chrome:  
http://ikarishinjieva.github.io/blog/blog/2013/03/05/chrome-workspace/

Guides about using SASS in Chrome:  
http://bricss.net/post/33788072565/using-sass-source-maps-in-webkit-inspector
http://my.umbc.edu/groups/web-dev/news/26213  

But not enough, one need SASS 3.3.0 to make it work.  
http://stackoverflow.com/questions/15940494/sass-support-in-chromer-developer-tools  

There would be Stylus version in the future:
http://stackoverflow.com/questions/9865302/less-sass-debugging-in-chrome-dev-tools-firebug

After some searches and attempts, I finished installing `3.3.0` :  
http://rubygems.org/gems/sass

```
gem install sass -v=3.3.0.alpha.141
```

Finally I saw the `--sourcemap` option

But... Why? It doesn't work...  

```
➤➤ uname -a
Linux laptop 3.8.11-1-ARCH #1 SMP PREEMPT Wed May 1 20:18:57 CEST 2013 x86_64 GNU/Linux
➤➤ ruby --version
ruby 2.0.0p0 (2013-02-24 revision 39474) [x86_64-linux]
➤➤ sass --version
Sass 3.3.0.alpha.141 (Bleeding Edge)
➤➤ google-chrome --version
Google Chrome 28.0.1500.5 dev
```

Found that, after I removed my file out of workspace. It begin to work.  
And it wolln't work every time I save and reload,  
I mean, who knows why it doesn't generate `.map` every time.  

```
➤➤ slimrb -p slim/index.slim > html/index.html
➤➤ >>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
  overwrite css/style.css
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
  overwrite css/style.css
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
  overwrite css/style.css
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
  overwrite css/style.css
  overwrite css/style.css.map
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
  overwrite css/style.css
>>> Change detected to:
.....
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
  overwrite css/style.css
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
  overwrite css/style.css
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
  overwrite css/style.css
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
  overwrite css/style.css
  overwrite css/style.css.map
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
  overwrite css/style.css
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
  overwrite css/style.css
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
  overwrite css/style.css
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
  overwrite css/style.css
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
  overwrite css/style.css
  overwrite css/style.css.map
>>> Change detected to: /opt/s/demo-of-sass-chrome/sass/style.sass
```

"Ctrl + Click" on a propertery goes to the variable, fine.

Then I try using raw file rather than Nginx, still fail.