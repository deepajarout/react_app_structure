# react_app_structure

**CRUV(Containers, Routes, Utils, Views): Structure React apps in 4 directories and 3 files**
Creating a CRUV app is simple. All you do is generate an app with create-react-app, and then create 4 folders and 2 files. You can try it out by copying and pasting this into your terminal:
```terminal

create-react-app myapp
cd myapp/src
mkdir containers routes utils views
touch config.js contexts.js 
mv App.* routes
sed -i '' -e 's/.\/App/.\/routes\/App/g' index.js

```

