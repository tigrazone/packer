FIXED by tigrazone@gmail.com  
can be used with Node.js

:warning: :warning: :warning: **DO NOT USE THIS** :warning: :warning: :warning:

I threw this up on npm a long time ago but there are better options now. Packer appears to be unsupported and has bugs like [this](https://github.com/evanw/packer/issues/9) that cause it to generate invalid JavaScript. I recommend using a community-supported JavaScript minifier such as [uglify](https://github.com/mishoo/UglifyJS2/) instead. I'm only keeping this page up on GitHub because some packages likely depend on this package and may attempt to navigate here.

# packer.js

This is a simple port of [/packer/](http://dean.edwards.name/packer/) by Dean Edwards to node.js.

## Installation

If you use [npm](https://github.com/isaacs/npm):

    npm install packer

If you don't use npm, clone this repository or download the latest version using the GitHub repository Downloads link.

## Usage

This module contains one function called `pack(script, base62, shrink)`:

    > var packer = require('packer');
    > packer.pack('1 + 2');
    '1+2'
    > packer.pack('', true);
    'eval(function(p,a,c,k,e,r){e=String;if(!\'\'.replace(/^/,String)){while(c--)r[c]=k[c]||c;k=[function(e){return r[e]}];e=function(){return\'\\\\w+\'};c=1};while(c--)if(k[c])p=p.replace(new RegExp(\'\\\\b\'+e(c)+\'\\\\b\',\'g\'),k[c]);return p}(\'\',2,0,\'\'.split(\'|\'),0,{}))'

It also adds the `packer` command:

    $ node ./cli.js -h
    usage: <script> [options]

    options:
    -i FILE	Input file (default stdin)
    -o FILE	Output file (default stdout)
    -b	Base62 encode
    -s	Shrink variables

    $ echo 1 + a | node ./cli.js -b
    eval(function(p,a,c,k,e,r){e=String;if(!''.replace(/^/,String)){while(c--)r[c]=k[c]||c;k=[function(e){return r[e]}];e=function(){return'\\w+'};c=1};while(c--)if(k[c])p=p.replace(new RegExp('\\b'+e(c)+'\\b','g'),k[c]);return p}('1+0',2,2,'a|'.split('|'),0,{}))
