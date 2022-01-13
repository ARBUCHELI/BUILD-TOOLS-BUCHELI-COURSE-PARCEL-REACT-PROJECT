# BUILD-TOOLS-BUCHELI-COURSE-PARCEL-REACT-PROJECT

# Building Apps with Parcel

## Learn how to build a web app using Parcel.

Let’s get started!

## Installing Parcel
Parcel, like Webpack, is a Node package. If your project is not a Node.js project, remember that you can initialize Node.js using:

```
npm init -y
```

The project is already a Node.js project. But you will need to install dependencies defined in package.json via:

```
npm install
```

Next, we’ll need to install Parcel using this command:

```
npm install parcel
```

You should now see Parcel listed under the dependencies section in your package.json file like below:

```
"parcel": "^2.0.0-rc.0"
```

Note that the package name is parcel, not parcel-bundle which is the name of the deprecated Parcel v1 package. Make sure that you install the up-to-date parcel package and refer to Parcel’s v2 documentation.

## The Serve and Build Commands

Let’s add our start and build commands in the scripts section of package.json. The start command starts up Parcel’s built-in dev server and the build command bundles your app for production.

```
{
  "scripts": {
    "start": "parcel src/index.html",
    "build": "parcel build src/index.html --public-url ./"
  }
}
```

In the code block above, the start command bundles and runs our app at the entry point src/index.html, with the bundled assets served from ./dist. Likewise, the build command runs with the same entry point at src/index.html.

If your website files are hosted somewhere other than the root folder (/), the build command will require an additional --public-url flag to specify that file path. In the example above, ./ specifies that the site will be served from the working directory, in our case, the ./dist folder, which Parcel automatically generates when you run the build command.

Remember that you can run the build and start commands with npm run X, where X is our custom script.

A convenient feature of Parcel’s built-in dev server is hot reloading. When you run npm run start, you will see the following message:

Server running at http://localhost:1234
Try navigating to http://localhost:1234 on your browser and making a small change to your app (like the font size of a heading). You’ll see that Parcel automatically re-bundles and updates your app in the browser without the need for a page refresh!

However, if you’re following along with the provided React app, running either command will produce the following error in the terminal:

Error: No transformers found for src/sun.svg.
This error is caused by the way the .svg files were imported. We’ll resolve this in the following section!

## Transformers
Parcel supports out-of-the-box transformers for many kinds of files without the need for additional configuration. These include CSS, TypeScript, JSX, and images.

## Images
Parcel allows you to directly import a variety of image file types to your code using import but they must be converted into URLs, by prepending 'url:' before the file paths.

In our example React app, we need to edit the import statement for sun.svg in Carousel.js to use the url: prefix like below:

```
import sun from 'url:./sun.svg';
```

You will also need to prepend 'url:' to our image paths in app.js.

If you’re still running your app on the dev server via npm run start, you should be able to see your app automatically update to display the images in your browser.

## CSS
When CSS files are imported directly in JavaScript with the import statement, Parcel will automatically gather all referenced CSS files and bundle them into a single CSS file at the exit point.

We import Carousel.css in Carousel.js like below:

```
import './Carousel.css';
```

Parcel doesn’t need any additional transformer configurations in order to bundle the Carousel.css file.

## Putting It All Together
Now that we’ve set up package.json and imported our assets, running the build command should generate a ./dist folder that holds the bundled assets of our project.

Remember that you can preview the bundled app on the dev server by running:

```
npm run start
```
Try using Parcel to build your next web project!
