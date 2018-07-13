# How I Built My First [Electron App] & You Can Too Pt.1 - Problem, Idea & Tech Stack

Have you ever though about building your own electron app? Maybe you have an idea you want to realize. Or, maybe you have a problem nobody else is solving. Or, you are just curious and want to learn how to build an electron app. Maybe all of these reasons. This is exactly what we are going to do, build our own electron app from scratch. In this part, we will start with the problem we want to solve. Then, we will outline the idea for our app. Then, we will decide what tech stack will we use. So, without further ado, let's begin our journey into the World of electron.

<!--
Table of Contents:
## The problem
### Grease the groove method
### Back to the problem
## The idea and solution
### The must-have features
### The nice-to-have features
## Tech stack
## Closing thoughts on building an electron app
How I Built My First [Electron App] & You Can Too [part 3].
-->
How I Built My First [Electron App] & You Can Too [part 2].

## The problem

Every product, and service as well (well, theoretically, service is a product), should start with a problem. Although, it could be fun to build something for the sake of building it, or for the sake of learning, it is not optimal. The work itself is often more pleasure when the thing we want to build has also some utility. And, by that I mean something more than being just an educational prop. In the case of things that have some utility, it is more likely that there is someone else, in the World, who may want to use what we build.

This was reason why I decided to create this tutorial on creating an electron app and base it on solving a real problem, even though a small one. So, what is the problem we are going to solve? Have you ever heard about "grease the groove" method? As some of you may already know, I am a huge fan of fitness and training, especially [calisthenics]. One problem I deal with at this moment is the lack of strength. There are exercises that are just not an option for me. And, this is where "grease the groove" method enters the scene.

### Grease the groove method

I first heard about this method from a Soviet Special Forces instructor and popularizer of kettlebell training [Pavel Tsatsouline] on [Tim Ferriss Show]. Put simply, "grease the groove" method is about increasing one's strength through practice. The theory behind this method is that strength is a skill. And, like any other skill, if we want to improve it, we have to practice it and train it. This way, we create and strengthen the connection between our nervous system and our muscle fibers. This also strengthens [myelin sheet] around the axons of nerve cells involved in the practice.

The stronger is the connection between our nervous system and muscle fibers, and the myelin sheet, the faster our muscles can contract. Faster muscle contractions means that the move or exercise we practice becomes more natural and easier. As a result, we develop neuromuscular motor pattern. Why is it good to work on these neuromuscular motor patterns?  Neuromuscular motor patterns allows us to use more force. The way it does this is by utilizing a greater amount of muscle fibers. And, the more efficient these patterns the greater the amount of muscle fibers we can use, leading to more force.

The equation is simple. Faster muscle contraction + more muscle fibers contracting = more force (getting stronger). To summarize it, practicing a specific movement helps us get stronger in particular movement by developing a more efficient neuromuscular motor patterns. Do it often and you get better at it. And, this is what "grease the groove" method is all about. We take a specific movement, or two, and practice it multiple times a day. With time, as we develop more efficient neuromuscular motor patterns we get stronger. That's it.

One caveat. Before you try this at home, there is one important thing to keep in mind. It is necessary to AVOID going to failure. Grease the groove method is about practicing the movement in the best form we can. It is not about killing ourselves. Usually, this means practicing at somewhere around 40-50% of what we are capable of doing. Let's say we want to get increase our strength and make progress in push-ups. In that case, we will take the maximum number of reps (repetitions) we can do and then do only 40%, or at 40% difficulty level.

Finally, we will repeat these 40% multiple times a day. A more specific example. Let's say we can do 15 push-ups at max in a single set. Our grease the groove program will then be doing just 6 push-ups in a perfect form in a single set. And we will do this set a couple of times a day with enough time between these sets. This can be every 45, 60 or 90 minutes. We can choose whatever time frame we want, we just have to be fresh and fully rested and recovered from the last set. Remember, it is a practice, not a workout in a gym.

At the end of the day, by practice greasing the groove we can manage to do a high amount of perfect push-ups. Imagine how many perfect push-ups it will be in a week, or month. This quantity and quality will slowly make us stronger. The next time we will test our max, it will not be 15 push-ups, but maybe 20 or even more. I know that this may sound insane. Doing some exercise or movement multiple times a day? However, it does work. If you want to know more, there is a great long article about this method on [The Art of Manliness blog].

### Back to the problem

Okay, back to the problem and the reason to build the electron app. The problem is a lack of strength. One potential solution is grease the groove method we just discussed. However, this introduces a number of small issues. First, we need to track the number of sets we have to do in a day and how many we already did. Second, we want to measure the rest period without constantly watching the clock. Third, we may want to keep track of our progress in the long term. Fourth, we may need a help with setting the right amount of reps.

Some of these issues are easy to solve. We can use document editor or pen and paper and write down how many sets we want to do as well as how many we already did. We can then store these notes somewhere so we can review them later. Next, we can use stopwatch to measure the break and let it notify us when it is time to do another set. Finally, we can use head or calculator to find the right amount of reps we should do in a single set, remembering that it should be somewhere between 40 and 50% of our maximum.

The problem with this solution, and the reason why I don't like it, is that it is too complex. It includes too many tools. There has to be another way, one that is much easier. A way that would make this whole process almost automatic. What if there was just one tool, one simple app that would take care about all this, nothing more? Well, if there is nothing that fits our need, why can't we build it ourselves? Why can't we build a simple electron app that would help us practice grease the groove? Challenge accepted!

## The idea and solution

