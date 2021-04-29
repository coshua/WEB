For JavaScript, regex variable can be declared as following format
`var reg = /word/;`

`reg = /a|b/; //or operator`

`reg = /a/i; //case insensitive`

`var result = reg.test(sentence); //boolean`

`var result = sentence.match(reg); //array contains one matching words`

`result = sentence.match(/reg/g); //array contains all matching words`

`reg = /a./; //wildcard character .`

`reg = /a[bc]/; //only allow 'b' or 'c' after 'a'`

`reg = /a[b-e1-9]/; //only allow range of alphabets b-e after 'a'. Also applicapable to numbers.`

`reg = /[^abc]/; //negated character set. Find except a or b or c.`

`reg = /a+/; //one or more serial 'a'`

`reg = /Aa*/; //zero or more seiral 'a'`

By default, Regular expressions are greedy, which returns the longest possible matching string. 

`reg = /a*?/; //You can do lazy-matching using ?`

`reg = /^Cal/; //Car should appear at the beginnings of the string. You can search the end of the string using dollar sign $. /val$/`

`reg = /\w/; // \w equals to [A-Za-z0-9_].`

`reg = /\W/; // \W equals to ^\w`

`/\d/ equals to [0-9], and \D = [^0-9]`

`/\s/ finds whitespace \S non-whitespace`

`/\s{3,6}/ {} specifies the number of character. Or use it like {3,} to define Greater than, or use it {3} to define exactly 3`

`/abc?/ matches both 'abc' and 'ab'`

You can replace the matched texts to anything you want with .replace function of String.

`wrongText.replace(regex, String | Function);`

