# Lauren Tan on GrokBot teams, constraints, and CI

- Source: https://x.com/0xCodila/status/2092331579527803215
- Author: codila (@0xCodila)
- Posted: 2026-08-25 19:21 UTC
- Duration: 57:06
- Sibling: [summary](2026-08-25-lauren-tan-grokbot-workshop.summary.md)

## Tweet

SpaceXAI engineer (ex-Cursor):

"I barely look at code anymore - agents absorb the pain of constraints and CI

Grokbot build a team of individual agents and orchestrate them like people"

In a 1-hour workshop, Lauren Tan showed how she builds GrokBot teams and how agents changed the way she codes.

## Transcript

Whisper `small` / int8, English. First ~6 minutes are leftover React/compiler Q&A; Lauren starts around 06:25. ASR often hears GrokBot as Grocbot / Rockbot / Glockbot.

[00:00-00:06] Personally, I think that the best use of AI is really like a pair, like someone you're
[00:06-00:12] pair programming with, and not someone that's not a tool to just replace the act of writing
[00:12-00:18] code or worse, outsourcing your thinking. And I think there's a tendency like, you
[00:18-00:22] know, because AI is so exciting, you want to put AI everywhere and be seen as someone
[00:22-00:30] who's very, you know, what do you call it, like on the ball I guess with AI, that you feel
[00:30-00:35] this pressure of like, you know, I'm just going to, I got to increase my productivity, I got
[00:35-00:39] to ship like 100 PRs this week and barely understand what I'm doing and, you know,
[00:39-00:49] vibe code my way to a million ARR or whatever. But I think, you know, one of the things
[00:50-00:55] that I've personally seen is that although when I use AI, I save some time, you know,
[00:55-01:00] writing the code, I actually find myself spending more time reviewing what the AI did and
[01:00-01:05] like correcting it. So, you know, like I've tried the thing that a lot of people say,
[01:05-01:10] like, you know, you, instead of prompting an AI to just build the future outright,
[01:10-01:15] you sort of get it to build a spec for you first, then you review that spec, and
[01:15-01:20] then you do that whole thing. Then it's like, it's such a time consuming process. And if
[01:20-01:26] you don't really understand what the AI is doing, then I think you're doing yourself a
[01:26-01:32] disservice because it's like the same way that in school you use a calculator or, you
[01:35-01:40] know, you have an open book exam. The skill of being a developer is really in like the
[01:40-01:46] knowledge of using tools. And I think when you just completely outsource that, you know,
[01:46-01:51] thinking, I think that's like really dangerous. But I think, I don't know, I don't know what
[01:51-01:58] other people will say to that. But yeah, that's my personal thought. Because I wrote the PR.
[02:00-02:07] But also it's like, also the same feature that I don't like the most. Should I save the
[02:07-02:12] answer for a later question? Let's hear it. Well, so use effect event is like a new API.
[02:14-02:19] We, it's a little bit tough because we don't want people to abuse it. And I think if you
[02:22-02:26] start thinking about like, you know, where can I start throwing use effect event across
[02:26-02:31] my code base? I think the question you might want to ask first is, do I actually even
[02:31-02:36] need an effect here? And then, you know, read the docs on, you might not need an effect. And
[02:40-02:47] only in the very rarest of circumstances where you do need an effect, the docs also do a
[02:47-02:52] really good job of describing the use cases where you might need a use effect event. And
[02:52-02:57] so like the canonical example is where you have, for example, an effect that connects
[02:57-03:03] to some web socket, like a chat room, and you might want to trigger some sort of event whenever
[03:04-03:10] the user like connects to a chat room, like show a notification. And so use effect event
[03:10-03:15] will sort of let you issue that event from the effect without you having to define or
[03:17-03:22] declare that dependency in the dependency array. So yeah, it's kind of an advanced API. So
[03:23-03:29] don't use it too much. It's the take then. Use effect event is actually one of my favorite
[03:33-03:37] features of React 19 as well, because I can imagine a lot of code getting cleaned up. And
[03:37-03:41] you're right, like use effect gets abused a lot. So I'm worried use effect event would
[03:41-03:47] also get abused a lot. But I'm hoping that people will stop doing that ESLint exception to
[03:48-03:53] avoid the dependencies. Yeah, exactly. Definitely use the linter as well, because the new version
[03:53-03:59] of the linter will tell you, will give you the appropriate warnings if you're using use
[03:59-04:03] effect event incorrectly. So definitely make sure to, if you do have to use use effect
[04:03-04:09] event, use the linter. Yeah, and to add to that, I think we talk about this in a doc as
[04:10-04:15] well, but you absolutely shouldn't feel pressure to go and like remove all your manual
[04:18-04:24] memorization, because the compiler can just optimize your components anyway, even if you've
[04:25-04:30] already used manual memorization. So yeah, there's definitely no rush to, you know,
[04:30-04:37] delete all of them. And are there plans to deprecate use memo and use callback
[04:37-04:44] in the future in favor of Rear compiler? No, I don't think so. Maybe Joe, you want to add
[04:47-04:54] more to that? Yeah, so. One thing we've definitely heard a lot is the fact that, you know, the
[04:54-05:00] compiler is still a Babel plugin. And we know a lot of the community has moved on to
[05:00-05:07] like Rust based tooling, like SWC. So that's definitely like one of the recurring
[05:07-05:13] questions we get is like, when is, you know, compiler, the compiler going to work like
[05:13-05:20] natively in my SWC build pipeline. And for that, I think that the team we've talked about
[05:20-05:25] it a lot. I think our current plan is to, so there's this project at Meta that's
[05:25-05:31] called static Hermes. And it's a project to use Hermes, which is our own JavaScript
[05:32-05:39] engine, to pre-compile JavaScript into native code. And so the idea being that we can, you
[05:41-05:47] know, keep the very flexible development process we have in the compiler, which is written
[05:47-05:54] in TypeScript, compile and get the benefits of a natively built binary. But that's still
[05:54-06:00] a bit, like maybe I'm not sure, like, how far out that is. But it's something on
[06:00-06:04] our radar and something we want to explore. But if that doesn't pan out, then we'll have
[06:04-06:11] to think a lot about maybe another attempt at porting the compiler to Rust and then that
[06:13-06:18] can work with SWC. But yeah, definitely, though, it's like a question that comes up
[06:18-06:25] a lot. Yeah. I suspect there'll be a lot of interesting answers from this, from
[06:25-06:32] this chairs here. Hello, everyone. I am Lauren Tan, I guess not many people know my last
[06:32-06:42] name. I am Potato on Twitter, Potato with spelled with an E. And I have been at cursor for
[06:42-06:49] about five months. Previously, I was at Meta where I worked on the React team, specifically
[06:49-06:53] working on the React compiler, which was a whole lot of fun. I'm still on the core
[06:53-06:59] team and contributing to open source here and there. So that's really nice that they
[06:59-07:06] still let me do that. And before Meta, I was at Netflix where I was both a tech lead and
[07:06-07:13] I transitioned to be an engineering manager for about two years. So I've had a lot
[07:14-07:20] of experience going between engineering management and being an individual contributor. And
[07:20-07:24] I think something I've noticed, actually, which is quite interesting is that there are so
[07:24-07:30] many parallels with management skills and how to manage agents. And that's actually a big
[07:30-07:35] part about what I wanted to chat with you and everybody else about today. And yeah, I've
[07:35-07:42] gotten to a point where I really don't look at the code anymore. And I say that not
[07:42-07:47] just to sell you tokens, but because it took a lot of work to get to that point.
[07:47-07:51] I spent a lot of tokens to get the code base to this point where I no longer have to look
[07:51-07:57] at it. But I'm very excited because of the potential where it's not just, this doesn't
[07:57-08:04] just benefit me. It benefits everyone contributing to GrockBot. And it also empowers designers
[08:04-08:10] and product managers and even GTM people to add features to GrockBot. And I don't
[08:10-08:13] have to worry, I don't have to wake up at night in the middle of the night and
[08:13-08:16] worry that, oh shit, someone's just merged to perf regression. I think like
[08:16-08:22] greenfield applications, especially the brand new applications are the biggest risk, in my
[08:22-08:29] opinion, and also the greatest opportunity. Because if you vibe code a project, a prototype,
[08:29-08:34] like we did for GrockBot, GrockBot was spun up very, very quickly. And if you haven't
[08:34-08:39] heard of GrockBot, it's like a new application we just launched yesterday. It's really
[08:39-08:45] cool. Let's you orchestrate your great individual agents that have their own identity and
[08:45-08:49] you can kind of orchestrate them. It's super cool. Definitely check it out. But yeah,
[08:49-08:54] it was a very greenfield application, like most prototypes are. So it's like vibe
[08:54-09:00] coded very quickly. Humans were not reading the code at all. And I had this tweet
[09:00-09:07] recently where I said something about organic architecture. Maybe I'll find it.
[09:08-09:14] But the idea is that when you have a completely vibe coded application, you
[09:14-09:20] essentially have no guardrails whatsoever. So your agents, when you give them a task,
[09:20-09:25] they will just solve it in whatever method is the most convenient. And over time, you
[09:25-09:29] get into this situation where you have a code base that is spiraling out of
[09:29-09:34] control, because you don't understand it. Your agents understand it, I guess, in
[09:34-09:38] a way, but like they've built something that is, you know, optimized for
[09:38-09:44] for shortcuts. And, you know, it will you will suffer, you have a lot of issues with
[09:44-09:50] that application. So I think starting your code base with like very strong
[09:50-09:57] constraints is very much needed. Because like when you have a code base that you
[09:57-10:02] can trust, right, when you have guardrails that actually help you help your
[10:02-10:06] agents, right, good code, you can get into the, you know, like into this part
[10:06-10:10] of the curve where I where I said, you know, I woke up today and I had like 20
[10:10-10:17] PRs merged by my agents. And that's because I invested a lot of time over
[10:17-10:23] 600 PRs. I calculated yesterday when I refactored all of GROCBOT to this new
[10:23-10:29] architecture that I've been building. Right, I have a ton of constraints and
[10:29-10:33] CI is like, it's actually very annoying to write code in GROCBOT by like agents
[10:33-10:38] absorb all of that annoyance. But yeah, I'm happy to talk about what exactly
[10:38-10:45] that is. Yeah, I think one question before we get into this part here is just
[10:45-10:49] around that element of like what your your CI looks like or maybe some of the
[10:49-10:51] constraints and then also like the average PR size. I saw a question about
[10:51-10:55] that earlier. Just to get people, you know, kind of a glance. It doesn't
[10:55-10:58] have to be like mathematically average, but just, you know, like what
[10:58-11:02] generally the size of the PR is, if it's only a couple lines of code or,
[11:02-11:03] you know, yeah.
[11:06-11:12] I think it depends. I'm trying to do this in a way where I'm not going to like.
[11:12-11:13] Yeah, you don't have to share the actual number of views.
[11:13-11:15] Like an actual average just.
[11:15-11:16] This is fine.
[11:16-11:16] That's fine.
[11:16-11:22] But like we have, so okay, this is not that interesting, but well, fun fact is
[11:22-11:28] that virtualization in GROCBOT and in cursor is actually powered by
[11:28-11:33] pretext, which is a sort of new library that someone's built.
[11:34-11:35] That's really interesting.
[11:35-11:36] You should you should check it out.
[11:36-11:38] But it's not really that important.
[11:38-11:41] I think the average PR size, I actually don't know.
[11:42-11:43] I don't know if I want to click on these.
[11:43-11:45] I probably can.
[11:45-11:48] But I would say like they can range anywhere from a few hundred lines
[11:48-11:52] or 50 lines to like a thousand, depending on what the thing is doing.
[11:53-11:55] So here I'm deleting a bunch of files.
[11:55-12:00] So I expect that it's just as like mostly deletion, but it kind of varies.
[12:01-12:04] There's no like, yeah, this is like hard cap or the middle.
[12:04-12:08] They're all like 50 line there's no hard cap, but I do encourage my agents
[12:08-12:10] to split up their work into multiple PRs.
[12:11-12:17] I do that mostly because I like I like the idea of I guess
[12:17-12:19] maybe this is much harder to do now as in the world of agents
[12:19-12:21] and you have like so many commits.
[12:21-12:23] But I like the idea that, you know, the get history is a very rich
[12:24-12:29] source of context and I like the I like each PR to sort of atomically
[12:29-12:34] describe what that small piece of thing is doing, which also makes it easier
[12:34-12:37] for me to revert changes and like figure out, you know, oh, I shipped a bug
[12:37-12:39] and it's this it's here.
[12:39-12:43] It's not in this 40,000 line PR where who knows what landed in there.
[12:45-12:48] But I don't have a hard cap on PR size.
[12:49-12:49] Cool.
[12:49-12:52] And then yeah, also quick question on like CI.
[12:52-12:54] So again, you don't have to go into like the screen share like your CI does.
[12:54-12:58] But just generally, what would you describe what the CI kind of looks
[12:58-12:59] like or how strict it is?
[13:01-13:01] Yeah.
[13:01-13:05] So well, specifically for Rockbot.
[13:05-13:09] So Dune is the is the sort of cheeky code code name for the architecture
[13:09-13:11] that we built for Rockbot.
[13:12-13:17] The CI looks pretty annoying because there's checks for everything.
[13:17-13:19] So like literally I have.
[13:20-13:23] Well, if you've written any reactor, example, you know, you know that one
[13:23-13:25] of the biggest foot guns in react is use effect.
[13:26-13:30] So in Dune and in Rockbot, we've banned use effect.
[13:31-13:34] So Dune is just the the mental model of what Dune is.
[13:35-13:39] You can kind of think of it as like next.js for electron apps
[13:39-13:43] and it's designed for agents to write and it's like custom for, you know,
[13:43-13:45] our agent powered applications.
[13:46-13:48] So the CI checks are very like specific to that.
[13:48-13:49] Like, you know, don't use this effect.
[13:49-13:53] It's it's it's bands like CI will fail and yell at you.
[13:54-13:57] We have like some of the more interesting ones that people might
[13:57-14:00] raise eyebrows is like I actually banned code comments as well,
[14:01-14:02] which is very interesting.
[14:02-14:07] But I've noticed that 99% of the time agents just write code
[14:07-14:10] comments that kind of describe some historical thing that is
[14:10-14:12] actually totally irrelevant to the code.
[14:14-14:15] Like it will often say like, you know, oh, Lauren said
[14:15-14:16] you should never do this.
[14:16-14:20] And it's now in the code comment like what like why what that was.
[14:20-14:23] I didn't say that as like a durable, you know, global rule.
[14:23-14:26] I just meant like your this PR sucks and you should change that part.
[14:28-14:31] Agents don't really understand us that well, surprisingly.
[14:32-14:35] And or they kind of assume too much and they kind of do things
[14:35-14:36] in like very stupid ways.
[14:36-14:38] So like, yeah, we just ban everything.
[14:39-14:42] Everything you can imagine like the agents are bad at we ban.
[14:43-14:48] So one example that we actually suffer a lot in the agents window is we have,
[14:48-14:51] you know, if you've used agents, you've definitely seen performance issues
[14:51-14:53] and you know, we're constantly trying to fix them.
[14:54-14:56] But it's like a.
[14:56-14:59] So never ending struggle because there's so many pull requests
[14:59-15:02] that get merged every any one of them could just regress
[15:02-15:04] performance or stability or reliability.
[15:05-15:07] You know, the agents window doesn't have this architecture yet.
[15:07-15:11] I plan to do bring this learning back there and kind of refactor
[15:11-15:15] everything there, but it just regresses super often
[15:16-15:20] because there's just one example is like we have very poor
[15:21-15:22] isolation between processes.
[15:22-15:26] So like, you know, on Electron, you have a renderer thread that renders your UI,
[15:26-15:29] but you also have like a main thread that you can run other code
[15:29-15:31] that doesn't need to block the renderer.
[15:33-15:35] But we do a poor job of separating those things.
[15:35-15:38] And so oftentimes you just accidentally have code
[15:38-15:40] that gets pulled into running on the renderer thread.
[15:41-15:44] And then all of a sudden you're competing with the renderer that,
[15:44-15:47] you know, that has a very if you want like 60 FPS,
[15:47-15:51] you have every frame that gets drawn has to be done in 16 milliseconds.
[15:51-15:54] So very, very small, you know, deadline per frame
[15:54-15:56] if you want, you know, a very smooth product.
[15:57-15:59] And when you start building, bringing in accidentally bringing in,
[16:00-16:03] you know, things that are like very computationally heavy
[16:03-16:07] or they have a lot of IO, then you just get into like a lot of jank
[16:07-16:09] and your FPS really drops.
[16:09-16:11] You start, you know, losing frames.
[16:11-16:14] You get long tasks that take more than 16 milliseconds
[16:14-16:16] and then you just get this really choppy experience.
[16:17-16:19] So all of those patterns that we've learned,
[16:19-16:22] basically building Electron apps, we've encoded into this framework
[16:22-16:24] and it becomes like a hard failure.
[16:24-16:27] So I literally in GROC about we literally have a directory
[16:27-16:30] called Electron main, Electron renderer.
[16:30-16:34] And we have import CI, I guess,
[16:34-16:37] where we actually check the dependency graph
[16:37-16:39] to make sure they're not accidentally importing code
[16:39-16:40] from one directory to another.
[16:41-16:46] So that's enforced by CI, as well as bug bots,
[16:46-16:51] which is our, which cursors like code review tool that runs on CI,
[16:52-16:53] you know, in our agents and be it's everywhere.
[16:53-16:58] Like, so I had this thing here where I talk about like,
[17:00-17:02] you know, like there are multiple layers, I think,
[17:02-17:03] for building a good code base.
[17:04-17:06] Obviously, the code base is one where
[17:06-17:10] if you have an architecture like this where it's extremely strict,
[17:10-17:13] you know, the way to build features is very conventional.
[17:14-17:17] That's like the strongest, strongest level of enforcement
[17:17-17:19] because agents just love to copy existing patterns.
[17:20-17:23] So one example of this in GROC is like, we have this,
[17:23-17:27] these concepts called like a feature and we have entry points
[17:27-17:29] and transcript cards, like, you know, the cards that you see in the chat.
[17:30-17:34] These are all like, like nouns, I guess, in the framework.
[17:34-17:37] And so there's a very conventional way of creating them.
[17:37-17:41] And so like a feature is all in a single directory, as an example.
[17:41-17:44] And so all of the code that contributes to that feature
[17:44-17:45] lives in one directory.
[17:45-17:48] So it's all co-located in one place, makes it super easy.
[17:48-17:50] You know, agents don't have to like grab around
[17:50-17:53] and try to figure out like where all the things are.
[17:53-17:55] It just looks at the feature and like, oh, OK,
[17:55-17:58] I'm working on the onboarding feature in GROCBOT.
[17:59-18:00] I'm just going to work in this directory.
[18:00-18:02] And for 80 percent of the work,
[18:02-18:04] it's mostly just very encapsulated there.
[18:05-18:09] But like, it's like, it's like designed again for, you know,
[18:09-18:12] like the dumbest agent, like you don't have to think, right?
[18:12-18:16] The one of the key principles I have for this framework is like,
[18:16-18:19] the shortest path is the best path.
[18:20-18:24] So because that plays exactly to how agents love to record,
[18:24-18:26] is that they like to take shortcuts, really, you know,
[18:26-18:29] to find the quickest way to solve the problem.
[18:29-18:32] So why not make that the best way to solve the problem?
[18:33-18:36] So I probably won't get into all the specific details.
[18:37-18:41] And this framework is really more of a collection of ideas
[18:41-18:43] and principles rather than something that will open source.
[18:44-18:46] You can screenshot this, I guess, if you want,
[18:46-18:52] and tell your agent to do something like this for you, too.
[18:54-18:56] Yeah, but it's really all about the layers.
[18:56-18:58] You know, like the code base is one part with features
[18:59-19:03] and directories and, you know, import or blocking import
[19:03-19:05] dependencies that shouldn't be imported.
[19:06-19:09] But and it all enforces that and static analysis.
[19:09-19:11] So like there are CI checks.
[19:11-19:14] We have a lot of links for bad patterns that we observe.
[19:15-19:17] Compiler diagnostics.
[19:17-19:21] There's also rules and bug bot, which are, I think,
[19:21-19:23] like three, four, five are more soft, right?
[19:23-19:27] These two actually make CI read, right?
[19:27-19:29] So that, you know, there's a hard constraint
[19:29-19:32] where the agent can just write crappy code
[19:33-19:35] for rules and skills and bug bot.
[19:36-19:38] Your agents can still forget, right?
[19:38-19:41] You can still or it may not always consistently apply them.
[19:42-19:47] So I like to layer them, but I don't I don't like to rely on them
[19:47-19:51] as the only source of enforcement because it's very, very soft, right?
[19:51-19:53] And if you if you only have rules and bug
[19:53-19:56] bot and skills and the style guide for code, you will.
[19:56-19:59] It's only a matter of time before your code base looks like complete trash.
[20:00-20:05] Sorry to say that, but I definitely recommend investing in things
[20:05-20:07] that can be hard enforced, right?
[20:07-20:11] And this is why, you know, maybe the choice of tech stack
[20:11-20:13] that you use is also very important.
[20:14-20:16] Like I think, for example, Rust is sort of making
[20:16-20:19] you know, is like getting super popular again
[20:19-20:22] because the compiler is so strict, right?
[20:22-20:24] The compiler enforces so many different things, you know,
[20:24-20:27] there's a borrow checker that you have to appease and as long
[20:27-20:30] as you make sure your agents don't write unsafe code blocks,
[20:30-20:33] you can more or less feel somewhat confident that if the code
[20:33-20:35] compiles, it probably works and it's good.
[20:36-20:39] But usually it gives you that level of trust and confidence
[20:40-20:45] that you as a human engineer no longer need to go and check it yourself.
[20:45-20:49] You know, you rely on code and static analysis
[20:49-20:53] to actually make that a lot smoother.
[20:54-20:58] And I guess the worst part, the worst place to be in is if you are stuck
[20:58-21:02] in code review land where you actually enforce all of the constraints,
[21:02-21:07] the invariance in your code base by literally the human person saying,
[21:07-21:09] you know, reading the code and like, OK, you should not do this, right?
[21:10-21:13] Every time you have to do that, you should consider that as a code
[21:13-21:17] like an anti-pattern and you should say, OK, instead of me commenting
[21:17-21:21] on the PR, how do I turn this into a hard rule, right?
[21:21-21:22] How do I turn this into a lint rule?
[21:22-21:25] How do I turn this into a CI failure?
[21:25-21:29] Or how do I even categorically eliminate this problem entirely?
[21:30-21:34] Cool. One question that had a couple of came up a couple of times
[21:34-21:36] was just around like token usage.
[21:36-21:40] So the question is like, is what you're describing a realistic thing
[21:40-21:44] for people who are on, you know, a normal set of token usage
[21:44-21:48] they don't have, you know, basically unlimited tokens to work with?
[21:49-21:50] I think that's a really good point.
[21:50-21:53] I mean, like, obviously, you know, I work at an AI lab
[21:53-21:54] where we have unlimited tokens.
[21:54-21:59] So I definitely cannot say that, you know,
[21:59-22:02] this is something everyone should do in the exact same way that I did it.
[22:03-22:06] I think it's possible to get to this point without, you know, breaking the bank.
[22:07-22:09] But, you know, if you are like an engineering leader
[22:09-22:11] or, you know, you have a startup that you lead,
[22:12-22:16] I think that may as a question of ROI and it's like,
[22:17-22:21] yes, you spend a lot of money on tokens in the upfront stage.
[22:22-22:24] You know, like refactoring your code base is going to take a lot of tokens.
[22:25-22:27] Adding all these things is going to take a bunch of tokens.
[22:28-22:31] But if we're heading to a world where agents are writing all the code
[22:32-22:35] and, you know, you want to be very lean, right?
[22:35-22:36] You don't want to have to hire.
[22:36-22:38] You don't want to be, you don't want to become like meta, right?
[22:38-22:41] Like, I mean, like in terms of you don't want to become
[22:41-22:45] a 10,000 person engineering org because, I mean, that's a cool problem to have.
[22:46-22:48] But also, you know, you have so much overhead.
[22:48-22:52] There's like planning, you know, like it's personally, I wouldn't.
[22:54-22:55] It is not super fun.
[22:55-22:58] But I think you want to stay very nimble, right?
[22:58-23:01] And you want to be like agents are all about allowing you
[23:01-23:03] to do things that you couldn't do before.
[23:03-23:05] That's really to me like the value of agents.
[23:06-23:08] You know, it's not just storing tokens on every single little thing.
[23:09-23:12] But to me, like the thing I couldn't do before is like
[23:12-23:17] enforce this level of constraints in a code base by myself, right?
[23:17-23:21] Like I'm just a single person, you know, it would have taken me years
[23:21-23:27] to build this framework and do all the refactoring and test everything
[23:27-23:30] myself and verify, you know, like run, imagine if it was just me, right?
[23:30-23:35] No, in pre-agent era, just like running, you know, it would take me so long.
[23:35-23:37] All right. And my salary is pretty high, right?
[23:37-23:41] Like so, you know, the question I think an engineering
[23:41-23:45] leader might have is just then, you know, like, what is there's a trade-off
[23:45-23:49] of do you hire someone to do this or do you spend the tokens to set up
[23:49-23:54] a code base so that even the most naive, right, the dumbest agents
[23:54-23:56] can do a good job.
[23:56-23:59] And when you actually get to this point, like even agents that are not,
[23:59-24:02] you know, fable size do an excellent job of writing code.
[24:03-24:07] And this pays a lot of dividends as well for me personally, where I have
[24:07-24:11] been powered, not just myself, but again, like, PMs, designers,
[24:12-24:15] engineers who are not familiar with Gropot to just contribute in a way
[24:15-24:17] that is sustainable.
[24:18-24:22] So, yeah, I think to kind of round it up, I think it's like
[24:22-24:27] it's it's there's a if you do your own analysis, I feel like it's pretty
[24:27-24:31] positive, it'll be pretty positive that the ROI you get from investing
[24:31-24:36] in stuff like this just empowers not just yourself, but your whole team
[24:36-24:38] to be so much more productive, right?
[24:38-24:41] Like, imagine if you have an army of engineers like me who are
[24:41-24:46] shipping so much improvements and bug fixes every day.
[24:46-24:49] One last question before we wrap up, this one is for the people in product
[24:49-24:50] on the call.
[24:50-24:54] So let's say we do have an army of engineers for shipping like Lauren.
[24:54-24:57] I'm just curious, like, how is the product team or other functions
[24:57-25:00] of your company keeping up, given that, like, if you're shipping
[25:00-25:03] so quickly, are they using AI more to do their jobs?
[25:03-25:05] Like, as much as you can speak to that, I always say, you know,
[25:06-25:08] like, you're not in that role, but just curious about how that works.
[25:09-25:12] I think this is where graph bot has been actually exceedingly powerful
[25:13-25:18] where so before graph bot, like, you know, obviously cursor only had cursor,
[25:18-25:21] like we only had agents window, we had a CLI, we had an IDE.
[25:22-25:25] And these are really like power user tools, right?
[25:25-25:28] They're designed for developers, so it's very, very developer centric.
[25:29-25:32] You can do knowledge work in them, but it's like the UI is not
[25:32-25:34] really optimized for that.
[25:34-25:38] So we actually didn't really have, well, I think like a lot of people
[25:38-25:41] in like, you know, GTM product, like they might have used cursor
[25:42-25:45] to do their work, but it definitely wasn't like a delightful experience
[25:45-25:48] with them. I think now with graph bot,
[25:49-25:52] it's become graph bot is basically like their cursor moment
[25:52-25:56] for people who are not in tech, in my opinion, like, it's like,
[25:56-26:00] it's like a very, very accessible way to use agents in a very comfortable,
[26:00-26:01] very familiar interface.
[26:01-26:05] It looks like iMessage, and it's very fun, too.
[26:05-26:07] You know, you can give your agent a fun name.
[26:08-26:12] You can have, you can kind of do orchestration in a very like natural way
[26:12-26:14] where you can sort of, you know, each agent is like a person,
[26:14-26:17] and now you're a team of agents like working on one agent per account
[26:17-26:20] that you manage, as an example, or if you're a PM, you have,
[26:20-26:22] you know, you can have an agent that summarizes all the work
[26:22-26:25] that Lauren did last night, and then now you know what I did, right?
[26:26-26:30] So I think our PMs are leveraging of that a lot, and they're shipping code, too.
[26:30-26:33] So, you know, oftentimes they will just say, oh, here's a bug.
[26:33-26:34] I fix it. Can you look at it?
[26:34-26:37] And then I'll go review it and actually it's just perfect.
[26:37-26:38] I'm like, OK, stamp.
[26:38-26:43] So I think that shows that, you know, the Dune architecture is holding up, right?
[26:43-26:48] The all the really strict constraints allow people who are not experts
[26:48-26:50] in engineering to contribute at a high level.
[26:51-26:54] So I feel like I've already seen that payoff a lot where, you know,
[26:54-26:59] designers and PMs are just able to to ship features directly.
[27:00-27:04] And that just makes the Glockbot team super fast, right,
[27:04-27:06] where we can ship so quickly.
[27:08-27:11] And we have a lot planned, so I'm very excited to, you know,
[27:12-27:16] to ship more agents to write code.
[27:16-27:18] And I'm sure a lot of you have had the same experience as well,
[27:18-27:20] is how do you trust it?
[27:20-27:24] You know, especially if you are an engineer that's been writing code
[27:24-27:28] for a very long time, you have a lot of opinions and lessons
[27:28-27:30] that you've learned about doing good engineering.
[27:31-27:34] And when you see agents just, you know, weaning it and, you know,
[27:34-27:38] guessing, hallucinating, you know, confidently stating that they found
[27:38-27:43] the smoking gun for the hundreds of time, but it's actually not the real problem.
[27:43-27:45] You lose a lot of trust.
[27:45-27:47] And when you lose, when you don't have much trust in your agents,
[27:48-27:51] I feel like you really can't get the most out of them.
[27:51-27:54] And for me, the parallels like with management.
[27:54-27:57] So if I'm an manager, an engineering manager of a team,
[27:58-28:02] and I have a bunch of, you know, I have a team of engineers on my team,
[28:03-28:06] and I don't trust them, then the mode of operation I'm going to be in
[28:06-28:08] is going to be like micro management, right?
[28:08-28:12] I'll have to spend a lot of time looking over my report's shoulders
[28:12-28:15] and checking that they're doing their work well, you know,
[28:15-28:18] that they're not shipping bugs to production.
[28:18-28:23] And so I drew this chart because it's not it's not a very scientific chart,
[28:23-28:28] but like this is how I imagine myself and my journey through using agents.
[28:29-28:34] So, you know, like fast forward or back forward or fast back,
[28:35-28:39] fast backwards, like a year or so when, you know, nobody was,
[28:39-28:41] or not many people were using agents to code.
[28:42-28:46] I think you, you know, get into this mode where you are
[28:47-28:52] in very heavily in the loop with one or several like a handful of agents.
[28:52-28:55] And you find yourself just constantly figure, you know,
[28:55-28:59] try to understand what your agents are doing and you're very, very in loop.
[28:59-29:01] You're watching every single output.
[29:01-29:06] You are sitting there prompting and you really can't parallelize beyond that
[29:06-29:09] because you don't, again, you don't have that trust, right?
[29:09-29:12] You can't go to a hundred agents, like spawn a hundred agents
[29:12-29:14] when you don't even trust the output of one agent.
[29:16-29:19] So over the past five months, I feel like I've really been able
[29:19-29:23] to like ascend this trust curve.
[29:23-29:28] And now I'm at the point where I actually have this sounds kind of scary to say this
[29:28-29:31] and it makes me sound like a sloth artist, but I promise I'm not.
[29:32-29:35] But I actually have my agents now auto merging PRs for me,
[29:36-29:38] which is like a wild thing to say.
[29:38-29:42] But like I woke up today and there were like 20 PRs landed
[29:42-29:46] and I just reviewed them on main like they were already landed and they were good.
[29:47-29:49] So how did I get to that point?
[29:49-29:51] It's basically why I wanted to talk about today.
[29:53-29:56] And again, like, yeah, feel free to jump in if you have questions, Colin.
[29:57-30:03] But oh, yeah, of course, I got to show this, this chart where.
[30:05-30:09] No, do not trust someone requested to control my computer.
[30:10-30:12] Probably won't do that.
[30:12-30:15] But yeah, so this chart, I think I'm sharing this chart
[30:15-30:19] not to kind of like flex, but to kind of show like the journey.
[30:19-30:23] Like so you can see like the curve, like it's sort of like inversely matches
[30:23-30:25] the contributions I've been able to land at cursor.
[30:26-30:29] So I joined five months ago and five months ago, like, you know,
[30:29-30:33] my first month, I was like, not very productive because I was, you know,
[30:33-30:35] I was learning the code base, didn't know what the heck was going on.
[30:36-30:39] And as I got more confident in my agents,
[30:40-30:43] I've really been able to kind of ramp up my productivity.
[30:43-30:47] And again, like, yeah, like last month, I shipped a thousand PRs,
[30:47-30:49] which is ridiculous.
[30:49-30:51] And then this month, we're only on the 12th.
[30:51-30:55] I'm already at like almost 800 PRs landed.
[30:56-30:58] So the velocity is definitely high.
[30:58-31:01] And you I'm sure a lot of you will definitely be questioning
[31:01-31:03] like how how much of this code is actually good.
[31:04-31:07] And I think, yeah, that's definitely fair to question.
[31:08-31:14] But yeah, I think, I think if you set up your agents well,
[31:14-31:17] you can definitely get to a very similar level.
[31:18-31:20] And so I'm going to talk about how we do that.
[31:23-31:27] So for me, I think I'm curious, like I guess calling your experience as well.
[31:27-31:32] But for me, I think the most important skill that you should have
[31:32-31:36] in your toolbox when you work with agents is verification.
[31:37-31:42] And by verification, I mean the ability for an agent to actually run the code
[31:43-31:50] or take CPU traces or heap snapshots or, you know, open an iOS simulator,
[31:50-31:54] whatever, you know, however your application is exposed to your users,
[31:54-31:58] it can do the same thing and run it for real
[31:58-32:00] and actually test and verify it don't work.
[32:01-32:03] Because that's the thing that really closes the loop.
[32:04-32:06] It doesn't guarantee your agent writes good code,
[32:07-32:10] but it allows them to at least write correct code,
[32:11-32:14] which is a big, a really big stop within cursor.
[32:16-32:20] Oops, where let me open this.
[32:29-32:31] There you go.
[32:31-32:34] So for the for cursors agent window.
[32:35-32:37] So this is actually an interesting story.
[32:37-32:40] But when I joined cursor five months ago,
[32:41-32:44] they're actually, well, I was supposed to join a different team
[32:44-32:46] I was supposed to join like the cloud agent team.
[32:47-32:50] But then since I have a lot of experience working on React
[32:50-32:52] and agents window is a react application,
[32:53-32:59] I was I was asked to basically help out with the agent window work.
[33:00-33:05] But there wasn't really a lot of like skills to help me.
[33:06-33:08] So I just found myself like, OK, agents
[33:08-33:09] we're going to launch in like a week, right?
[33:09-33:14] We have a really tight deadline and there was,
[33:14-33:16] you know, I was just sitting there, OK, I'm going to open up
[33:16-33:19] the performant, the Chrome Dev tools and just like take a trace,
[33:19-33:22] look at it myself and try to make sense of this flame graph.
[33:22-33:24] And keep in mind, I was just like in my first week.
[33:25-33:26] So I had no idea what I was looking at.
[33:26-33:28] No idea what, you know, I mean, I had some idea.
[33:28-33:31] But, you know, the code base was completely fresh to me.
[33:32-33:35] And I realized like my agent had no idea either, you know,
[33:35-33:37] like I would take a screenshot of the trial download tray.
[33:37-33:40] So I send it to it and it'd be like, yeah, it kind of looks like this,
[33:40-33:43] you know, and it would like confidently state like it's this thing.
[33:44-33:47] And then I try to fix that and turns out that's not the actual thing.
[33:48-33:50] So this was a very, very slow process.
[33:50-33:52] And if you've ever done any like performance work yourself
[33:52-33:55] or just even development with an agent
[33:55-33:59] where you don't have a verification skill, you are the verifier.
[33:59-34:00] You're the bottleneck.
[34:00-34:02] You tell your agent to do something
[34:02-34:04] and then it goes off and write some code.
[34:04-34:06] Then you open up your local dev build
[34:06-34:08] and then you start to say, oh, you know, it doesn't work.
[34:08-34:13] Then you got to copy paste screenshots or console errors or whatever.
[34:13-34:17] And then your agent like slowly kind of like, you know, works with that
[34:17-34:21] and then tries to understand it and fix the thing.
[34:22-34:25] But then you're constantly just in the loop and being a bottleneck.
[34:25-34:27] So there's really no way to parallelize.
[34:27-34:29] So the control glass skills, like one of the first skills I built
[34:30-34:34] for Cursure and Glass, by the way, is the code name for agents window
[34:34-34:38] that we use internally, but it's just Cursure, I guess.
[34:39-34:44] And so this skill is, I guess, the code itself is not super interesting.
[34:44-34:46] Your agent can very easily make one for you,
[34:47-34:50] where if you're building an electron app or a web app
[34:50-34:55] or even iOS applications, you can teach your agent
[34:55-34:57] how to use like the Chrome DevTools protocol
[34:57-35:01] or through Apple has some utilities as well
[35:01-35:03] for running the simulator and taking traces
[35:03-35:06] and programming the control as well.
[35:07-35:09] So that's really useful.
[35:10-35:15] But one thing I actually want to talk about is the this thing.
[35:17-35:18] Or just to read me.
[35:18-35:22] So this skill comes with this very unique feature called
[35:22-35:25] or not featured, a unique file called a feature map.
[35:26-35:29] And so the story then is like I built this skill.
[35:29-35:32] And so now the agent was able to actually run
[35:32-35:35] the agent window and take traces and whatnot.
[35:36-35:39] But it had no idea what what the agent's window was.
[35:39-35:42] So, you know, like someone say, like,
[35:42-35:46] oh, the left side bar is like laggy or something like that.
[35:46-35:49] Or, you know, the right side, the PR tab is not working.
[35:50-35:52] And the agent would just be like kind of flailing around.
[35:52-35:54] It would spend a lot of time trying to like look up the code.
[35:54-35:55] And, you know, where is this feature?
[35:55-35:57] How do I actually get to it on the UI,
[35:58-36:00] which made it basically completely useless?
[36:00-36:04] You know, like we would I would run the skill locally
[36:04-36:06] and, you know, it would spawn a dev build.
[36:07-36:10] But then it just be turning like I just try to click here.
[36:10-36:13] It wouldn't know how to get to things.
[36:13-36:15] And it was just an awful experience.
[36:15-36:18] So we was putting arrows on my screen.
[36:19-36:23] So, yeah, this this feature map has been really useful
[36:24-36:27] because it teaches the agent how to get to all of the features that you have.
[36:28-36:31] And in Pstack, the plugin that I've made,
[36:32-36:36] if you search for Pstack cursor on Google, you'll find it.
[36:37-36:40] But there is a create verification skill in that plugin
[36:40-36:42] where it actually helps you set up something like this for yourself,
[36:43-36:45] including the feature map.
[36:45-36:46] So it will actually explore the code
[36:46-36:48] and build up this initial feature map
[36:48-36:52] that tells your agent how to get to all of the different features that you have.
[36:52-36:54] And this is extremely powerful
[36:54-36:57] because now that you have these user reports that come in
[36:58-37:02] you can actually map even like a vague report or even a screenshot.
[37:02-37:05] So we have this internally at cursor
[37:05-37:09] where we have a Slack channel with lots of people
[37:09-37:12] giving us feedback on the agent's window and rock bottom and whatnot.
[37:13-37:17] And oftentimes the report is very bad, like very low quality.
[37:17-37:20] Like someone will just put very often we get like a screenshot
[37:20-37:22] and then someone just says question mark, question mark, question mark.
[37:22-37:24] Like, what is this?
[37:24-37:27] And, you know, without this, your agent's like, I have no clue.
[37:27-37:29] Right. But with a feature map like this,
[37:30-37:33] it has a lot more context and understanding
[37:33-37:36] of how to actually navigate how to get to all of the different features.
[37:37-37:39] So, like, you know, example, like, I guess, like the sidebar,
[37:39-37:41] like, what is the sidebar?
[37:41-37:44] You know, like all the different sub features that are present in it.
[37:46-37:47] Like from the user point of view,
[37:47-37:50] here's how to get to it, all the different keyboard shortcuts.
[37:52-37:55] Even like the what do you call it, the DOM elements
[37:55-37:58] or, yeah, like the attributes that you use for selecting things
[37:59-38:01] through the CDP are all there.
[38:02-38:07] So, again, yeah, this is like really, really powerful for agents.
[38:08-38:11] And piece that ships that create verification skill,
[38:11-38:15] but also a maintain verification skill, so you can keep this up to date.
[38:16-38:18] Cool. Yeah. I was just going to ask how you created that.
[38:18-38:20] So do you want to share a little bit more about
[38:20-38:22] that process in the context of P stack
[38:22-38:25] and maybe just what P stack is for the folks who aren't familiar?
[38:25-38:27] Yeah. So P stack is pretty interesting because,
[38:28-38:30] well, first of all, the name is kind of goofy.
[38:30-38:36] Like the P the P and P stack is like potato potato snack because I
[38:37-38:42] so there is a pretty famous person, Gary Ten,
[38:42-38:44] who is the CEO of Y Combinator,
[38:44-38:48] and he's come up with this plugin called G stack, Gary stack.
[38:48-38:51] And funnily enough, we share the last name.
[38:51-38:53] We have no relations,
[38:53-38:57] but I thought it'd be funny to kind of poke fun at Gary and make P stack,
[38:57-39:00] my version of his plugin,
[39:01-39:05] but kind of tailor it to my own set of engineering practices.
[39:06-39:09] But I honestly actually never set out to build P stack.
[39:09-39:11] It just started with a bunch of skills, right?
[39:11-39:13] Like I started with that control glass skill.
[39:13-39:16] And then I started with another skill like called how,
[39:16-39:20] which I also noticed through like observing agents.
[39:21-39:22] So like, you know, in the early days of me,
[39:22-39:23] you know, trying to climb this ladder,
[39:23-39:26] I was like super in the loop and I was basically
[39:26-39:28] nitpicking my agents to an extreme degree.
[39:28-39:30] I was like, I would tell it,
[39:32-39:33] you know, this feature has stopped working.
[39:33-39:34] Here's a bug report.
[39:34-39:36] Like, why isn't it working?
[39:37-39:41] And very often, the agent would just like of confidently state,
[39:41-39:42] like, oh, it has to be this, right?
[39:42-39:43] It has to be this thing.
[39:43-39:46] And I noticed like when I look at the actual tool calls,
[39:46-39:48] I noticed it wasn't actually reading the code.
[39:50-39:51] That I thought should be affected.
[39:52-39:53] And that made me just extremely suspicious.
[39:53-39:55] And at that point, I was like, I'm not going to,
[39:55-39:57] I can't trust any, this agent anymore,
[39:57-39:59] because it's just, it's just completely hallucinating.
[40:00-40:03] And I think, I think it's very easy to just,
[40:03-40:06] you know, like build up that distrust and not
[40:06-40:08] and kind of feel helpless.
[40:08-40:10] Like, you know, you don't know how to help your agents succeed.
[40:11-40:14] But like, again, I think the management analogy is super helpful
[40:14-40:17] because like imagine if you were a manager of an engineering team
[40:17-40:20] and you had an engineer in your team
[40:20-40:23] who was a really good coder, no business context whatsoever.
[40:23-40:24] You know, they just, you just hired them
[40:24-40:27] and they onboarded, you know, like five seconds ago.
[40:29-40:32] And so how do you actually teach that person to be effective?
[40:32-40:35] So how you do that is through a skill, a skill being just,
[40:35-40:37] you know, it's just marked down, right?
[40:37-40:40] But, you know, it encodes a lot of information, instructions.
[40:40-40:45] A lot of, you can really draw out a lot of intelligence
[40:45-40:48] from an agent by, well, some people on Twitter call it,
[40:48-40:51] like, you know, pull the agent to a different latent space,
[40:51-40:53] which is kind of like a fancy we have just seen.
[40:53-40:55] Like since, you know, LLMs are sort of like,
[40:55-40:59] they predict the next token, when you give it some high quality
[40:59-41:03] tokens to begin with, then, you know, it can kind of pattern
[41:03-41:06] match on like a higher space that's, you know, smarter.
[41:08-41:11] So that's like a very interesting model there.
[41:11-41:13] But yeah, I built PSAC very, very incrementally.
[41:14-41:18] So started with just really observing how agents, you know,
[41:18-41:21] all the different failure modes of that agents were having.
[41:21-41:24] And every time I saw that, I just, OK, I'm just going to make that a skill.
[41:24-41:26] All right, like stop hallucinating.
[41:26-41:28] Actually go and search up, look up the code.
[41:29-41:33] Use a lot of subagents and yeah, stop guessing.
[41:35-41:36] Watch people in the chat.
[41:36-41:38] So I guess it's two parts.
[41:38-41:40] So one is like, how do you maintain these skills?
[41:40-41:41] So like the product changes over time.
[41:41-41:43] Obviously there's a lot of people who are shitting against the code base.
[41:43-41:45] So how do these skills get maintained?
[41:46-41:48] And then second to that is like, how do you know when your verification
[41:48-41:53] is good enough like, and, you know, you can trust that the verification
[41:53-41:56] loops that you've built are going to, I guess you trust that the outputs
[41:56-41:57] when they're done.
[41:59-42:03] Yeah, maybe I'll talk about, I think there's some art really that
[42:03-42:04] I'll maybe I'll start with this one first.
[42:05-42:08] So like, how do I maintain these skills?
[42:09-42:14] So if you're not familiar with this concept and eval is essentially
[42:14-42:18] like a way to, the mental model I had is like, it's like a unit test
[42:18-42:23] for an agent and you can actually make your own evals.
[42:23-42:25] You don't need like a special framework for them.
[42:25-42:30] You can build one depending on like, you know, how scientific
[42:30-42:31] and how rigorous you want to be.
[42:32-42:33] My screen is red.
[42:34-42:35] Yeah, there's a little button.
[42:36-42:36] Sorry.
[42:37-42:39] Disabling the drawing or something.
[42:39-42:40] I can't see my screen.
[42:40-42:41] Yeah, sorry.
[42:41-42:42] If you guys could not draw on the screen, I agree.
[42:42-42:45] But there's a little button in the troll.
[42:46-42:47] Yeah, the little drop down.
[42:49-42:49] I clear.
[42:50-42:51] Yeah.
[42:51-42:51] Okay.
[42:51-42:52] Yeah, you got it.
[42:52-42:52] Perfect.
[42:53-42:55] Um, yeah.
[42:55-42:59] So evals are a way to unit test your skills basically.
[43:00-43:03] And actually in P stack, we ship under potato mode.
[43:03-43:04] There's a playbook.
[43:04-43:05] If you search for it called eval playbook.
[43:06-43:11] Um, and it's, uh, uh, it's like not, it's actually pretty, pretty
[43:11-43:12] rigorous the way it's done.
[43:13-43:17] But, um, essentially what I do is I spawn a lot of different sub agents.
[43:17-43:23] I have like my main coordinator agent, uh, come up with a rubric for, uh, what
[43:23-43:25] I want the skill to do.
[43:25-43:30] Um, and then it spawns all these sub agents and it, it creates individual
[43:30-43:35] directories for them, uh, which are cleverly named to not let the sub agent
[43:35-43:39] know that it's being evaluated because, uh, agents can actually tell.
[43:40-43:41] And when they do, they change their behavior.
[43:42-43:47] Uh, but it does a bunch of stuff like that to, um, essentially, yeah,
[43:47-43:51] like test whether or not the skill I'm making or changing is actually doing
[43:51-43:52] what I think it does.
[43:53-43:56] Um, and one of the really nice things about cursor is that we are, we
[43:56-43:58] support so many different models.
[43:58-44:02] So you can actually eval your skill across all sorts of different models.
[44:02-44:06] Um, and, you know, get a sense of how well it performs across
[44:06-44:10] that different matrix, um, especially for the models that you use.
[44:10-44:12] Uh, so I do this a lot.
[44:12-44:17] Every time I modify a skill, I will run one of these, uh, like the eval playbook,
[44:17-44:21] uh, and make sure that, you know, it's actually leading to a result I want.
[44:22-44:26] Uh, but I will say like maintaining skills is actually pretty hard.
[44:26-44:30] Uh, it requires, I think a lot of taste and observation.
[44:30-44:34] So you kind of need to be very good at being a backseat driver.
[44:34-44:35] You know what I mean?
[44:35-44:38] Like if you do pair, if you've ever done pair programming, for example,
[44:38-44:42] uh, and you watch a coworker code and you just like, you could probably
[44:42-44:42] do this better.
[44:42-44:44] You know, you could do it, you know, like, why did you not do this?
[44:44-44:44] Right?
[44:44-44:47] You, you ask a lot of questions to your coworker.
[44:47-44:48] And it's kind of a similar thing here.
[44:48-44:51] You like, you don't want to just be a passive observer agent.
[44:51-44:54] You want to be very in the driver seat in the initial stages when
[44:54-44:56] you're building up your own set of skills.
[44:57-44:59] Uh, you know, obviously you can use something like PSAC, but if
[44:59-45:02] you're building your own set of skills, it's very, I think, you
[45:02-45:06] know, opening up the, all the tool calls and like reading the code and
[45:06-45:11] reading all the agent behavior and their thinking blocks is a really
[45:11-45:14] great way to see where they, they fail, right?
[45:14-45:17] Like what, what, you know, where are they being done?
[45:17-45:18] And then you can go and build a skill for that.
[45:19-45:23] And then with verification, how you trust it is, it's, I think
[45:23-45:26] it's also a very similar iteration loop, uh, where, you know,
[45:26-45:29] like I actually did the same process for verifying the verification
[45:29-45:34] skill where I actually get, um, so one thing that's interesting
[45:34-45:37] about evals is that you can sort of hill climb them, meaning
[45:37-45:40] that, uh, your eval can produce a score, right?
[45:40-45:44] A score that you can get your coordinator to produce, uh, but
[45:44-45:49] also you can have a judge agent of a different model to, uh, kind
[45:49-45:53] of cross reference and make sure that the first model is not
[45:53-45:54] being biased, right?
[45:54-45:56] The model that's judging all of the sub agents that are running
[45:56-45:58] the thing, uh, but you can also like hill climb.
[45:59-46:02] So meaning that you can, you can use like slash loop in
[46:02-46:06] cursor and you can say, okay, keep looping on this eval, right?
[46:06-46:09] Until everything is 10 out of 10, as an example.
[46:09-46:11] Uh, and I did the same, the basically the same approach
[46:11-46:12] with the control skill.
[46:12-46:15] And so I kind of, it was very, it was very hands off actually.
[46:15-46:18] Uh, so, you know, I, uh, I kind of built, I built that
[46:18-46:21] skill that way, like the CLI in that skill.
[46:21-46:24] Um, and overtime is gone really good.
[46:25-46:27] Uh, but yeah, it was definitely not super smooth at the
[46:27-46:30] beginning and required a lot of iteration.
[46:30-46:35] And I think there's an analogy here for me, which is, um, while
[46:35-46:38] I make this analogy later in a different slide on my drawing
[46:38-46:42] here, uh, but I think of it like, uh, you know, as a, as a
[46:43-46:47] engineer now, you're sort of more like, uh, like meaning
[46:47-46:51] manager, or the analogy I like is like, you're like a chef in
[46:51-46:54] a restaurant, uh, you're the head chef, uh, you're not
[46:54-46:55] cooking all the food yourself anymore.
[46:55-46:57] You have a team of cooks, right?
[46:57-46:59] You have a line cooks, you have a sous chef, you
[46:59-47:00] have, you know, all these different stations.
[47:01-47:04] Um, and it's your job to really design the environment.
[47:04-47:06] You know, you, you're in charge of setting up the kitchen.
[47:06-47:10] You're in charge of, you know, like giving tasks to
[47:10-47:10] different people.
[47:11-47:16] So, um, yeah, it's a very interesting way of working.
[47:17-47:20] Uh, but yeah, that's, that's how I basically built, uh, these
[47:20-47:21] verification skills.
[47:21-47:21] Yeah.
[47:21-47:23] Just, just one ball there.
[47:23-47:25] I'm like, I had to go, try to go one layer deeper.
[47:25-47:29] So are you, let's say we wanted to build, um, uh, an
[47:29-47:31] eval or a skill for, for something.
[47:31-47:33] And we wanted to kind of get better on its own, which is, is
[47:33-47:35] what I think you're suggesting.
[47:35-47:38] Uh, are you doing that in like a work tree, kind of isolated
[47:38-47:41] with like the sub agents and then the reviewer agents and, and
[47:41-47:41] all that.
[47:41-47:44] Is it happening like in some type of cloud hosted environment?
[47:44-47:46] Like what's the more, the practical steps?
[47:46-47:48] If I wanted to go do this, uh, and like set up a
[47:48-47:50] verification system for something, what would I, what
[47:50-47:51] would I do or what would I start?
[47:53-47:56] Um, I think that, uh, the best place to start is
[47:56-47:58] local because you can observe.
[47:59-48:00] You can definitely observe what your agents are doing.
[48:00-48:03] So, uh, if you're building a verification skill for
[48:03-48:06] yourself, uh, I would definitely start local and just
[48:06-48:09] have your agent bring up the application, whether it's
[48:09-48:12] like a CLI or, uh, desktop app or whatever.
[48:12-48:13] And so you can actually observe, right?
[48:13-48:17] You can see how the agent is interacting with the, the
[48:17-48:20] application, you can see it, you know, how it calls
[48:20-48:23] like the different APIs that allow it to interact
[48:23-48:25] with the, uh, the application.
[48:26-48:31] Um, but, uh, for me personally, uh, I have basically
[48:31-48:33] been kind of all in mostly all in non-cloud agents
[48:33-48:35] because they're extremely powerful.
[48:35-48:38] Uh, and the really powerful thing about cursor is
[48:38-48:41] the, the cloud agents actually, where if you spend
[48:41-48:44] a little bit of time setting up the environment, these
[48:44-48:46] control skills, these verification skills pay
[48:46-48:49] a huge amount of dividend because it's not just
[48:49-48:52] something that makes you as a single engineer
[48:52-48:54] better, it actually levels up your whole team.
[48:54-48:57] Uh, and even your whole company, because, uh, you
[48:57-48:59] can actually start thinking about cloud agents, you
[48:59-49:02] can start thinking about automations that automatically
[49:02-49:06] do things like, uh, I'll, I get, I kind of talk
[49:06-49:09] about this a bit later, but I'll just kind of get
[49:09-49:11] into it, uh, where, where, you know, for example,
[49:11-49:13] like I talk a lot about this agent we have called
[49:13-49:16] Benny, right, who, who, uh, you know, takes all
[49:16-49:20] of the bug reports that we get and it automatically
[49:20-49:22] goes off in the cloud, opens up a cloud, uh,
[49:22-49:23] it's, you know, it's desktop.
[49:24-49:27] It runs cursor in its own computer and it uses
[49:27-49:30] the same control skills to interact with the
[49:30-49:32] application and try to reproduce the bug, uh, or
[49:32-49:35] the user report, right, and this is so, so powerful
[49:35-49:38] because at once I can immediately, I get so
[49:38-49:40] much information from this automatically.
[49:40-49:42] Like here in this example, you can see that, uh,
[49:42-49:45] the Benny actually reproduced the bug, uh, but
[49:45-49:47] it's already fixed on main.
[49:48-49:50] So it actually confirms that we fixed this
[49:50-49:52] problem already and all I need to do is just
[49:52-49:55] release another build of, of cursor, uh, so
[49:55-49:57] there's like huge information there that I
[49:57-49:59] didn't have to go off and sit with an agent,
[49:59-50:00] you know, and spend an hour trying to
[50:00-50:01] feel like, is this fixed, is this not fixed?
[50:02-50:05] So you, you, you gain back so much time, uh,
[50:05-50:07] but you know, everybody on my team benefits
[50:07-50:08] from this, everybody in the company
[50:08-50:12] benefits from this, uh, so definitely think
[50:12-50:14] that, uh, you know, keeping these, uh,
[50:14-50:17] using cloud agents is super powerful, uh,
[50:17-50:18] but yeah, it's like a journey.
[50:18-50:20] You have to trust it first, right,
[50:20-50:22] before you, you get to this point and that's,
[50:22-50:24] it goes back to what I was saying here where,
[50:24-50:27] you know, it's very hard, it's almost impossible
[50:27-50:28] and I would definitely encourage you not to
[50:28-50:31] try to jump from, you know, like,
[50:31-50:33] if you're still in this zone, you don't want
[50:33-50:35] to jump to like, I'm going to spawn a hundred,
[50:35-50:37] a thousand or thousands of cloud agents right
[50:37-50:39] now because you're just going to waste a
[50:39-50:41] lot of tokens, um, and it's going to be
[50:41-50:42] extremely expensive.
[50:43-50:43] Yeah.
[50:43-50:45] So just to kind of recap so far, basically,
[50:45-50:47] the, if we wanted to go on the journey
[50:47-50:48] that you've kind of gone on, it would be
[50:48-50:50] to start with verification, um,
[50:50-50:52] building some, some skills and some,
[50:52-50:54] some ways of determining that the agents
[50:54-50:56] are producing at least like correct code,
[50:56-50:57] whether, like you said, whether it's
[50:57-50:58] good code or not is maybe a separate question,
[50:58-51:00] but like it's, it's technically solving
[51:00-51:01] the problem by looking at, you know,
[51:01-51:03] stack traces, looking at, you know,
[51:03-51:05] the actual behavior in the app and so on.
[51:05-51:07] Um, and then once we trust it locally,
[51:07-51:08] then we can start to think about
[51:08-51:10] scaling into the cloud and running
[51:10-51:12] more agents that are picking up
[51:12-51:13] signals, I guess on their own, right.
[51:13-51:14] So whether it's like a bug report
[51:14-51:15] that comes in or something, they can
[51:15-51:16] go and pick it up and solve the
[51:16-51:19] problem and give us back a PR.
[51:19-51:20] I don't know, maybe the last step is
[51:20-51:22] like auto-merging the PRs, which is
[51:22-51:23] where you're at, maybe not where
[51:23-51:25] everyone's at, and then reviewing
[51:25-51:27] the one made, but is that, is that
[51:27-51:28] about right?
[51:28-51:29] Yeah, exactly. I think, yeah, that's
[51:29-51:31] why I drew this, this, this curve,
[51:31-51:33] right, because that, this basically
[51:33-51:35] describes my journey of, you know,
[51:35-51:37] when I started, barely could use a
[51:37-51:38] couple of agents and I was just
[51:38-51:39] observing every single thing.
[51:40-51:41] I think there's really no shortcut
[51:41-51:43] from going from here to there,
[51:43-51:45] because this is really about your
[51:45-51:47] personal level of trust in agents,
[51:47-51:49] right. Obviously, you know, as an
[51:49-51:50] engineer, you don't want to just
[51:50-51:51] slot code into production.
[51:51-51:53] So how do you actually build out
[51:53-51:56] that trust takes a lot of, I guess,
[51:56-51:59] taste and judgment, but, you know,
[51:59-52:01] like, I think plugins like P-Stack
[52:01-52:04] definitely kind of help you get up
[52:04-52:07] to speed much quicker, and so I
[52:07-52:08] guess it's like, if you trust me
[52:08-52:10] and you trust P-Stack, then in
[52:10-52:12] by extension, you can maybe trust
[52:12-52:13] your agents, but if you don't
[52:13-52:15] trust me, and I definitely would
[52:15-52:17] not encourage people to blindly
[52:17-52:20] trust me, you know, if you build
[52:20-52:22] up your own set of skills that you
[52:22-52:23] can obviously, you know, take a look
[52:23-52:25] at P-Stack and kind of fork it,
[52:25-52:26] make it your own, improve the
[52:26-52:28] skills, definitely encourage that,
[52:28-52:30] but for me, it's really all about,
[52:30-52:32] it just keeps coming back to trust.
[52:32-52:34] You know, every one of us here
[52:34-52:35] in this chat have a different
[52:35-52:37] standard for engineering, and there
[52:37-52:38] are different things that are
[52:38-52:40] important for us in our code base,
[52:40-52:43] and when you are able to encode
[52:43-52:45] all of that into skills and you can
[52:45-52:46] verify that your agent is actually
[52:46-52:48] doing them, that allows you to
[52:48-52:50] really kind of ascend this curve
[52:50-52:53] and, you know, start automating
[52:53-52:54] things.
[52:54-52:56] Yeah, I think there's a third part
[52:56-52:57] to this, which I haven't talked
[52:57-52:59] about yet, which is kind of an
[52:59-53:00] interesting one, which is like
[53:00-53:02] refactoring and rewriting, like one
[53:02-53:05] of the, I guess, most controversial,
[53:05-53:06] one of the most controversial
[53:06-53:08] topics in the industry, I think,
[53:08-53:09] is like, should you rewrite
[53:09-53:13] your app or not, because I think
[53:13-53:14] engineers are very prone to this
[53:14-53:15] where, especially when you join a
[53:15-53:17] company, you come in and you see
[53:17-53:18] like the code base and you're like,
[53:18-53:19] man, this is shit.
[53:20-53:21] Like, who wrote this code?
[53:21-53:22] You know, it's terrible.
[53:22-53:23] I want to rewrite the whole thing.
[53:23-53:25] There is a very common inclination,
[53:25-53:27] and I think a lot of, you know,
[53:27-53:29] before agents, and I guess
[53:29-53:31] arguably even now, people will
[53:31-53:32] definitely discourage you
[53:32-53:34] from rewriting stuff, but I'm
[53:34-53:35] actually here to make a case for
[53:35-53:37] why you might want to consider it,
[53:37-53:41] because I think it really depends.
[53:41-53:43] You know, Brownfield applications,
[53:43-53:45] I think, are actually in a pretty
[53:45-53:46] good spot, especially if they're
[53:46-53:49] set up well already, and like
[53:49-53:50] recently I've been talking to some
[53:50-53:52] people, but, you know, I was just
[53:52-53:55] observing, I just noticed this
[53:55-53:57] parallel, which is that a lot of
[53:57-54:00] big tech company problems are now
[54:00-54:02] everybody's problems, and the big
[54:02-54:03] tech company problem, you know,
[54:03-54:04] like when I was working at Meta,
[54:04-54:06] like we had this giant monoripo
[54:06-54:08] we had like, I don't know, 10,000s
[54:08-54:10] of engineers just, you know, like
[54:10-54:12] banging on their keyboards and
[54:12-54:15] shipping code, and a lot of really
[54:15-54:18] great engineers at Meta, but I'll
[54:18-54:20] say like, you know, you'll be
[54:20-54:21] surprised that the code quality
[54:21-54:23] is actually not that good, and so
[54:23-54:25] I often joke that like, you know,
[54:25-54:27] before AI sloth, we had human
[54:27-54:29] sloth, and so, you know, I think
[54:29-54:32] a lot of big tech info, like what
[54:32-54:34] Meta has, or Google, you know,
[54:35-54:37] really big tech companies, are
[54:37-54:38] actually designed for that, where
[54:38-54:40] you're sort of like, you're catering
[54:40-54:42] to the, you know, like, this sounds
[54:42-54:44] so bad to say, but like, the
[54:44-54:45] least capable engineer on your
[54:45-54:48] team, right, you build frameworks,
[54:48-54:49] you build conventions, you build
[54:49-54:51] guardrails, you know, you restrict
[54:51-54:53] credentials so that, you know, your
[54:53-54:54] intern doesn't wipe your production
[54:54-54:58] database, there's, you know, if
[54:58-55:00] you have that level of info
[55:00-55:02] already, I think your agents can
[55:02-55:03] actually already do a very solid
[55:03-55:05] job, right, because they have, the
[55:05-55:07] guardrails are already in place
[55:07-55:10] for agents to not cause havoc, or not
[55:10-55:12] cause too much havoc in your
[55:12-55:14] codebase, and you can always add
[55:14-55:17] more, you know, guardrails, but I
[55:17-55:18] think, yeah, it's definitely like
[55:18-55:19] a trade-off for sure, you know,
[55:19-55:21] like, nothing that's like free for
[55:21-55:22] sure, and tokens are pretty
[55:22-55:26] expensive, but oh, actually, I
[55:26-55:27] don't know how many of you have
[55:27-55:28] seen this, but we actually announced
[55:28-55:31] GROC 4.6 today, so very exciting,
[55:31-55:33] finally out, so yeah, GROC 4.6 would
[55:33-55:35] be like a great, it was very, very
[55:35-55:38] smart, it's really good on the
[55:38-55:40] benchmarks, and it's the same, the
[55:40-55:42] tokens, well, I hopefully I'm not
[55:42-55:44] saying this incorrectly, but I
[55:44-55:46] believe the cost per token is the
[55:46-55:48] same as 4.5, so you're actually
[55:48-55:50] getting more intelligence for the
[55:50-55:53] same cost, I think this is an
[55:53-55:55] area that Cursor tries to, Cursor
[55:55-55:58] and SpaceX AI, try to really
[55:58-55:59] optimize for, like that
[55:59-56:01] Pareto frontier of, you know, cost
[56:01-56:03] versus intelligence, you know, we
[56:03-56:04] don't necessarily want to build the
[56:04-56:06] biggest model ever because that is
[56:06-56:08] extremely expensive to run, it's
[56:08-56:10] really about like, how do you find
[56:10-56:11] that sweet spot, right, you don't
[56:11-56:12] need a giant model, but it's just
[56:12-56:14] super smart, right, and it's not
[56:14-56:17] very expensive for inference, but
[56:17-56:20] yeah, that's awesome, we are
[56:20-56:22] timed, so I guess, Lauren, if
[56:22-56:23] folks want to support you, maybe go
[56:23-56:27] try out GROC 4.6 and, you know,
[56:27-56:29] get to provide some feedback, but
[56:29-56:29] yeah, this was awesome, really
[56:29-56:31] appreciate you taking the time, thanks
[56:31-56:32] everyone for all the messages in the
[56:32-56:33] chat, lots of good questions, I know
[56:33-56:35] we didn't get through everything, but
[56:35-56:36] as I kind of said at the top, way more
[56:36-56:37] questions than we could get through,
[56:37-56:39] but yeah, really, really thanks,
[56:39-56:40] thanks for joining, thanks everyone
[56:40-56:42] for joining, and hopefully you
[56:42-56:45] enjoyed the session. Yep, I see,
[56:45-56:47] thanks for having me, and if you
[56:47-56:48] have any more questions, just DM me
[56:48-56:50] on Twitter, I'll open them up, I
[56:50-56:52] guess. You're gonna get a lot of
[56:52-56:55] DMs. Yeah, I'll open the updates, so
[56:55-56:56] yeah, DM me, maybe I'll do like a
[56:56-56:57] Twitter space at some point, that's
[56:57-57:00] all for more questions, but really
[57:00-57:01] appreciate everyone for showing up,
[57:01-57:02] you know, taking an hour out of your
[57:02-57:04] day. Yeah, all right, thanks, I'll see
[57:04-57:06] you the next one.

