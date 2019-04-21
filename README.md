One of the newest requirements was being able to use React in Microsoft Sharepoint. While I was not new to Sharepoint or react separately, I never worked on these technologies with dependency on each other.

It was a nice blend of React and Sharepoint API but the catch was using TypeScript to code react. While coding AngularJS I learnt TypeScript but left it once I switched to ReactJS. 

I had created a full fledged react application with created using create-react-app - fully functional and meeting the requirement of the client all written in Javascript but not in TypeScript..

So the hunt started.. There were so many ideas .....a) converting the existing application to support TypeScript.. how  but had no idea on how to do it.. besides TypeScript had its own set of rules..b) Using TypeScript based create-react-app. c) Learning TypeScript from scratch  d) Using React Sharepoint Framework (SPFx) to generate boilerplate start up code that supports Sharepoint, TypeScript and React (yo @microsoft/sharepoint) e) Online Converters to convert JavaScript to TypeScript.. etc..

Option 'a' had quite a few KB articles and the one from the official TypeScript was very useful too. However, none answered the questions I had in full. 

Option 'b' looked promising.. but I wanted my existing create-react-app application to support TypeScript..

Option 'c' was going to take a long time I felt (actually I fixed all the errors while converting JavaScript to TypeScript and it took less than 2 days to figure out how TypeScript needs to be coded)

I ran into issues with option 'd' on a windows 7 64 bit machine. The installation failed at gulp serve which was critical to compile and run the changes.. so I had to drop that option.  I was able to install it later on a Windows 10 machine on cloud but that option was needed for Sharepoint Integration and not immediately..

I chose Option 'a' to convert the existing create-react-app application that had the fully functional ReactJS code in JavaScript to support TypeScript.  Here are the steps followed..

1) First, in the project command prompt, install the TypeScripts types as below. I understood that @type represent the TypeScript types.. we need to install TypeScript types for supporting React types in TypeScript.. so we install these packages first. In fact we do the same thing for every library that needs to be used in our application with support for TypeScript. For example I used uuid.. The npm install for the TypeScript version of this library is @types/uuid.. rest of the installation process is the same.. npm install --save-dev @types/uuid..as opposed to npm install --save-dev uuid for the JavaScript version..

npm install --save react react-dom @types/react @types/react-dom

2) Next add development-time dependencies on awesome-typescript-loader and source-map-loader. It should hardly take any time (I still feel this step is not required, I did it anyway)

npm install --save-dev typescript awesome-typescript-loader source-map-loader

awesome-typescript-loader helps Webpack compile your TypeScript code using the TypeScript’s standard configuration file named tsconfig.json. 

3) Add a TypeScript configuration file.. TypeScript looks for this file for. You could use the barebones configuration provided in the above TypeScript site.

Create a tsconfig.json file  in the same path as the package.json file and copy this configuration.

{
    "compilerOptions": {
        "outDir": "./dist/",
        "sourceMap": true,
        "noImplicitAny": true,
        "module": "commonjs",
        "target": "es6",
        "jsx": "react"
    },
    "include": [
        "./src/**/*"
    ]
}

4) Write a few TypeScript files.. bear in mind that files with .ts extension are for plain TypeScript components and any file that needs support for React shall have the extension .tsx (like the equivalent Javascript version of .jsx). 
Go ahead and create the Hello Component and Index.tsx described in the https://www.typescriptlang.org/docs/handbook/react-&-webpack.html

In the project folders, you will find index.js, components and containers folders that contain both *.ts and *.tsx files and interfaces folder that contain Types defined in TypeScripts used by the application. 

5) Webpack.config.js: Create-react-app internally uses webpack. We are not required to install webpack separately. With create-react-app, we are not required to deal with webpack.config.js files. They are pre-built and packed and insulated from changes. So if you are using create-react-app to run TypeScript, you really dont need to change any settings in webpack.config.js even if you locate it :-)

You will be glad to know that the moment the project in opened in VS Code, support for TypeScript is automatically provided and syntax highlight comes to play immediatley.

6) Bootstrap: Since index.js relies on App.js, I renamed App.js to something else and provided an App.tsx file instead which bootstrapped the application.

7) Running application: this is the same old command used with create-react-app based applications.  npm start

8) Making changes:  Use VS Code to edit the solution. The syntax highlight support for TypeScript is superb. Through it I learnt TypeScript.

Happy Coding!!

References:

https://github.com/Microsoft/TypeScript-React-Conversion-Guide
https://www.samatkins.me/post/converting-react-app-typescript/ 
https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html 
https://samhogy.co.uk/2018/09/converting-a-react-app-to-typescript.html, 
https://www.typescriptlang.org/docs/handbook/react-&-webpack.html
https://docs.microsoft.com/en-us/sharepoint/dev/spfx/sharepoint-framework-overview
