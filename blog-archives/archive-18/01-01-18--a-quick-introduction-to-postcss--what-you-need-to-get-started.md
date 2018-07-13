# A Quick Introduction to [PostCSS] - What You Need to Get Started

As web designers and developers, we spend a lot of time working with CSS. For many, this is a time full of pain. There are many tools that aim to make working with CSS easier, faster, more flexible and fun. PostCSS is one of those tools. You may already heard about it. Maybe you even thought about trying it out. Unfortunately, you didn't know where to start. Good news. In this article, you will learn what you need to know about PostCSS in order to start using it today. Let's begin!

<!--
Table of Contents:
## A quick introduction to PostCSS
### Why PostCSS?
## How to use PostCSS
### Npm Scripts
### Gulp
### Grunt
### Webpack
### Parcel
## Closing thoughts on getting started with PostCSS
-->

## A quick introduction to PostCSS

Okay, where to start? Let's start with a little bit of theory. What is actually PostCSS? As I mentioned in the beginning, PostCSS is a tool that makes work with CSS easier, more flexible and faster. Some people are even not afraid to say that PostCSS is a way to reinvent CSS. I don't know whether this is true. There are other tools such as Sass, LESS and Stylus that are also doing great job reinventing CSS and the way we work with it. However, there is something that makes PostCSS different, that almost puts it in its own category.

Well, there is one thing we should make clear sooner rather than later. PostCSS is not a "real" preprocessor, whatever does it possibly mean. PostCSS is rather a CSS parser, framework or API that allows us to use plugins which can do various tasks. By itself, without any plugins, it actually does nothing, it doesn't transform CSS in any way. We can install it parse a CSS through it and the result will be the same as the raw CSS we used. Sure, we can say this about preprocessors as well. We can take raw CSS, use Sass or LESS, and the result will be again the same.

One difference is that both, Sass and LESS, already contain all the features such as mixins, extends, loops, conditions and so on. PostCSS does not. In order to change the raw CSS we have to add at least one plugin. Metaphorically speaking, we can think about PostCSS as a manager. It manages plugins and provides them with data (CSS converted into an abstract syntax tree (AST)). It is these plugins that do all the heavy lifting. Manager needs people. People get the job done. Without these people, manager is basically useless. PostCSS is a manager.

### Why PostCSS?

So, why trying PostCSS is a good idea? No, it is not due to the number of stars on [GitHub]. Although, PostCSS seems to be a winner in this race of fame as well. No, there is something else. What is this thing? Why so many people like to use PostCSS? Well, different people will probably give us different answers. However, there are at least three main strengths people often like to mention. First, there is the extendability. PostCSS is an ecosystem rich in custom [plugins and tools]. Every webdesigner and developer can pick and use any plugin she wants.

When you want to make some part of your work with CSS easier, there is a chance that you are not alone who thought about it. With a bit of luck, there is a PostCSS plugin you can install and use. And, if not? Well, you can some small handy plugin by yourself and release it. Then, other people in the community can use it and maybe also improve it. This is something other preprocessors don't offer. With other preprocessors, we are usually limited by what is available in the "standard package" and use only that.

The second strength of PostCSS, and reason why many developer prefer it over other options, is its modularity. What do I mean? Other preprocessors are full of a lot of useful stuff. However, we may never really use some of these features. The problem is that we can't just take them and throw them into the trash can, to minimize the code. Just as we can't add new features we would like to use, we can't strip away some of those features we don't want to use. Again, we are limited by what is available in the "standard package".

PostCSS is different. As I already mentioned, PostCSS is basically an ecosystem of plugins. So, when we want to use some feature, we find the plugin that provides this feature and install it. The same is true in case if we don't want to use certain feature. All we need to do is to remove the plugin. That's all. We can add or remove features, or plugins, (and write new) the whole day as we wish, if we want. The third and last strength of PostCSS is it respects W3C standards. We can use it as a polyfill and use the latest W3C features.

This is possible thanks to the constantly growing ecosystem of plugins created by the community. This is what many of these plugins aim to do. Their goal is to allow us use the latest CSS features without worrying that our project will not work right after we release it into the World.

There is one more thing that will be useful for people used to working with other preprocessor. PostCSS works with the same principles as other preprocessors such as Sass, LESS and Stylus. Meaning, we can use features that are not available in the CSS. For example, we can use mixins, extends, loops, conditions, better version of imports, "non-native" variables and so on. The result is always clean and "browser-friendly" CSS. In the end, we can customize our PostCSS workflow that it feels like using one of the other preprocessors.

## How to use PostCSS

