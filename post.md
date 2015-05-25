You’re a busy person. Security is not a very visible feature in most applications, and so sometimes it’s not a priority. Of course you know it’s important, but how can you fit it into your busy schedule?

The answer may be in the power of habits, especially [mini habits](http://minihabits.com/). These are good for busy people or those who want to make a (big) improvement, but get distracted or feel demotivated after a few days. In a minute I’ll show you what this has to do with security.

![Image](https://media.licdn.com/mpr/mpr/AAEAAQAAAAAAAAN4AAAAJGExMGM2ZThiLWQ4ZDQtNGQ2MS1iYjU2LWU1OTQ0OTUwOTMwMQ.png)

The key to mini habits is that you **minimize your daily goals to an absolute minimum, to something small that requires only willpower to complete, not necessarily motivation**. As we all know, starting is the hardest. But once the ball is rolling it’s easy. Even if you only achieve your small goal, you’re one step further. You can do more, of course, but your goal is already reached. As described in the [Mini Habits book](http://minihabits.com/), although it’s easy to use willpower, we only have a limited amount of it. Motivation tries to push us out of our comfort zone, while **willpower just takes a few steps out** and then falls back into our comfort zone.

Creating habits should be part of your workday routine. Once the actions you want to turn into a habit are transformed into something that you do automatically, you will feel that the tasks are much easier.

**“So, what does this have to do with security?”** you ask. Here’s the strategy: **Set a few minutes aside** every day for security. **Use reminders** to remember your daily goal. Use a pen and paper or software, the tools don’t matter really. The **consistency **and effort to achieve every day is what matters. To keep the ball rolling, think about the next day today so that you can start right away tomorrow. If you know it will be a very busy day, find an easy task to do first.

If you’re **in a team**, other people can be responsible for parts of this. But it’s best if you use a system to track responsibilities, otherwise your good intentions will fall through the cracks on busy days.

### The Week

So here’s an outline for a week with mini habits that form a Rails security strategy. (Well, actually it’ll also work similarly for other programming languages.)

### Monday

Well, it’s Monday, so start your week with something easy! For example, some manual work: Check your software and components. Your software should be up to date. Chances are you already have a standardized process to update your server or it’s managed by the provider. But what about the Ruby gems? Get on the mailing lists if they have one, subscribe to their blog feed or just keep links to their **changelog** and check for updates today in these places.  
Take a look at the gem [bundler-audit](https://github.com/rubysec/bundler-audit) to automate this process. It will check your gems for known vulnerabilities and also recommend some improvements regarding the update process in general. However, the database is a community effort and does not include all the gems you might use, so you should also keep some manual checks.

You probably know **these two mailing lists** already, but do subscribe to these to stay on top of security updates: [Rails security updates](https://groups.google.com/forum/#!forum/rubyonrails-security), [Ruby security announcements](https://groups.google.com/forum/#!forum/ruby-security-ann) including updates for some important gems.

Also, the [National Vulnerability Database](http://nvd.nist.gov/download.cfm#RSS) provides an RSS feed about recent vulnerabilities in all kinds of software and libraries. Subscribe to it to hear about updates for your web server, database software or other software in your ecosystem. It only shows the vulnerabilities of the last eight days, so that’s why you should do this every week.

![Tuesday](https://media.licdn.com/mpr/mpr/shrinknp_200_200/AAEAAQAAAAAAAAJxAAAAJDBiZTQ3YTQzLTliZmQtNDkxOC1iYjJjLThkNmZmMGMyYWU0NA.png)

### Tuesday

Well, you’re still busy with keeping up, so let’s do something manual again. Chances are your web application uses **TLS/SSL** and you probably heard a lot about the recent vulnerabilities in that area. So head over to [https://www.ssllabs.com/ssltest](https://www.ssllabs.com/ssltest) and **perform a free test of your TLS/SSL web server configuration** today. This is also a good day to check the expiry date of the SSL certificate because it expires without warning. This could also be the day to start learning something new about this whole complex area. For example, every Tuesday you could read two pages of the book “[Bulletproof SSL and TLS](https://www.feistyduck.com/books/bulletproof-ssl-and-tls/)”. It’s a complete guide to using SSL/TLS and OpenSSL. It also covers weaknesses at every level and the latest attacks, such as BEAST, Heartbleed et al. Or start with the free short guide “[SSL/TLS Deployment Best Practices](https://www.feistyduck.com/books/bulletproof-ssl-and-tls/)” in the Preview section on the book’s website.

![Image](https://media.licdn.com/mpr/mpr/AAEAAQAAAAAAAAONAAAAJGU2MTkxOTU0LTZmMWYtNGJhMS1iYTk3LTkzNGUyYTVhMmI5Zg.png)

### Wednesday: The bigger picture

Great, we’ve hit the middle of the week and the todo items from the weekend are done, so let’s review something now! Give some thought to the changes or the new features from the past week. What are the security implications? Let’s say somebody added a feature to change a user’s email address. That sounds like a normal feature. And it’s secure by itself, because only the user can change her own email address. But today it’s about the **big picture** and you’re thinking: What if somebody somehow gained access to an account? That means she could simply take over the entire account by just changing the email address. And from there she could use the “Forgotten password” feature to create a new password which will be sent to the new email address. So you can effectively change the password without knowing the old password, that’s the inconsistency here.

It’s easy to overlook these problems in a busy daily schedule. So what will you do if you have a security strategy here? Ask for the user’s password to change the email address or verify the change with a confirmation email to the former address.

So today, you go through the changes and ask:

- What if this new field had a special value from somewhere else in the app (an ID from somebody else), or was empty or nil?
- What will happen to this feature if you copy and paste cookies, tokens, links, IDs from elsewhere?
- If something bad happened, would this feature make it even worse? As in the example from above. Or if someone gained access to an admin account, would all client data be gone then?
- What would happen if the user first clicked this new link and then clicked another unexpected link somewhere else in the app?

If this is the first time you do this reflection, look at the critical areas first: Cookies, sessions, authentication, authorization, user accounts, API, and configuration. **And limit the time you spend on this.** Otherwise you won’t want to do it next week, because it took too long last time.

![Image](https://media.licdn.com/mpr/mpr/AAEAAQAAAAAAAANZAAAAJDVjY2EzZDdjLTU5ZWYtNDQxOS04MTk1LTA1YzdiNTNiOWIwZg.png)

### Thursday

This is another day for reflection because the weekend is still miles away. How about thinking about the **“what if”** today? What if somebody is trying to brute-force the app, will you notice or be able do something against it? What if someone managed to inject Cross-Site Scripting (XSS) code into the whole application? What if you suddenly have to revoke 300 compromised API keys? Many things can go wrong in a public web application. I think it’s important to be ready for the unexpected. With a security strategy, you’re ready for at least some incidents because you’ve prepared little command line tools and checklists. You can quickly revoke access of some users. You see who is affected by a security breach. You can see what happened. You can quickly develop, test, and deploy a fix. You have a way to notify affected users and ask them to change their password. You have a manual **step-by-step script ready to react quickly and not forget important steps**. That’s what will set you apart from other applications.

![Image](https://media.licdn.com/mpr/mpr/AAEAAQAAAAAAAANrAAAAJGU1MWUwZjQxLTE2MzktNDEyNC04ZjQwLWM0MDE0MWNhZmU1Nw.png)
### Friday
Well, it’s Friday (hurrah!), so, let’s do something automatic. Today you can run static code security analysis tools like [brakeman](http://brakemanscanner.org/). Or you can verify that all code follows a style guide, for example with [Rubocop](https://github.com/bbatsov/rubocop). Start with a weekly run because it might be quite some work to do all the fixes that these tools recommend. Only then you could run them more often, or even on a continuous integration (CI) server.

Also, keep a SECURITY.md file in your repository and note when it was last run, who’s responsible for it and what the result was.

Some of it might sound like boring assembly-line work, but **the boring things ensure steady quality and security**. Ask franchise businesses. Don’t spend too much time every day if you’re usually busy, otherwise it will be like a New Year’s Resolution: The first week of January we’re motivated… but then we go back to our old habits. So instead of doing too much in the first week, move some tasks to the next week.

### Bonus

And here’s another habit that is “on-demand”. If you’re the only developer in the “team”: Check your code again before you commit. I use [gitk](http://git-scm.com/docs/gitk) (I’m sure there are better tools) to read through all the changes before each commit and think about the implications for security (and quality) again. It’s amazing how much you can spot by yourself with a little reflection before handing changes in. Over time you’ll develop a way of thinking when doing this. You’ll ask yourself what would happen if this variable was empty, nil, or something unexpected.

And if you’re in a team, reviewing the changes of your colleagues is an effective way to ensure quality and security. **Some teams also use pull-request cycles with great success.**

![Image](https://media.licdn.com/mpr/mpr/AAEAAQAAAAAAAAKyAAAAJDY3MzZkMGE4LTM4NTktNDkyNS1hM2FmLWUyYWQ1YTJiODQ4Zg.png)  
One more thing, you like learning, right? Maybe you want to keep a list of topics or Rails methods to look up one day (how about today?). Let’s say that in your code review you come across the sanitize method and think, “How secure is it really?”. And indeed, there’s a huge difference between [the newest version](http://api.rubyonrails.org/classes/ActionView/Helpers/SanitizeHelper.html) and the [older implementation](http://apidock.com/rails/v4.1.8/ActionView/Helpers/SanitizeHelper/sanitize) that “does it’s best”.

Right, there’s the week.

**Tl;dr:** In summary, it’s a set of mini habits for every workday to achieve a little progress in all the different aspects of security. Of course you can swap the days and do a different habit on Monday. Or you can add your own procedure to it.

PS: If you’d like, I’ve prepared a **5-page guide** for each day for you to follow. Click the link in the pinned tweet in my Twitter profile to get it.