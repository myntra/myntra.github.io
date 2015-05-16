---
layout: post
title: Personal thoughts on the shutdown of the myntra.com website
---

*[Note: My name's Sunil Pai. I work as a UI architect in myntra. I wrote this as an internal post to myntra engineering, and they're nice enough to let me share it with you. I've only edited some gramar and semantics. Giant disclaimer that I had no say in the company's decision to go app-only, but read on for my opinion on it.]*

I'd like to share some memories and thoughts on the desktop website, if only for posterity's sake.

Early 2013, I was goofing around Bangalore trying to get my own startup off the ground. It was to be a tiny analytics tool for developers called 'kolo', that would hopefully make me enough money for food, cigarettes, and the occasional movie. As you can imagine, that didn't go anywhere. By May, I'd lost most social skills, my facial hair made me look outright dangerous around children, and I was so. friggin'. bored. I used to hang on the weekends with a buddy who'd just started working at myntra, and he'd tell me about some of the problems facing the tech team. I told myself it'd be fun to maybe work on myntra's problems for a while, until I knew what to do with kolo. I had an initial conversation with Shamik (holy shit, this guy got Lytro to market?), did the interview rounds, and got to work in June.

By this time, myntra had already decided to move to node.js. ([I did a talk on the tech details of the move](https://www.youtube.com/watch?v=49M0-VPvFjE)) Folks were already building dedicated (micro) services corresponding to the site's features, so the only real job was to build the damn frontend. We did multiple projects at once. I remember while Gopi Raghu et al were doing the home/landing pages, I took on the search/product details page with Kunal Anand Sam et al, and we got cracking.

Those days were glorious. We were pumping out code so fast that we managed to fit in hundreds of extra goodies, and didn't miss a single deadline. While originally to be just the 'browser' front end, we ended up writing the whole stack, all the way from servers and service clients and builds, to a highly tuned isomorphic stack for the browser app itself. The header rewrite happened in a weekend, and I lost count of the number of arguments with the designers. We set out to be the fastest ecommerce site in the country, and did that with room to spare. 6 months, thousands of lines of code, and unending conversations on how to do it 'right'. Indeed, fixing this layer meant that the services finally got the load that they were built for, and exposed all the innards to true scale.

For perspective - we had 10+ php machines that would go down whenever we did a sale. We were struggling to do upwards of a crore a day during those times. When the node stack launched, we could run all of myntra's traffic through ONE server. (theorized and tested by Rana, what a good day that was)

So we've grown like mad since then. The code we wrote in those days forms a big chunk of our networking layer now, and we're easily India's biggest node.js shop. We've written api gateways and mobile apis and microsites and whatnot. node's the default front facing solution for webpages and apis (though there's some movement around go/clojure that we should keep an eye on), and it's fairly easy for newer engineers to jump into. All that code written on dark cold nights is still working, and constantly being fixed/tuned/replaced. The modular nature of node means we could move away from it in parts or completely whenever we choose, and overall it's had a positive effect on the business. node does us well in these mobile times too, and that knowledge is turning out to be invaluable in writing actual mobile apps (more on that in a bit).

But for a while this last month, I've been feeling quite... sad. Purely sentimental, only because I've never really lasted long enough at a job to see my work being taken down. That project gave me personal validation, and made me learn so much. 2 years I've lasted at myntra! (I even tried quitting, but was thankfully talked off that ledge) I've received the occasional tweet abusing me about the site shutdown, telling me how much they loved the website ux, leaving me quite nonplussed and unsure how to respond. I've been uncertain about my own role in this company, and whether this paradigm shift would obsolete me.

I showed up for the 14th midnight shutdown event at office... not sure why. I suppose I had to show up for the funeral. Oddest feeling ever, doing this. Prasad was really sweet and called me up to push Anurodh's finger to shut down the site, and we broke out the booze. After 2 glasses of champagne, and a day of thinking it through, I think I have a much better perspective on what this shutdown means to me.

For one, I'm not done as a web developer. I've barely started.

Desktop websites were always a hack, you understand, becoming a much bigger platform than was originally thought of. Javascript, the language I adore and make a living off, was busted out in 10 days. HTML and CSS are a hodgepodge of 'good to have' features accumulated over 20 years, and we evolved a set of so-called 'best practices' to get around the pain of developing in an environment quite hostile to a user interface developer's needs. (Who here can tell me why a doctype is important?) And when the mobile revolution started (circa 2007, post iphone), shoving that browser into a tiny screen has made the problem WORSE, not better. 'Web standards' evangelists will tell you that this is ideal, the idea of incremental updates, but despite the big corporates pumping millions into making a better browser, there's been very little innovation, other than better perf, and exposing sensors to the web environment. What worked for the web was ubiquity, and humanity coming together to produce/consume content, and build the infra required for it.

Read my lips: HTML/CSS/JS != Internet.

The real innovation in the mobile world has come from seamlessly connecting devices and services and people in real time with tiny electronic devices that everybody carries with them. And the scale of these devices is many multiples of what desktop will ever be. If you take that, and piggyback on the ubiquity of the Internet, magical things happen. Traditional Ecommerce is just the tip of a very, very big iceberg.

Read my lips: Mobile browsers != Mobile internet.

While the word 'apps' makes it sound like these are desktop style apps, with tiny closed domains as whole worlds onto themselves, the mobile scene is a little different. It's getting incredibly easy to talk between apps and services, and smaller screens means better, focused UX (at least from companies that give a shit :P) And I'd talk your ears off about how streaming apis/observables + IOT will literally change the world. Very exciting. By having access to a platform that's so... 'connected' with human beings, I repeat, magical things happen. Understand - THIS is how we reinvent the web for the mobile world. And this is how we will delight our customers. What happens over the next 2 (3?) years of combined effort across the world will define what the mobile internet is. And while we're at it...

Read my lips: Always bet on JS

This is Brendan Eich's repeated mantra at conferences, and while I've always thought it should say 'Always bet on Lisp', JS has this one killer advantage over the others. What? Accessibility. By pulling off a complete "English" move, it's adopted features from a number of languages, while keeping the core easy to implement on a vm, and is easy(ish) to learn. I feel thus that JS shares the accessibility of the internet. So the pattern is now established and works - create a very high performance VM/environment (blink, gecko, webkit, libuv(?), jvm, dalvik, ios, tessel, etc etc), implement a JS engine on it (v8, javascriptcore, spidermonkey, nashorn, whatever), and go to town. Many times has the death of javascript been predicted (GWT, Flash, silverlight, native apps(!), etc etc), but not only has it overcome those challenges, but come up with incredibly competent (and still accessible!) responses (insert 5 minutes of React Native gushing) And you combine an accessible programming language with mobile devices and the internet, and guess what? Magical things happen.

But also, for this revolution, I actually get to *participate*. The desktop revolution happened when I was a child, but this time I'm in the thick of it. Heck, my employer just threw down the gauntlet to the world, with a bold stride towards this future. And my work experience as an async programming / user interface developer means I have the skills required to write programs for this world. On a kickass platform, on my own terms! This feels so empowering, I can't stop smiling.

Secondly, I get to do this with people that I genuinely *like*.

Ecommerce fundamentally isn't easy, because your users trust you with their money and personal details. This is an incredible privilege that we must never EVER abuse, and means we must always be sympathetic to their problems, even if they happen to be shouting at you loudly when it happens. What this also means, is that the team that runs this business have to operate with the utmost diligence and standards. Remember, site-stays-up is, and always will be, the engineering team's first priority. When our site goes down, India gets MAD.

In the process of being in such a team, you get close to each other. You see the ugly sides, the personal quirks. You wind up at their weddings, and drunk late at night in the middle of bangalore arguing about unit tests and PRDs. You have little to hide, because being 'on the go' all the time means these people truly become your *friends*. Some days are great, when we do launches and hit targets, and some days are bad, when we don't.

The only reason we got through such a giant tech stack rewrite, was because *everybody* bought in, and did everything in their power to make it work. There are few teams in the world who can pull off this kind of multi-month effort, and I'll always be proud of the way myntra behaved during the transition. Our culture let us achieve many big things, while the actual tech was just an implementation detail :) What I think that means, is that culture will be a key factor again during this mobile phase. It'll be challenging considering all the new faces, but I have faith we'll do it right.

So yeah, exciting times; for me, and for myntra. Many things will change - the way we write code, the way we deploy to these devices, the way we test our services (imagine being DDOSed by every mobile device on the planet), what 'design' means (do designers still use illustrator to mock tiny dynamic screens?), so called "web standards"... all of it. We already have a number of internal experiments progressing well, and I can't wait to see how our customers react.

To wind this up, I'd like to make one last mention of the website. It struck me that no other website ends on a high, and most of them close because of failure. For that reason, myntra.com was the Sachin Tendulkar of websites. Sure, in his last few days, he got outshone by his younger teammates. But he also got a standing ovation when he left the field, if only for paving the way for the future.

Thank you for reading.

π