By now, we have at least some idea about what PostCSS is and what are some of its strengths. The next question is, how to use it? What do we have to do to experience the taste of working with PostCSS? The answer is, as usually, it depends. It depends on what task runner or bundler are we using in our workflow. Whether your task runner or bundler of choice is Gulp, Webpack, Parcel, Grunt (really?) or you like to use hard-core npm scripts, there is a solution for it. And, if you don't use any, maybe this article may help you decide. Let's take a look at all of them.

### Npm Scripts

Let's start with simplest way to use PostCSS. And, that is through command line. This will not require installing any task runner or bundler. All we need is npm and node.js. If you don't have these, download node.js installer for your specific computer and operating system from the [official website] and install it. This will also install npm on your computer. Then, we can install PostCSS. Since we want to use PostCSS directly via command line, we will need to install `postcss-cli`. Keep in mind that it has to be installed globally.

```
npm install -g postcss-cli
```

From now on, we can use PostCSS from our command line any time we want. For example, let's say we want to take our `style.css` file inside `src/css` directory parse it through PostCSS and save the result as a new file (`styles.css`) inside `dist/css`. Since, we didn't install and use any plugins, the output CSS will be the same as the input. The simplest way to use it is by using following command.

```
// template: postcss [some-options] --output output-file input-file

postcss --output src/css/styles.css dist/css/styles.css
```

Let's say that we want to use some plugins, such as cssnext for prefixing and cssnano for minifaction. This means we will need to install `postcss-cssnext` and `cssnano`. I suggest that you install these packages as local dependencies for every project, with `npm install --save-dev postcss-cssnext cssnano`. However, if you want to install them globally, feel free to do so. Also, if you prefer using yarn over npm to install dependencies, feel free to use yarn `yarn add -D postcss-cssnext cssnano`.

Now we can use the following command. This will take our CSS file `styles.css` autoprefix it with `cssnext` and then minify it with `cssnano`.

```
postcss --use postcss-cssnext --use cssnano --output src/css/styles.css dist/css/styles.css
```

We can also use shorter versions of those flags and write. You can find all flags, commands and information about `postcss-cli` in its [GitHub repository].

```
postcss --use postcss-cssnext -u cssnano -o src/css/styles.css dist/css/styles.css
```

### Gulp

Next, let's talk about my favorite task runner, Gulp. If you used this Gulp before, you know that its configuration is very easy and fast. And, if you don't have any experience with this task runner, but you are curious, let me give you two resources you can later explore. First one is the [official web], and docs. This will give you sufficient amount of information to learn about what Gulp is and how it works. Then, take a look at [Gulp for Web Designers] tutorial on my blog. So you can learn how to use it and start using it straight away. Now to the configuration.

Let's create a minimum and functional Gulp config. We will again use `cssnano` and `postcss-next` plugins. We will also need to add `gulp-postcss` plugin. This plugin will help us pipe CSS through the plugins we want to use. So, `npm install --save-dev gulp-postcss postcss-cssnext cssnano`. Before moving to the next step, please make sure you already have Gulp installed on your machine. If not, run `npm install -g gulp` first. Then, in your `gulpfile.js` add following lines.

```
const gulp = require('gulp');
const postcss = require('gulp-postcss')
const cssnano = require('cssnano')
const cssnext = require('postcss-cssnext')

// A simple 'css' task to transform CSS
gulp.task('css', function() {
  return gulp.src('src/css/styles.css')
    // Pipe the styles in through PostCSS and use specific plugins.
    .pipe(postcss([
      cssnano(),
      cssNext()
    ]))
    // Save the output CSS to the 'dist' folder.
    .pipe(gulp.dest('dist'))
})
```

Now, we need to use `gulp css` command to make the magic happen.

### Grunt

Next one is [Grunt]. I have to admit that I used this task runner only once. And, it was only because Grunt was already used on the project I was working on and I didn't want to rewrite the setup of the project. However, Grunt is still used by a large group of people, even though it popularity is on the decline. Anyway, in order to use PostCSS with Grunt, we will need to install `grunt-postcss`. And, the plugins we want to use. As in the case with Gulp, make sure you have Grunt on your machine. If not, run `npm install -g grunt`. Then, add following code to your `Gruntfile.js`.

```
module.exports = function(grunt) {
  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    styles: {
      options: {
        processors: [
          require('cssnano')(),
          require('postcss-cssnext')
        ]
      },
      dist: {
        src: ['src/css/styles.css'],
        dest: 'dist/css/styles.css'
      }
    }
  })

  // Load post-css.
  grunt.loadNpmTasks('grunt-postcss')
        // Register default task.
  grunt.registerTask('default', ['styles'])
}
```