So, this is what we are going to do in this mini series. We are going to build a simple electron app that will run on desktop computers. It should be compatible with major platforms, Windows, Mac, and Linux. We can talk about building a mobile app using the same stack later. This app will have just one goal and do just one thing. It will help us practice grease the groove method for whatever exercise or movement we want. Now, let's talk about features, those that are the must-have as well as those that are the nice-to-have.

### The must-have features

First, the must-have features. As we discussed, we need to track the number of sets to do every day as well as how many we already accomplished. Next, our app should include some simple stopwatch to measure the rest period between the sets. These are basically the must-have features. Well, there is one more. We should be able to minimize the app to system tray. Our app should be visible only when necessary or when we want. Otherwise, we should not even know it is running. No additional window on the screen. So, system tray is a must-have.

### The nice-to-have features

Now, let's talk about the nice-to-have features. It would be nice if our app could keep track of our progress. We may want to know how are we doing in the long term. And, we may also want to know how long are we practicing specific exercise or movement. This can help us understand whether we make any progress and how fast this progress is. It will also make it easier to log the exercises and movements we already practiced in the past. Next, the app could help us with setting the right amount of reps, or at least give us some rough estimate.

This feature would be useful for two reasons. First, no counting necessary on our side. Sure, it is a very simple math, but it is still something we can make automate. Second, we need to make sure that knowing the theory behind grease the groove method should not be necessary. The app should be useful even for someone knows nothing about this method and wants to try our app simply because she wants to get stronger. So, having a calculator with one, or a number of, presets would solve this issue.

There is one more feature we may want to consider, notifications. Let's assume that our electron app will include a stopwatch. That will be handy. However, we will still have to open the app from time to time to check whether it is time for another set. This is not ideal. We have a ton of other things to do during the day. And, since the app will run on the background, it will be easy to forget about our grease the groove practice. This puts notifications somewhere between a must-have and nice-to-have. App will work without them, but they can improve overall experience.

So, let's do a quick recap. Tracking the number of sets (to do and already done), simple stopwatch and system tray. These are the must-have features. Something to track our progress, some simple reps (and sets) calculator with presets and desktop notifications, maybe with some sound. Sounds like we have a very good idea about what we want to build, at least for our [MVP]. Now, it is time to think about the tech stack for our electron app.

## Tech stack

The underlying framework for our app will be [electron]. There is clear. This also means that we will work with HTML, CSS and JavaScript. These technologies will also make this mini series easier to follow for all of us who are coming from the World of web development and web design. In the end, these technologies are the tools of our trade and our daily bread, so to speak. Now, also quickly discuss what libraries can we use to develop our electron app. Sure, we can stick to basics. However, we can also practice working with some popular libraries.

The first and most important library we will use in this project will be [React]. It will help us build our electron app using modular approach and components. It also makes working with JavaScript and DOM manipulation easier, and faster. With React, we can use `state` for features such as the stopwatch and sets counter. Finally, it is also personal. I like React and this can be an opportunity to learn more about it. In case of the `state` management may also consider [MobX] especially because of observables and observers. For now, we will stick to React `state`.

When it comes to CSS and styling, I first wanted to use PostCSS. However, I think that we should use [styled-components] instead. This library for styling works great with React, is easy to use and can handle everything we will need for our electron app. The last thing to consider is what bundler will we use. For now, let's try out [Parcel bundler]. I know that this is a wild card that can backfire, but it looks quite well. And, in the worst case, we can always switch to good old Webpack. And, maybe we will. That's it for additional libraries. Well, almost.

We need something to build our electron app. This leaves us with three options. The first one is [electron-builder]. The second is [electron-packager]. The third option is [electron-forge]. At this moment, I am still deciding between electron-builder and electron-packager. As with the bundler, I am not sure which one to choose. The only condition both these packages meet is the ability to create a portable app, no installation needed. Let's keep this open until the next part where we will start with development phase.

## Closing thoughts on building an electron app

This is all I have for you for this introductory part of this mini series. I hope you are not disappointed because this part was focused on pure theory and planning and we didn't write a line of code today. The upside is that we have a clear idea about what we want to build and what features should our electron app have. This will help us work on what is really important and, as a result, develop our electron app faster. Thank you for your time today and get ready because, in the next part, we will get our hands dirty and dive into code.

One more thing. If you have any recommendation, thoughts, advice or tip for bundler or builder/packager or any other library that could be useful, please share it in a comment or ping me on [Twitter]. Or, you can write a [mail] if you want. This is my first project on building electron app and there is a lot to learn. I will be very grateful for any advice or help.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[part 2]: https://blog.alexdevero.com/electron-app-pt2/
[calisthenics]: https://blog.alexdevero.com/calisthenics-why-it-is-the-best-hobby-ever/
[Pavel Tsatsouline]: https://www.strongfirst.com/
[Tim Ferriss Show]: https://tim.blog/2015/01/15/pavel-tsatsouline/
[myelin sheet]: https://en.wikipedia.org/wiki/Myelin
[The Art of Manliness blog]: https://www.artofmanliness.com/2016/01/20/get-stronger-by-greasing-the-groove/
[MVP]: http://ask.leanstack.com/lean-startup-fundamentals/what-is-a-minimum-viable-product-mvp
[electron]: https://electronjs.org/
[React]: https://reactjs.org/
[MobX]: https://mobx.js.org/
[styled-components]: https://www.styled-components.com/
[Parcel]: https://parceljs.org/
[electron-builder]: https://github.com/electron-userland/electron-builder
[electron-packager]: https://github.com/electron-userland/electron-packager
[electron-forge]: https://github.com/electron-userland/electron-forge
[Twiter]: https://twitter.com/AlexDevero
[mail]: https://alexdevero.com/contact.html

<!-- ### Inspiration
-
 -->