As the final step, in order to run the task, we need to use `grunt` command.

### Webpack

The third one is module bundler [Webpack]. To say that Webpack is popular would be an understatement. It is a go-to tool and favorite choice for many developers, especially those working on bigger projects. So, let's take a quick look at how to use PostCSS with Webpack. And, let's again use `postcss-cssnext` and `cssnano`. Aside to these plugins, we will also need to install `webpack`, `css-loader`, `file-loader` (it is a dependency), `postcss` and `postcss-loader`. If you have Webpack dependency installed globally on your machine, you may skip it during the installation.

```
npm install --save-dev webpack css-loader file-loader postcss postcss-loader cssnano postcss-cssnext
```

Now, we can create a short snippet of code for PostCSS and put it inside our `webpack.config.js` file.

```
const webpack = require('webpack')
const path = require('path')
const ExtractTextPlugin = require('extract-text-webpack-plugin')

module.exports = {
  context: path.resolve(__dirname, 'src'),
  entry: {
    app: './app.js';
  },
  module: {
    loaders: [
      {
        test: /\.css$/,
        use: ExtractTextPlugin.extract({
          use: [
            {
              loader: 'css-loader',
              options: { importLoaders: 1 },
            },
            'postcss-loader',
          ],
        }),
      },
    ],
  },
  output: {
    path: path.resolve(__dirname, 'dist/styles'),
  },
  plugins: [
    new ExtractTextPlugin('[name].bundle.css'),
  ],
  // The rest of your Webpack config
}
```

It is a good and common practice to have configuration for PostCSS, and other tools that support it, in a separate file. So, let's create another file, called `postcss.config.js`, for just for PostCSS and put what we need for PostCSS there. Since we want to use only cssnano and postcss-next, our code will be very short.

```
module.exports = {
  plugins: {
    'cssnano': {},
    'postcss-cssnext': {}
  }
}
```

If you have Webpack installed globally, you can use `webpack` command (with other options you want to use). Otherwise, create an npm script, called "webpack" for example, and then use `npm run webpack`.

### Parcel

The last tool, also a module bundler like Webpack, is Parcel. This bundler is quite new and I didn't have the chance to try it on my own properly. However, it looks very promising as it doesn't require any configuration and offers similar functionality as Webpack. In order to use PostCSS with Parcel, we need to do only thing, aside to installing Parcel and our plugins `npm intall --save-dev parcel-bundler postcss-cssnext cssnano`. We need to create config for PostCSS and use it to store our configuration for PostCSS.

This config file can be either `.postcssrc`, `.postcssrc.js` or `postcss.config.js`. Any option will work. The only difference will be in syntax. Let's pick the `.postcssrc` and create a simple configuration in JSON. Now, we can fire it up by choosing an entry file and using command such as `parcel index.html` to build our project, for example.

```
{
  "plugins": {
    "cssnano": {}
    "postcss-cssnext": {}
  }
}
```

## Closing thoughts on getting started with PostCSS

This is it! You just finished your journey through the world of CSS and PostCSS. I hope you enjoyed this article and learned something. I also hope that, by now, you have enough information to start using PostCSS right away. One question you may be asking now is, what now? Well, there is no official syntax for PostCSS you would have to learn and memorize. So, my answer will be very simple and straightforward. Take a look at the plugins available for PostCSS, pick those you like and use them in your first PostCSS project.

Remember, that the best and fastest way to learn anything is by doing it. It is also much more fun. So, don't wait think about it. Go ahead and just start. Give yourself some interesting challenge and see how will you handle it. And, if your still unsure, check out this extensive tutorial on [Smashing magazine]. You can also visit the [PostCSS website]. So, go and have some fun!

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[GitHub]: https://github.com/postcss/postcss
[Sass]: http://sass-lang.com/
[LESS]: http://lesscss.org/
[Stylus]: http://stylus-lang.com/
[plugins and tools]: https://www.postcss.parts/
[official website]: https://gulpjs.com/
[official web]: https://nodejs.org/
[GitHub repository]: https://github.com/postcss/postcss-cli
[Gulp for Web Designers]: https://blog.alexdevero.com/gulp-web-designers-want-know/
[Grunt]: https://gruntjs.com/
[Webpack]: https://webpack.github.io/
[Parcel]: https://parceljs.org/
[Smashing magazine]: https://www.smashingmagazine.com/2015/12/introduction-to-postcss/
[PostCSS website]: http://postcss.org/

<!-- ### Inspiration
-
 -->
