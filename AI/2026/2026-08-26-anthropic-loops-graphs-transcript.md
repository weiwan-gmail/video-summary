# Anthropic engineer on loops, graphs, and self-improving agents

- Source: https://x.com/Mahaximus_/status/2092670041062035853
- Author: Mahax (@Mahaximus_)
- Posted: 2026-08-26 17:46 UTC
- Duration: 41:30
- Sibling: [summary](2026-08-26-anthropic-loops-graphs.summary.md)

## Tweet

Anthropic engineer:

"If you want to be in the 1% of AI engineers.

You need to build a system that improves itself [Loops and Graphs]"

In 40 minutes they break down how Anthropic's team builds with AI internally, and why Loops and Graphs are at the center of it.

## Transcript

Whisper `small` / int8, English. Video starts mid-conversation.

[00:00-00:03] You need a lot of infrastructure, you need a lot of ways to
[00:03-00:07] continue it to allow the agent to basically recover from its errors.
[00:07-00:10] And then to do work in ways that are secure and
[00:10-00:11] compliant with what you're trying to get it to do.
[00:11-00:13] And those are just a different class of problems.
[00:13-00:16] So instead of spending all this effort to tell the model to go one direction,
[00:16-00:18] you're actually just like the model's doing it,
[00:18-00:23] just enable it to continue to run longer, execute, and recover from its errors.
[00:23-00:24] Really cool.
[00:24-00:27] And maybe before we dive into exactly how that works,
[00:27-00:29] do you have some examples of how these agents are,
[00:29-00:32] these long running agents are maybe more relevant to different use cases that
[00:32-00:36] wasn't possible to serve without this type of intelligence and infrastructure?
[00:36-00:41] It's actually just happening across the board almost through all of knowledge work.
[00:41-00:44] And I think it looks a little invisible in a sense, but
[00:44-00:47] there's a lot of tasks where you give something, let's say in finance,
[00:47-00:50] where you want it to go and in the past you might have given a very,
[00:50-00:51] very concrete task.
[00:51-00:54] There is this Excel spreadsheet and you should calculate here and
[00:54-00:57] here it's very discrete and small.
[00:57-01:00] And that's kind of in the direction of you point the model at a thing and
[01:00-01:01] then you try to scaffold it around it.
[01:01-01:03] So it specifically edits the cells that you wanted to go and edit.
[01:03-01:07] And today, you should be in a direction where you're just saying oh,
[01:07-01:10] so the whole thing I actually wanted to do is I actually just own a DCF of
[01:10-01:14] that company and decide if I should invest it or not at the right price.
[01:14-01:16] And that's the level in which you're talking about it.
[01:16-01:18] And in that world, these kind of long running agents end up doing all the
[01:18-01:20] work. So they actually open the spreadsheet.
[01:20-01:22] They calculated for you.
[01:22-01:25] They then verify and say oops, I definitely did not calculate that right.
[01:25-01:26] So let me try and do it again.
[01:26-01:28] But you didn't need to like interfere.
[01:28-01:29] You didn't need to hop in there and be like,
[01:29-01:32] make sure you double check your work or any of those kinds of things.
[01:32-01:35] And so across like finance, I think across healthcare,
[01:35-01:37] across any kind of like knowledge work where you're just giving it sort of
[01:37-01:40] like an outcome, very much like you would a fellow associate.
[01:40-01:44] That is starting to become a place where work is just getting offloaded
[01:44-01:46] directly to agents and people are becoming more productive through those
[01:46-01:48] kind of innovations.
[01:48-01:51] I guess maybe to frame the conversation a little bit.
[01:51-01:54] You're both relatively new to Anthropic, right?
[01:54-01:57] And I would love to hear like, what brought you to Anthropic and what's
[01:57-01:59] the journey been like so far?
[01:59-02:01] Yeah. So I've been here about a year,
[02:01-02:04] which sounds relatively new in like normal tech jobs.
[02:04-02:07] I imagine that Anthropic, you're like a veteran now.
[02:07-02:09] Time is dilated.
[02:09-02:10] Time is so weird.
[02:10-02:13] People sometimes say actually every month feels like a year.
[02:13-02:14] I think that's maybe too extreme.
[02:14-02:17] Doesn't feel like I've been here 12 years, but so yeah,
[02:17-02:21] when I joined Anthropic, it came from Stripe previously and we were
[02:21-02:23] working together at Stripe on Stripe Connect.
[02:23-02:26] And so in some ways, similar problem spaces in the sense that we're
[02:26-02:29] working with customers who are working with a developer platform.
[02:29-02:35] They're trying to, you know, embed value within their products for
[02:35-02:38] their customers and they're working with us across the spectrum of like,
[02:38-02:41] I want primitive building block solutions or I want more out of the
[02:41-02:45] box solutions depending on where I'm at as a business and what role
[02:45-02:48] payments and financial services plays within my products.
[02:48-02:52] And so it was interesting going from that to Anthropic.
[02:52-02:55] I ended up in Anthropic because, I don't know, the industry around me
[02:55-02:59] was kind of changing in wild ways and felt just very compelling to
[02:59-03:00] come be a part of it.
[03:00-03:02] And there are folks who I've worked with in the past who are here
[03:02-03:06] now as well, but it was kind of like, you know, so compelling to
[03:06-03:09] come work on the way that all these things are changing and
[03:09-03:12] then take that kind of similar mindset of like build a developer
[03:12-03:15] platform, enable people to enhance their own products,
[03:15-03:18] enhance their own systems with this underlying technology.
[03:18-03:21] In that similar developer platform mindset where it's like we
[03:21-03:23] work with people on a more primitive basis and give them
[03:23-03:26] building blocks and then we work with people on a more like give
[03:26-03:30] you agents full-fledged out of the box and so it's been a very
[03:30-03:31] cool transition.
[03:31-03:34] I'm curious if there was like one particular moment or set of
[03:34-03:37] moments that just made you think, oh man, I've got to join
[03:37-03:40] Anthropic because it's been incredible just seeing like the
[03:40-03:42] variety of people that I thought were totally unhireable
[03:42-03:45] that have very recently joined Anthropic, whether it's
[03:45-03:48] founders or honestly ML celebrities or stuff like that.
[03:48-03:50] I'm always just kind of curious like the journey and yeah,
[03:50-03:53] you kind of had that Eureka moment that led to you joining.
[03:53-03:56] Yeah, I mean, I think almost anybody, if you really step back
[03:56-03:58] and think about what's happening, it's like really a
[03:58-04:02] revolution and technology that's happening right now and
[04:02-04:04] you always kind of want to feel like you're on the correct
[04:04-04:07] side of something that's a revolution, if that makes sense.
[04:07-04:10] And I think the way that at Anthropic we're thinking
[04:10-04:13] about these problems is we're just like really all in on
[04:13-04:16] this idea that if this technology is going to become
[04:16-04:19] so powerful, we want it to be creating really great
[04:19-04:20] outcomes within the world.
[04:20-04:23] And I think that level of thoughtfulness comes with some
[04:23-04:26] of the hardest I think work problems that you could ever
[04:26-04:27] expect to have.
[04:27-04:30] Like on a day-to-day basis, we're making decisions when it
[04:30-04:33] comes to safety and our commercial business and
[04:33-04:35] intelligence and like the intersection of all these
[04:35-04:39] things that we've assembled a team of people who can just
[04:39-04:42] think so fast on the fly but so deeply about really
[04:42-04:44] hard problems and they're intellectually open to these
[04:44-04:47] things but also, you know, like values driven and
[04:47-04:48] stick to their values in the right ways.
[04:48-04:52] And so the set of humans who are doing this together is
[04:52-04:55] just like so insanely fun to be a part of.
[04:55-04:58] And I think that just kind of getting deep on that and
[04:58-05:00] like learning about Anthropic and how we think about
[05:00-05:02] things and how the team has come together, it was just
[05:02-05:04] it was hard to pass up.
[05:04-05:05] How are you, Angela?
[05:05-05:07] So Caitlin and I left Stripe at the same time.
[05:07-05:10] Much to our team's unhappiness, we like went
[05:10-05:12] to completely separate labs and our team was kind of
[05:12-05:14] like you guys couldn't have like coordinated that.
[05:14-05:16] And we're like, no, we didn't quite chat with each
[05:16-05:17] other about that.
[05:17-05:19] So she went to Anthropic and then I went to OpenAI at
[05:19-05:20] the same time.
[05:20-05:22] At the time, chat GPT had already existed and I thought
[05:22-05:25] it was a great product but I wasn't necessarily like
[05:25-05:27] something that I actually like actively wanted to work on.
[05:27-05:29] And it actually took me a little bit and there was
[05:29-05:31] actually a moment where Caitlin and I and our teams
[05:31-05:34] had worked on this like V2 API.
[05:34-05:36] So at Stripe, there's like this idea that when you
[05:36-05:39] make, you know, the company had versioned their
[05:39-05:41] APIs from the very, very beginning with this kind of
[05:41-05:44] like really long minded, you know, concept of when you
[05:44-05:46] make this abstraction it should be like decades long.
[05:46-05:48] And it was very, very hard to go then make like the
[05:48-05:49] next version of that.
[05:49-05:51] So to deserve the version bump, you had to make
[05:51-05:53] something like, you know, the next kind of like
[05:53-05:54] couple of decades worth.
[05:54-05:57] And so it built this API, which was the V2
[05:57-05:58] Accounts API.
[05:58-06:01] And like our team had spent all this time kind of
[06:01-06:02] painstakingly like building this.
[06:02-06:04] And it was a really, really wonderful and awesome
[06:04-06:05] project.
[06:05-06:09] And I remember distinctly, we did a UXR interview with
[06:09-06:11] a customer who was going to just like integrate
[06:11-06:12] this new API.
[06:12-06:14] And at the time, they just kind of like grabbed the
[06:14-06:15] docs that we gave them and they just like put
[06:15-06:16] it into cursor.
[06:16-06:18] And they were like, oh, just integrate.
[06:18-06:21] And I was like, oh my God, what did you just do?
[06:21-06:23] And it came back and it was like 70% accurate.
[06:23-06:25] It was like, you know, a while ago.
[06:25-06:27] And that was like just eye-opening for me.
[06:27-06:29] I was like, the future is here.
[06:29-06:31] And this kind of like knowledge work, this kind of
[06:31-06:33] like just capabilities being unlocked by the
[06:33-06:35] models, like I want to be part of that.
[06:35-06:37] So then I ended up going to open AI.
[06:37-06:38] We're done the API product over there in very
[06:38-06:40] kind of like similar capacities as here.
[06:40-06:42] And then Katelyn has a version of this story,
[06:42-06:44] but effectively we tried my version.
[06:44-06:46] Yeah, you can tell it if you'd like.
[06:46-06:49] But we basically just tried to convince each other to
[06:49-06:50] come to their respective labs.
[06:50-06:51] We worked together.
[06:51-06:52] I was like, you should come over.
[06:52-06:54] And she's like, you should come over.
[06:54-06:55] And I was like, I need to end the partner.
[06:55-06:56] She's like, I need a product partners.
[06:56-06:58] We went back and forth, back and forth.
[06:58-06:59] And then the end, she won.
[06:59-07:01] So I moved over to Anthropic.
[07:01-07:02] So you sold it my way.
[07:02-07:05] Yeah, I did tell it your way.
[07:05-07:08] You know, I think like Katelyn said, like the
[07:08-07:10] talent density here and just like how much the
[07:10-07:13] company cares about making like safe AGI, I think
[07:13-07:15] is just such an awesome and incredible mission.
[07:15-07:17] And it means you do tackle the hardest problems,
[07:17-07:20] whether they're societal, economic, technological.
[07:20-07:22] When I think back to that moment of like why I wanted
[07:22-07:24] to go in to make that change, like seeing that kind
[07:24-07:27] of revolution through, so that can be distributed
[07:27-07:30] to everyone in a way that's like safe is exactly
[07:30-07:30] what I'm here to do.
[07:30-07:31] That's awesome.
[07:31-07:34] And I'm curious when you think about managed agents,
[07:34-07:37] how do open AI and Anthropic differ the most?
[07:37-07:38] Just like philosophically?
[07:38-07:40] Over time, we might potentially have like
[07:40-07:42] somewhat similar concepts.
[07:42-07:44] But I think philosophically on our end,
[07:44-07:48] we have a lot of like architectural beliefs,
[07:48-07:50] because I like Katelyn kind of like speak to.
[07:50-07:52] I think from like kind of a product angle,
[07:52-07:54] the kind of philosophy that we have with managed agents
[07:54-07:59] is that you should do as a builder on top of the platform,
[07:59-08:00] you should do the things that differentiate you
[08:00-08:02] and you shouldn't have to do things
[08:02-08:03] that are undifferentiated.
[08:03-08:06] And so from that kind of like philosophy,
[08:06-08:07] what we view as to be undifferentiated
[08:07-08:10] are basically things like the infrastructure.
[08:10-08:12] It's a really hard problem, it's a distributed system problem.
[08:12-08:14] You need a lot of scale to eventually get your customers
[08:14-08:16] to have a really awesome agentic experience.
[08:16-08:18] Going back to that example of like a long running agent
[08:18-08:20] that just like does that DCF for you,
[08:20-08:21] actually takes quite a bit of work
[08:21-08:22] to go make that like just work.
[08:22-08:25] And there's largely an infrastructure problem these days
[08:25-08:27] as opposed to like a pure kind of like
[08:27-08:28] harness optimization problem.
[08:28-08:30] So therefore we view that as like largely
[08:30-08:31] undifferentiated, so we should go
[08:31-08:33] and like resolve that for you.
[08:33-08:34] Now there is a layer of differentiation
[08:34-08:35] that you should do.
[08:35-08:37] Like they're having different philosophies
[08:37-08:38] out there in the world that maybe
[08:38-08:40] there's one true harness that does everything.
[08:40-08:42] I think empirically we kind of like don't see that to be true.
[08:42-08:44] And we would probably lean on like
[08:44-08:46] there's different layers of optimization
[08:46-08:47] that you should be doing
[08:47-08:50] and how do we give you more control to go do those things.
[08:50-08:52] So you should be innovating at the layer of like
[08:52-08:54] you really understand your customer really well
[08:54-08:55] and you know your problem space
[08:55-08:57] and how do you bring those insights
[08:57-09:00] and tweak the pieces at the highest level
[09:00-09:02] so that you can just like get that best performance,
[09:02-09:05] best customer experience for that agentic system
[09:05-09:06] that you created.
[09:06-09:07] But you should just go do it at that layer
[09:07-09:09] as opposed to like doing all the work
[09:09-09:10] at the undifferentiated layer,
[09:10-09:13] which I mean it's hard and it's challenging
[09:13-09:14] but it's probably not gonna result
[09:14-09:16] in the business outcomes that you're kind of hoping for.
[09:16-09:17] I'm curious if you wanna speak a bit
[09:17-09:18] on some of the systems pieces.
[09:18-09:21] So as models have gone better at working for longer,
[09:21-09:24] they were like okay great I can do these long running tasks
[09:24-09:25] and get things done.
[09:25-09:27] The wall that a lot of people hit
[09:27-09:29] is the infrastructure around this agent.
[09:29-09:31] So like yes it's undifferentiated
[09:31-09:34] but you also kind of have to like get it right
[09:34-09:36] but it's not necessarily about the infrastructure itself.
[09:36-09:38] I think maybe the way that people are thinking about this
[09:38-09:41] like I have an agent and it needs to be able to accomplish stuff
[09:41-09:43] but you can't go rogue, right?
[09:43-09:45] So it needs some guardrails
[09:45-09:48] and I'll put it in a sandbox like what people call
[09:48-09:49] but it's just like container
[09:49-09:50] but you call it a sandbox
[09:50-09:52] and it's like you can play in there
[09:52-09:53] and not mess anything up.
[09:53-09:55] And so it's kind of like okay,
[09:55-09:58] put your agent in a sandbox and let it do its thing.
[09:58-10:00] But the problem is the technology
[10:00-10:02] that drives sandboxes is often
[10:02-10:03] they're meant to be ephemeral, right?
[10:03-10:05] They're not necessarily meant to be
[10:05-10:07] long running infrastructure.
[10:07-10:09] And so what we've spent a lot of time and energy on
[10:09-10:12] is how do we rethink the agent,
[10:12-10:15] make it a more kind of modular broken down architecture
[10:15-10:16] and say maybe like the harness
[10:16-10:18] or the brain of the agent runs over here
[10:18-10:20] on a server that's durable
[10:20-10:22] and then when it needs to execute work
[10:22-10:24] which is a scary part, go spawn a sandbox,
[10:24-10:26] do it within the sandbox
[10:26-10:28] and then tear down the sandbox when it's done.
[10:28-10:30] Because in that world if one of your sandbox dies
[10:30-10:32] you lose connection, whatever it might be
[10:32-10:34] your whole agent doesn't die.
[10:34-10:36] And that's us having formed an opinion
[10:36-10:39] on this having built many agents internally
[10:39-10:40] and within our products
[10:40-10:42] and then trying to take those concepts
[10:42-10:44] and put them into the platform
[10:44-10:45] and make that available for people
[10:45-10:48] to be able to take advantage of the models
[10:48-10:51] being great at executing really long running work
[10:51-10:53] without having to solve the problem over and over again
[10:53-10:54] of like how do I do this
[10:54-10:56] from an architecture and infrastructure perspective?
[10:56-10:57] Maybe taking a step back,
[10:57-11:01] like if I'm a CTO CEO VP Venge
[11:01-11:03] at a large Fortune 500 company
[11:03-11:04] and I'm coming to you guys and I'm saying,
[11:04-11:06] hey, I love this idea of long running agents.
[11:06-11:07] It's really cool.
[11:07-11:08] The rest of my employees right now
[11:08-11:10] are using cloud co-work to some capacity
[11:10-11:11] but it's really not the same
[11:11-11:14] as like me putting in production for my customers.
[11:14-11:14] Where do I start?
[11:14-11:15] I heard this hardest thing
[11:15-11:17] is like a really cool busy term
[11:17-11:18] but I don't even know what it means.
[11:18-11:19] I'm trying to figure out like what's the,
[11:19-11:21] what's, how do I do my prompt caching
[11:21-11:22] and the context engineering?
[11:22-11:24] Like any advice there are just high level
[11:24-11:26] like where do you think these executives should start
[11:26-11:27] because it feels still
[11:27-11:29] that they're in the early days of adopting this
[11:29-11:30] even though the capabilities
[11:30-11:32] it seems like it's just exponentially going up.
[11:32-11:33] Yeah, we would actually just tell you
[11:33-11:35] to use cloud advantage agents like literally
[11:35-11:37] this is actually one of the reasons
[11:37-11:38] why we designed this product.
[11:38-11:40] It's a set of higher order abstractions
[11:40-11:43] and you can access the lower layers.
[11:43-11:45] So you can imagine there's probably a bit of like
[11:45-11:47] a life cycle, you know, if you're just starting out
[11:47-11:48] you probably shouldn't have to like worry
[11:48-11:50] about all these like really complicated details
[11:50-11:52] to just get your employees to be able to like
[11:52-11:53] build something that works
[11:53-11:55] for some long running process that they want to have.
[11:55-11:56] And so using cloud manage agents is like
[11:56-11:58] literally the single easiest way
[11:58-12:00] for you to go ahead and do that.
[12:00-12:02] And if you get more and more opinionated over time
[12:02-12:03] where do you want to, you know
[12:03-12:05] be able to tweak very, very specific details
[12:05-12:06] maybe over time you're like actually
[12:06-12:08] I have now formed a very concrete opinion
[12:08-12:10] on exactly how I want to do my prompt caching
[12:10-12:11] with extreme control.
[12:11-12:13] You can go ahead and like go to our lower level primitives
[12:13-12:15] that allow you to go and do that.
[12:15-12:17] But we really want to kind of give people
[12:17-12:19] these kind of like, you know, great starting points
[12:19-12:21] so that you can go ahead and experiment
[12:21-12:23] and figure out what's actually gonna be useful
[12:23-12:24] for your organization.
[12:24-12:26] I think that for a lot of these kind of leaders
[12:26-12:29] they see the ROI on the other side
[12:29-12:31] or they can imagine it
[12:31-12:32] but getting started is like just really tough.
[12:32-12:35] And so the more like friction we can reduce
[12:35-12:37] and then just make it easy for you to kind of see
[12:37-12:39] if you give something an outcome
[12:39-12:41] and it actually just ends up producing it for you
[12:41-12:43] that really unlocks maybe the possibilities
[12:43-12:44] that you could have without having to deal
[12:44-12:47] with I think a lot of the technical complexity
[12:47-12:48] in order to just get started.
[12:48-12:50] And even like, I don't know
[12:50-12:52] I would say a lot of our stuff internally
[12:52-12:54] someone's like I need to spin up an agent
[12:54-12:55] to do a thing.
[12:55-12:56] They'll build on cloud manage agents
[12:56-12:59] even if they're like the world's deepest expert
[12:59-13:01] on something like prompt caching and context management
[13:01-13:03] because it's not always the highest level
[13:03-13:06] reduce of your time to like rehack that stuff each time.
[13:06-13:09] And so the point of cloud manage agents is like
[13:09-13:11] a harness that like pretty generically is good
[13:11-13:15] at that stuff and like holding onto a model
[13:15-13:17] and letting it do long running work
[13:17-13:19] but then what we exposed you is like
[13:19-13:20] you can tune the system prompt
[13:20-13:22] you can set up skills
[13:22-13:24] you can have MCP connections
[13:24-13:27] to whatever external contacts and these sorts of things.
[13:27-13:28] And so there's a lot of control
[13:28-13:30] that you actually have within those agents
[13:30-13:32] to make them really great at the thing that you care about
[13:32-13:35] without having to do some of that lower level
[13:35-13:36] harness engineering work
[13:36-13:38] which makes it something that even our team reaches for
[13:38-13:40] for a lot of the things that they want to get done.
[13:40-13:41] Really cool.
[13:41-13:43] And is there some element of trust
[13:43-13:44] that you have to navigate?
[13:44-13:46] Whether it's just elegant off ramps
[13:46-13:48] if something goes awry or some type of guardrail
[13:48-13:50] is like how does how should executives
[13:50-13:51] work with you guys on that
[13:51-13:52] when they do the manage agents?
[13:52-13:54] Yeah, I think there's two layers of trust.
[13:54-13:55] The first one is kind of baked
[13:55-13:57] into the architecture of managed agents
[13:57-13:59] where it's about like making sure
[13:59-14:00] that when the agent does work
[14:00-14:03] it's within your security bounds to go and do that.
[14:03-14:04] And so we have offerings
[14:04-14:06] for bringing your own sandbox
[14:06-14:07] and other things like that.
[14:07-14:09] But that's probably the most crucial bit
[14:09-14:10] is of course that the agent's gonna touch
[14:10-14:11] your production systems
[14:11-14:14] and do work on sensitive internal data.
[14:14-14:15] That should absolutely be something
[14:15-14:16] that you have control over
[14:16-14:18] and you decide exactly how that happens.
[14:18-14:19] I think the second layer
[14:19-14:21] is actually on as a ability of the agent.
[14:21-14:23] So this is kind of a good problem to have
[14:23-14:24] in the sense that you want the agent
[14:24-14:25] to be capable of doing things.
[14:25-14:28] And once it does you go into the next stage
[14:28-14:29] of problem where it's like,
[14:29-14:31] okay, well, did it do it correctly
[14:31-14:34] and kind of make sure that it's like audible
[14:34-14:35] and it's actually like executing
[14:35-14:37] in the way that I hope it can.
[14:37-14:39] And that layer we try to offer
[14:39-14:40] quite a bit of like observability and tooling
[14:40-14:42] so that you can kind of inspect it.
[14:42-14:43] There's still a lot of integration
[14:43-14:45] that you'll need to do with your systems in a sense
[14:45-14:46] but I think those two layers
[14:46-14:47] are probably the most important ones
[14:47-14:49] to build the right levels of trust
[14:49-14:51] so that ultimately you can empower your employees
[14:51-14:53] or alternatively your users
[14:53-14:55] to have that level of like autonomy.
[14:55-14:56] Cool.
[14:56-14:57] How do you kind of think about
[14:57-14:59] which parts of the infrastructure stack
[14:59-15:02] to offer yourselves versus where to keep it open
[15:02-15:06] and just partner with external infrastructure companies?
[15:06-15:09] Yeah, I think honestly there's not very much
[15:09-15:10] that we're super precious about.
[15:10-15:13] Obviously running and serving our models, right,
[15:13-15:15] is the part that we're gonna keep doing.
[15:15-15:17] And as you go up the stack, you know,
[15:17-15:19] our safety classifiers that are running
[15:19-15:22] all these sorts of things, we care a lot about that.
[15:22-15:23] And really everything I'm describing
[15:23-15:26] is the layer below the messages API
[15:26-15:28] which is our like most primitive API
[15:28-15:31] that gets you access to tokens within the model.
[15:31-15:33] Everything above that, I think that's where we're
[15:33-15:36] in the territory of being opinionated about architecture
[15:36-15:39] but not necessarily opinionated about infrastructure.
[15:39-15:41] And so we wanna get like today,
[15:41-15:42] I think we live in a world where we've got
[15:42-15:43] our very primitive API
[15:43-15:44] and then we have cloud managed agents
[15:44-15:46] as our higher order stuff.
[15:46-15:48] And I think we wanna break this down more
[15:48-15:49] and Angela mentioned, you know,
[15:49-15:51] you can self host your sandboxes today.
[15:51-15:54] We offer infrastructure for MCP tunnels
[15:54-15:56] like heavier MCP servers behind a firewall
[15:56-15:58] and the agent can still reach them.
[15:58-16:00] I think we want more and more of that
[16:00-16:02] to be able to be self hostable over time
[16:02-16:05] because again, it's like the infrastructure
[16:05-16:08] is it's whatever you want it to be,
[16:08-16:09] however you wanna run it.
[16:09-16:10] I think as long as we're conforming
[16:10-16:12] to the architecture that we think is gonna be powerful,
[16:12-16:15] we have less opinions about the infrastructure itself.
[16:15-16:18] It feels like there's a common fallacy right now
[16:18-16:21] among closed versus open models just like writ large.
[16:21-16:23] The first being like if I use a closed model,
[16:23-16:25] I'm giving off my context and data and fropic
[16:25-16:27] and therefore I'm losing my advantage as a company.
[16:27-16:30] Can you just like to bunk that for us?
[16:30-16:31] Yeah, we don't train on your data.
[16:31-16:35] So it's like straight up we do not do that.
[16:35-16:36] And so I think there's a,
[16:36-16:38] I understand like there's maybe some concerns
[16:38-16:41] or like belief that we might believe actively do not.
[16:41-16:43] I guess how do you think about the sort of argument
[16:43-16:44] for cost?
[16:44-16:47] So, you know, maybe I'm using managed agents
[16:47-16:49] but maybe there's an argument that
[16:49-16:50] I would love to use managed agents
[16:50-16:52] with open source models to get cost down internally
[16:52-16:54] as I scale up my agents.
[16:54-16:57] What would be the most common sort of way to keep cost down
[16:57-17:00] while still only using for example, anthropic models?
[17:00-17:02] Yeah, it's something that we're actively exploring.
[17:02-17:04] I think people tend to reach for models
[17:04-17:06] as like the mechanism to go into that,
[17:06-17:08] which I think is reasonable to an extent.
[17:08-17:09] But when we look at like the kinds of problems
[17:09-17:10] that you're trying to solve,
[17:10-17:12] so we ask you, what are you actually trying to do?
[17:12-17:15] So here heard on cost, but what were you trying to do?
[17:15-17:16] And usually the answer is like,
[17:16-17:18] I was trying to like ship this product faster
[17:18-17:20] or I was trying to like make my team more efficient,
[17:20-17:22] right? There's like an actual business outcome
[17:22-17:23] at the end of all of that stuff.
[17:23-17:26] And we're more oriented on how do we go,
[17:26-17:28] help you get that business outcome
[17:28-17:31] at like as cheap, as reasonable as a cost as possible.
[17:31-17:33] So our general interpretation of that kind of direction
[17:33-17:36] is not necessarily that the best solution
[17:36-17:38] is to always reach for a variety of different models.
[17:38-17:41] We think that probably more likely
[17:41-17:43] is that we need to get a better job
[17:43-17:45] at understanding the outcome that you want.
[17:45-17:46] And then from that outcome,
[17:46-17:49] make sure we take the absolute most efficient path.
[17:49-17:50] And sometimes that might counterintuitively
[17:50-17:54] actually be using a bigger, more expensive model.
[17:54-17:56] As long as that model is actually like
[17:56-17:58] every single token is correct.
[17:58-17:59] If every single token is correct, you waste nothing
[17:59-18:01] and you've like perfectly solved that problem.
[18:01-18:03] And that's gonna end up being a lot cheaper
[18:03-18:05] than it would look like if you just look at things
[18:05-18:07] from a pure like token point of view.
[18:07-18:09] Now there are obviously some like specific tasks
[18:09-18:12] that I think don't require that level of intelligence.
[18:12-18:14] And over time, our hope is to get to a place
[18:14-18:17] where we're actually very, very good at detecting
[18:17-18:18] when you need to go and do that
[18:18-18:20] so that we can execute the same strategy
[18:20-18:24] of like just put enough perfect tokens effectively
[18:24-18:25] to go solve that problem for exactly
[18:25-18:27] that cost structure that you need.
[18:27-18:29] And I think that that is like the direction
[18:29-18:31] that like we're kind of like pushing the bounds on
[18:31-18:32] and where we're trying to invest.
[18:32-18:34] I think these like kind of token economics
[18:34-18:36] are somewhat divorced unfortunately from the reality.
[18:36-18:37] We really wanna make sure that we index
[18:37-18:40] on like what the true objective is
[18:40-18:41] and then make sure that that thing
[18:41-18:45] is actually cost effective and of the right shape for you.
[18:45-18:46] Can you see more about that actually?
[18:46-18:49] Because another fallacy is like all tokens are the same.
[18:49-18:50] Like it's very fungible and like Emma compares it
[18:50-18:52] to like gas or electricity.
[18:52-18:55] And obviously this feels like a fallacy, at least in my eyes.
[18:55-18:56] Like can you just say more about that?
[18:56-18:58] Like how every token is a little bit different
[18:58-18:59] and you guys are doing all the hard work
[18:59-19:01] in the background to help automate some of that.
[19:01-19:04] Yeah, I think today we're trying to figure out,
[19:04-19:07] so we're doing a lot of experimentation as a team
[19:07-19:09] on the different jobs that you could give to tokens.
[19:09-19:12] And what we would like to get to is a point where
[19:12-19:13] maybe people don't have to think that hard about it
[19:13-19:15] and we're automating more of it.
[19:15-19:17] In the meantime, we just want to put more of that control
[19:17-19:18] in people's hands to think about these things
[19:18-19:21] and share our learnings on how we think these things
[19:21-19:22] should work.
[19:22-19:24] And so we've had a few strategies that we've come up with
[19:24-19:26] that we've seen work really well
[19:26-19:28] for how you give tokens different jobs
[19:28-19:29] than just pure executing.
[19:29-19:32] And so a really good example is advising.
[19:32-19:33] You have a smaller model that's doing its work,
[19:33-19:36] it's executing and it reaches out to a larger model
[19:36-19:39] for help or advice when it's like
[19:39-19:40] a harder part of the problem.
[19:40-19:43] And we've seen like I think we've got some evals
[19:43-19:47] that show like sonnet executing with opus advising
[19:47-19:49] ends up getting almost opus level performance
[19:49-19:52] and it's actually cheaper than just sonnet
[19:52-19:55] because opus taught it how to do its job better
[19:55-19:57] and it used less tokens to get the job done.
[19:57-20:00] And so that's one example of use tokens
[20:00-20:02] for different jobs, not just executing also advising.
[20:02-20:05] We also have this concept of outcomes
[20:05-20:08] within cloud managed agents where you give a rubric,
[20:08-20:09] like here's what good looks like
[20:09-20:12] and we'll provision a second agent that's a greater.
[20:12-20:15] And so the first agent tries and then it's like,
[20:15-20:17] okay, I tried the greater is like not quite good enough,
[20:17-20:21] go again, and you get to a better outcome ultimately
[20:21-20:24] because you've done that kind of the greater
[20:24-20:26] and the executor do the work together.
[20:26-20:29] Dreaming is another one where you look back
[20:29-20:30] over past sessions and you write to memory
[20:30-20:32] and you write skills to improve.
[20:32-20:35] And so we definitely have some really strong evidence
[20:35-20:36] that if you give tokens different jobs
[20:36-20:40] besides just executing, you can get to a better,
[20:40-20:42] maybe like intelligence per dollar sort of setup
[20:42-20:45] than if you were just brute force executing.
[20:45-20:48] And I think what we're trying to say is like over time,
[20:48-20:49] we actually don't want you to have to like work
[20:49-20:52] as hard as we are to come up with what those strategies are
[20:52-20:54] and we'll do more of that stuff kind of automatically
[20:54-20:56] out of the box for you.
[20:56-20:57] Super cool.
[20:57-20:58] One thing I think you mentioned earlier,
[20:58-21:00] maybe I read in the past, which is like the,
[21:00-21:02] just maybe I'll call like harness engineering.
[21:02-21:04] Can you just talk about like what is a harness
[21:04-21:05] for those who don't know and then maybe like
[21:05-21:07] best practices or lessons learned there
[21:07-21:10] between the coordination, the execution
[21:10-21:12] and all the different components underneath that
[21:12-21:15] seem to get bundled into what is now called the harness.
[21:16-21:18] Yeah, so a harness is a loop,
[21:18-21:21] which is a little bit of a joke right now,
[21:21-21:24] but a harness really is like the most basic version
[21:24-21:26] of a harness is like a while loop
[21:26-21:28] that's literally just like go back and forth
[21:28-21:31] between like get input from the user, ask the model
[21:31-21:34] what it thinks, then call a tool over here
[21:34-21:35] and you keep that thing running.
[21:35-21:37] And it's just kind of the thing that holds onto a model
[21:37-21:40] and manages all of those parts of a conversation.
[21:40-21:44] But once you get into an agent wants to do more work
[21:44-21:46] or longer running work, then you have, okay,
[21:46-21:49] now you need an environment to execute those tools
[21:49-21:51] and do that work that's gonna be safe.
[21:51-21:54] And if you wanna be able to stop your conversation
[21:54-21:56] and pick it up later, you actually need to be storing
[21:56-21:58] the conversation state somewhere.
[21:58-22:01] So that's kind of another piece that comes into play.
[22:01-22:03] You've got credentials like secure credentials
[22:03-22:06] if you're gonna go reach out to an external system
[22:06-22:08] through MCP or whatever it is
[22:08-22:09] and you wanna inject those credentials,
[22:09-22:12] but you don't want the agent to actually see the credentials
[22:12-22:13] like that becomes another part of the system
[22:13-22:15] that you inject at a certain time.
[22:15-22:17] And so there's a lot of these pieces around the edges
[22:17-22:20] but really the most like basic version of this thing
[22:20-22:22] is like the very small bit of code that's running
[22:22-22:24] that just keeps hitting the model,
[22:24-22:27] asking the user for input and going back and forth.
[22:27-22:29] And then taking that like very core piece of the harness
[22:29-22:31] and we've like overused this word harness
[22:31-22:33] to mean like practically everything up
[22:33-22:34] to like an application at this point.
[22:34-22:37] But that very core piece is like the most fundamental one
[22:37-22:39] on top of that is where if you can get all these pieces
[22:39-22:41] you can get to the place where you start doing
[22:41-22:42] these more innovative things
[22:42-22:44] where you do give token jobs
[22:44-22:47] and you truly start to treat them as not fungible.
[22:47-22:49] And so you can add the next layer
[22:49-22:51] and some people have used the word like meta harness,
[22:51-22:52] we've used the word like strategy,
[22:52-22:55] but it's like once you've gotten the core execution done
[22:55-22:57] you can do the next thing which is like
[22:57-22:59] maybe you coordinate the agents in a slightly different way
[22:59-23:00] they can engage with each other,
[23:00-23:02] they can feedback into each other's loops,
[23:02-23:03] they have slightly different jobs.
[23:03-23:05] And those areas we're seeing more alpha
[23:05-23:06] get created these days
[23:06-23:08] because the most basic stuff is now
[23:08-23:09] somewhat like understandable, right?
[23:09-23:11] You handle the errors, you make sure the loop happens,
[23:11-23:12] you make sure it's long running,
[23:12-23:14] but given your problem space and your domain
[23:14-23:16] and what you're trying to solve
[23:16-23:18] how you actually compose these strategies together
[23:18-23:19] we've actually seen that they result
[23:19-23:21] in some pretty different performance outcomes
[23:21-23:23] and that is specific I think
[23:23-23:25] to what you're trying to get that agent to achieve.
[23:25-23:26] You've now worked with I'm sure tons
[23:26-23:29] and tons of teams outside of anthropic building agents.
[23:29-23:32] What are the most common misconceptions about agents?
[23:32-23:34] What are the most common mistakes people make
[23:34-23:37] when they try to implement them internally
[23:37-23:39] just like any learnings for the average company
[23:39-23:40] that hasn't felt like they've gotten
[23:40-23:42] the full potential of agents yet?
[23:42-23:44] Yeah, I think people tend to try to bite off
[23:44-23:46] more they can chew as like the first problem
[23:46-23:47] they're like, they look at the promise
[23:47-23:49] of what that could be and they're like, okay, awesome
[23:49-23:50] I'm going to give it like a huge task
[23:50-23:54] task and I'm going to like automate my entire KYC process
[23:54-23:55] for my like massive bang.
[23:55-23:57] This is like an area where a lot of people can see
[23:57-23:59] you know, like the intuition
[23:59-24:00] from why you'd want to do that
[24:00-24:02] but then they end up having a really hard time
[24:02-24:03] making that a reality
[24:03-24:05] because they haven't really broken it up
[24:05-24:07] into like the absolute core pieces.
[24:07-24:10] And I think the fundamental fallacy there is like
[24:10-24:13] you take a very human process that's been ducted together
[24:13-24:16] and it works and it has all these policies
[24:16-24:18] and then you just try to like insert agents
[24:18-24:21] exactly where you see human inefficiencies
[24:21-24:23] and it's a somewhat hard proposition
[24:23-24:27] because in reality that doesn't actually work
[24:27-24:29] you end up having to try to like conform
[24:29-24:31] the agent to exactly what the human
[24:31-24:32] was attempting to do
[24:32-24:34] and what we've seen much better successes
[24:34-24:36] you can still pick a really ambitious project
[24:36-24:37] break it up like pretty aggressively
[24:37-24:39] into like the most basic thing
[24:39-24:42] that you would imagine almost like a new hire doing
[24:42-24:44] and then just reinvent that process to be agent first
[24:44-24:46] and sometimes it's surprising
[24:46-24:48] sometimes it means like you actually don't want
[24:48-24:49] you know, an agent to do something
[24:49-24:50] and then come back to you
[24:50-24:51] in a more fruitful direction
[24:51-24:53] we've actually seen that
[24:53-24:54] like give it something that can like
[24:54-24:56] it can autonomously fleet and self review
[24:56-24:58] and only maybe like escalate to you when necessary
[24:58-25:00] as a human if you were to ask a, you know
[25:00-25:02] subject matter expert when they do that
[25:02-25:02] they would probably say like
[25:02-25:04] I don't want to do that
[25:04-25:06] I would prefer that it does the thing
[25:06-25:07] and ask me for feedback
[25:07-25:08] and I keep going back and forth this way
[25:08-25:09] but it doesn't really work
[25:09-25:12] because really the agent is reinventing the workflow
[25:12-25:14] and so the more natively you can kind of re-express it
[25:14-25:16] and kind of delete some of your
[25:16-25:17] you know previous processes
[25:17-25:18] and design from scratch
[25:18-25:21] the more successful you'll like end up being
[25:21-25:24] What do you think is the future form factor
[25:24-25:26] to get like with humans and AI?
[25:26-25:29] My intuition that some part of this delta
[25:29-25:30] between AI's capabilities
[25:30-25:32] and like actual adoption today
[25:32-25:34] has to do a little bit with UX
[25:34-25:35] and kind of the interaction patterns
[25:35-25:38] Do you have any intuition on where we're going with AI?
[25:38-25:40] Yeah, I think we've like seen
[25:40-25:42] all sorts of form factors come through
[25:42-25:44] and you know like just even two years ago
[25:44-25:47] everyone was like chats like it
[25:47-25:49] and so we're just through a chat box like everywhere
[25:49-25:49] Totally
[25:49-25:50] when you get to a place where like
[25:50-25:51] I don't want to do that anymore
[25:51-25:53] I'd like want to actually engage directly with an agent
[25:53-25:55] and the agent does all the work
[25:55-25:56] so I think you know there's
[25:56-25:57] these form factors are just like rapidly changing
[25:57-26:01] and the kind of through line that we sort of see
[26:01-26:02] is you almost wanted to be
[26:02-26:05] almost like slightly more human ironically
[26:05-26:07] or maybe not ironically since it's AI
[26:07-26:08] as artificial intelligence
[26:08-26:09] and you wanted to get to the place where
[26:09-26:11] it acts a little bit more like
[26:11-26:13] a really amazing co-worker
[26:13-26:14] like kind of the best in class one who
[26:14-26:16] you know can push back in the right places
[26:16-26:17] but does all the work
[26:17-26:18] and like never complains
[26:18-26:20] and like really gets like the whole context
[26:20-26:22] and in that world you probably engage with it
[26:22-26:23] much more than you would engage with like
[26:23-26:26] just like the best co-worker you've like ever worked with
[26:26-26:27] so I think the form factors
[26:27-26:29] tend to be a little bit more human ironically
[26:29-26:31] like you might for example with with cloud tag
[26:31-26:33] the form factor for that is actually in Slack
[26:33-26:35] because that's where just like humans
[26:35-26:36] are engaging with each other
[26:36-26:37] and a lot of the cool stuff is happening
[26:37-26:38] like under the hood
[26:38-26:40] but really it's doing all this like
[26:40-26:41] kind of horsework to make sure that
[26:41-26:43] ultimately cloud just like gets it done
[26:43-26:46] and just understands what you wanted to go and do
[26:46-26:47] but the UI layer of it is just familiar
[26:47-26:50] it's exactly what you've always known in Slack
[26:50-26:52] and I think increasingly that kind of direction
[26:52-26:53] is where we're gonna see agents
[26:53-26:56] be more democratized to everyone
[26:56-26:57] because it's just a form factor
[26:57-26:59] that you use with anyone else
[26:59-27:01] Oh there, what do you think Kaelin?
[27:01-27:04] Yeah I mean I think there's also just gonna be
[27:04-27:07] this like continuation of agents
[27:07-27:08] can do stuff for you
[27:08-27:10] when you're not paying attention to them
[27:10-27:11] and I think in that world
[27:11-27:13] we're just gonna continue to need
[27:13-27:16] to have ways to say like
[27:16-27:18] but how do I like set off an agent
[27:18-27:19] to go do a thing that like
[27:19-27:22] is gonna come back with what I actually care about, right?
[27:22-27:24] And so I think that part
[27:24-27:26] is gonna continue to matter a lot
[27:27-27:28] I have people on my team who will be like
[27:28-27:30] oh I've got this hard problem to solve
[27:30-27:31] and I think I'm gonna like send some agents off
[27:31-27:33] when I go to sleep tonight
[27:33-27:35] and like see what they come back with in the morning
[27:35-27:37] and so I think just figuring out the right ways
[27:37-27:39] to have people have that experience
[27:39-27:41] where they're like there's agents in the background
[27:41-27:43] they're doing work for me
[27:43-27:46] but I have the right ways to express what I actually want
[27:46-27:49] and steer them in the direction that I want them to go
[27:49-27:50] is really what's gonna matter
[27:50-27:52] and I think we're gonna be doing a lot of work
[27:52-27:53] to figure out what the right form factor is
[27:53-27:54] for that to look like
[27:55-27:57] I don't think anybody has perfect answers to that yet
[27:57-28:01] As you think about more and more complex processes
[28:01-28:04] how do you think about what should be product
[28:04-28:06] and what should be a for-deployed engineer
[28:06-28:08] from Anthropa going into an enterprise
[28:08-28:12] and getting their hands dirty and figuring things out?
[28:12-28:14] I think actually in many cases
[28:14-28:16] the ideal case would probably be that
[28:16-28:17] that person at that company
[28:17-28:18] is actually able to figure it out
[28:18-28:20] in either direction whether it's a product
[28:20-28:23] from anyone or a for-deployed person
[28:23-28:25] it means that you're assisting
[28:25-28:26] at the end of the day you're assisting
[28:26-28:28] and you're trying to help express
[28:28-28:30] what that person ultimately wants
[28:30-28:32] I think the most magical outcome
[28:32-28:34] that is probably like most true
[28:34-28:36] to growing model capabilities
[28:36-28:37] is that the only thing really helping you
[28:37-28:39] is actually just the model
[28:39-28:40] so in the most pure sense
[28:40-28:42] the way that you would solve any problem
[28:42-28:44] is you would just literally talk to Claude
[28:44-28:46] and Claude would do everything
[28:46-28:48] whether that's helping you express yourself better
[28:48-28:50] or trying to build a scaffolding for you
[28:50-28:51] or even maybe it builds a product for you
[28:51-28:53] so that you can then re-express yourself
[28:53-28:54] and then it can tear it down
[28:54-28:55] and then build whatever process it is
[28:55-28:56] that you were hoping you could do
[28:56-28:59] so that's I think maybe the core piece
[28:59-29:00] now obviously we're not there today
[29:00-29:03] and I think depending on where your life cycle is
[29:03-29:06] there's what you're hoping to do as a company
[29:06-29:09] is to actually just inspire your employees
[29:09-29:11] to see the art of the possible
[29:11-29:13] you'd probably go reach for a product I think
[29:13-29:15] to kind of just help you get that initial sense
[29:15-29:16] and then with that initial sense
[29:16-29:18] with that realization that you have agency yourself
[29:18-29:20] to create a bunch of things
[29:20-29:21] one of our favorite things that happens at the company
[29:21-29:24] is like you have new employees come in
[29:24-29:26] they suddenly get access to the Claude products
[29:26-29:28] and they can go ahead and use them
[29:28-29:30] and they're like wow I can
[29:30-29:32] I don't need to ask permission from anyone
[29:32-29:34] I can just go and build what I wanted
[29:34-29:35] and sometimes what they want to say
[29:35-29:36] like tiny little dashboard
[29:36-29:37] but in the past you had to go
[29:37-29:39] and ask all these people right
[29:39-29:40] there's not a lot of agency in that
[29:40-29:41] and today you need to be like
[29:41-29:43] I literally talked to Claude
[29:43-29:44] and Claude deployed it
[29:44-29:44] and we're like that's awesome
[29:44-29:47] and he just feel like I can do things now
[29:47-29:48] so I think that's really incredible
[29:48-29:50] and I think sometimes just giving people a product
[29:50-29:52] to go and do that, to show them
[29:52-29:54] I think that that's really like part of the way
[29:54-29:56] to really kind of accelerate your organization
[29:56-29:58] and your company
[29:58-29:59] and other instances I think there's I think
[29:59-30:00] some things where you're just kind of like
[30:00-30:02] this is just such a freaking hard problem
[30:02-30:03] it's been so hard
[30:03-30:05] there's no like custom fit product
[30:05-30:06] to go and solve this
[30:06-30:07] and these are just kind of like
[30:07-30:09] foundational business problems usually
[30:09-30:11] something along the lines of like
[30:11-30:13] you know there's like maybe a large scale
[30:13-30:15] code migration that is going to take
[30:15-30:18] literally like 12 years for us to go and accomplish
[30:18-30:20] and it's a pain it's been a tax on the company
[30:20-30:22] for a really really long time
[30:22-30:24] and those kinds of things you can imagine
[30:24-30:26] probably you're not going to buy a product for that
[30:26-30:28] and you might want to take like some help
[30:28-30:29] I mean so an FTE coming in
[30:29-30:31] or alternatively having your engineers
[30:31-30:35] be of a mindset of like trying to use it with AI
[30:35-30:36] they can come in and be like
[30:36-30:38] okay I'm going to kind of custom design a process
[30:38-30:39] I'm going to iterate through this
[30:39-30:41] and at the end result will be like
[30:41-30:43] if I can solve this like code migration problem
[30:43-30:45] I really have also unlocked the company
[30:45-30:47] to do something they never could believe was possible
[30:47-30:49] so those 12 years of migration effort
[30:49-30:51] turn into like you know call it like
[30:51-30:52] three months or something like that
[30:52-30:53] and that I think is an incredible
[30:53-30:54] like mindset opening as well
[30:54-30:56] then what else could you do if you could do that
[30:56-30:58] I thought it was pretty staggering to learn
[30:58-31:00] that your team is only 200 people
[31:00-31:02] I mean we're talking many millions of
[31:02-31:03] customers and billions in revenue
[31:03-31:04] like you're going to operate a scale
[31:04-31:06] that effectively is almost unprecedented
[31:06-31:07] very shortly
[31:07-31:09] how do you guys, is there only like philosophy
[31:09-31:12] or opinion to have on org design and culture
[31:12-31:14] and managing the most leverage out of people
[31:14-31:16] because it's pretty incredible
[31:16-31:18] to do what you guys are doing
[31:18-31:19] and be this unsung heroes
[31:19-31:21] to make sure everyone has this magical
[31:21-31:22] authentic experience
[31:22-31:24] yeah I think the way we think about it today
[31:24-31:26] we're still we're I'm saying still
[31:26-31:28] probably always we'll be in this world where
[31:28-31:30] we think about our team similar to how
[31:30-31:32] people thought about teams for a long time
[31:32-31:34] in this industry
[31:34-31:35] like you have a set of human
[31:35-31:37] to understand a certain part of the system
[31:37-31:39] they have product ownership over where
[31:39-31:40] they want those things to go
[31:40-31:42] and the problems that they want to solve
[31:42-31:44] but they're just so leveraged
[31:44-31:46] is the difference with the tools
[31:46-31:47] that they have or that they're creating
[31:47-31:50] for themselves on the fly to get things done
[31:50-31:52] and so I do think it's been
[31:52-31:54] a journey that we've been on to figure out
[31:54-31:55] certain roles and certain people
[31:55-31:57] are very positively leveraging
[31:57-31:58] get a lot more done
[31:58-31:59] they can delegate a lot of things to agents
[31:59-32:01] and and make things happen
[32:01-32:03] similar with you know certain tech leads
[32:03-32:04] I would say
[32:04-32:05] like we have big projects that are happening
[32:05-32:07] where you know we have to
[32:07-32:08] work with all the clouds
[32:08-32:10] because we deploy our platform
[32:10-32:11] across all the different clouds
[32:11-32:13] we have internal teams that we work with
[32:13-32:15] across all the different concerns
[32:15-32:16] around safety and infrastructure
[32:16-32:18] like all these different pieces
[32:18-32:19] a lot of them sit within our team
[32:19-32:21] a lot of them sit external to our teams
[32:21-32:22] and the work
[32:22-32:24] to just get everybody on the same page
[32:24-32:25] about what we're going to ship
[32:25-32:26] and how it's going to work
[32:26-32:28] and especially when we're in the landscape
[32:28-32:30] of hard questions to answer
[32:30-32:32] that we talked about earlier
[32:32-32:34] like those sorts of roles are struggling
[32:34-32:36] because it used to be
[32:36-32:37] you start a project right
[32:37-32:39] and then a bunch of engineers go
[32:39-32:41] and and they click the clock
[32:41-32:42] and the work gets done right
[32:42-32:44] and during that time
[32:44-32:45] the more coordinating roles
[32:45-32:46] like the product manager
[32:46-32:48] the tech lead or a TPM
[32:48-32:49] whatever it might be
[32:49-32:50] can go do all that work
[32:50-32:51] to get everybody aligned
[32:51-32:52] and on the same page
[32:52-32:53] and now it's like
[32:53-32:55] you kick off that project
[32:55-32:57] you have a sense for where you want to go
[32:57-32:58] and engineers are kind of like
[32:58-32:59] okay cool it's done
[32:59-33:00] like two days later
[33:00-33:01] and you haven't had the time
[33:01-33:02] to do all the work
[33:02-33:04] to get everybody on the same page
[33:04-33:05] and so that I think is where
[33:05-33:07] we've definitely been on a journey
[33:07-33:09] within our team to figure out
[33:09-33:10] how do we just solve for that
[33:10-33:12] like how do we get to a place where
[33:12-33:14] that the things that are now bottlenecks
[33:14-33:16] become less bottlenecky over time
[33:16-33:19] and we set people better up for success
[33:19-33:20] but on the whole yeah
[33:20-33:23] like 200 people for the platform
[33:23-33:24] the product infrastructure
[33:24-33:25] all the things that we're doing
[33:25-33:27] if you told me a year ago
[33:27-33:28] that we'd be doing this
[33:28-33:29] with this number of people
[33:29-33:31] I would have said is absolutely impossible
[33:31-33:33] there's no way
[33:33-33:34] and it's just been cool to see
[33:34-33:36] how much leverage we've been able to get
[33:36-33:37] Oh
[33:37-33:39] what do you think Angela has a product lead
[33:39-33:40] like what's the intuition around
[33:40-33:41] like do you expect more
[33:41-33:42] from every individual you work with now
[33:42-33:46] or like how do you scale this team of 200 people
[33:46-33:47] One kind of thing
[33:47-33:48] that's been coming through recently
[33:48-33:49] is really I almost feel like
[33:49-33:51] they have to be almost like
[33:51-33:53] the purest forms of their job
[33:53-33:55] if I were to pick on product for example
[33:55-33:57] you know there's plenty of locomotive pieces
[33:57-33:58] of product management
[33:58-33:59] where it's like about coordination
[33:59-34:00] it's about like project management
[34:00-34:02] it's about getting people on the same page
[34:02-34:03] it's about moving forward
[34:03-34:04] but a lot of those things
[34:04-34:05] actually become less important
[34:05-34:07] because like they happen so quickly
[34:07-34:09] and you don't need to be like
[34:09-34:12] okay I want to allocate this engineering teams
[34:12-34:14] you know two weeks sprint cycle
[34:14-34:15] to do XYZ
[34:15-34:17] like that is now just like conversation with Claude
[34:17-34:18] and that just like happens
[34:18-34:20] so a lot of these things where
[34:20-34:23] traditionally product managers maybe
[34:23-34:25] you know could kind of lean on those places
[34:25-34:26] that they kind of don't exist anymore
[34:26-34:28] and so instead what you have to operate it
[34:28-34:29] is actually the absolutely like hardest level
[34:29-34:31] and almost like the purest level
[34:31-34:32] of what you need to do
[34:32-34:34] like what should we really be solving for
[34:34-34:36] who should we actually be solving for
[34:36-34:37] and these like
[34:37-34:38] sound like simple things to say
[34:38-34:39] but it's actually like almost like
[34:39-34:41] the purest form of problem solving
[34:41-34:43] and your ability to go and do that
[34:43-34:45] is like being required more and more
[34:45-34:46] and so from this sense
[34:46-34:48] I think it's a definitely a transformative
[34:48-34:49] like timeframe
[34:49-34:51] where PMs have to truly do like
[34:51-34:52] the true product bits
[34:52-34:53] and they don't really have
[34:53-34:55] a lot of the other pieces anymore
[34:55-34:56] and so the bets that you take
[34:56-34:58] the hypotheses that you make
[34:58-34:59] the thesis that you have
[34:59-35:00] like it really really matters
[35:00-35:02] in making sure that you do it right
[35:02-35:03] and are we talking like a
[35:03-35:05] what should we build in the next month
[35:05-35:05] six months
[35:05-35:06] like at what point is
[35:06-35:08] things moving too fast underneath you
[35:08-35:09] know things are moving so fast
[35:09-35:10] it's actually working here
[35:10-35:12] is actually really changed my mind
[35:12-35:14] on like how we would do product for
[35:14-35:15] at least for anthropic
[35:15-35:17] I don't know how much I would generalize this
[35:17-35:18] but you know normally you'd be like
[35:18-35:20] okay I do my homework
[35:20-35:21] and I'd probably pick a bet right
[35:21-35:23] and I'd like double down in this bet
[35:23-35:25] and then here you still do that
[35:25-35:26] but more often than not
[35:26-35:27] it's like the space of uncertainty
[35:27-35:29] is actually so high
[35:29-35:31] and then because the outcomes are so variable
[35:31-35:32] in that like distribution
[35:32-35:33] you actually need to build like
[35:33-35:35] a portfolio very very quickly
[35:35-35:37] so that you can kind of almost like
[35:37-35:38] if any of the bets hit
[35:38-35:39] you kind of win
[35:39-35:41] and it's a really weird way to do product
[35:41-35:42] because you'd be like
[35:42-35:43] it's not hyper focused
[35:43-35:44] it's more like
[35:44-35:45] you actually want the portfolio
[35:45-35:47] I guess maybe a little bit more like invested
[35:47-35:48] I was going to say
[35:48-35:49] so maybe there's a future where that's
[35:49-35:52] that's actually a very aligned job role
[35:54-35:54] but yeah
[35:54-35:56] which is a really weird way to build product
[35:56-35:58] but it's because so much of what you have to build
[35:58-36:00] can just be built like instantaneously
[36:00-36:01] so you don't really need to like
[36:01-36:03] you know like hyper concentrate on prioritization
[36:03-36:04] and things like that
[36:04-36:04] it's still important
[36:04-36:06] but only at the absolute highest layers
[36:06-36:08] and building that expression and container
[36:08-36:10] so that any possible outcome
[36:10-36:11] can result in positive
[36:11-36:13] of externalities for you
[36:13-36:14] is like how you actually need to start thinking
[36:14-36:16] which is a really weird way to think about
[36:16-36:17] a lot of that stuff
[36:17-36:18] Wow
[36:18-36:20] that must be a higher tolerance for failure
[36:20-36:21] extremely high
[36:21-36:22] also your team is right
[36:22-36:23] I might keep it normal to work on stuff
[36:23-36:25] and just switch a month later
[36:25-36:25] and say whatever
[36:25-36:27] we get a little bit less tolerance for failure
[36:27-36:28] on the engineering side
[36:28-36:30] but it actually it's funny
[36:30-36:32] we talk about it sometimes with our team
[36:32-36:33] is we have to be a team
[36:33-36:35] that's really ready to get punched in the face
[36:35-36:38] it's like literally the phrase that we use with our teams
[36:38-36:40] because we've got a plan
[36:40-36:41] and we're doing some stuff
[36:41-36:42] right everyone's got a plan
[36:42-36:43] until you get punched in the face
[36:43-36:45] and like the things that are punching us in the face
[36:45-36:48] are there's like really hard safety problems to solve
[36:48-36:49] or there's really hard infrastructure
[36:49-36:51] scale problems to solve
[36:51-36:52] like I don't think any of us thought
[36:52-36:53] six months ago
[36:53-36:56] we'd have a scale situation
[36:56-36:57] that we'd be in
[36:57-36:59] that is like quite this extreme
[36:59-37:00] I tell the story sometimes
[37:00-37:02] I went back home to New York
[37:02-37:04] for Christmas and saw my family
[37:04-37:05] and they were all kind of like
[37:05-37:05] what do you work on?
[37:05-37:08] And probably Claude like what is this?
[37:08-37:10] And then in the spring or on Easter time
[37:10-37:11] I went back home
[37:11-37:14] and my cousin was like
[37:14-37:15] let me show you my Mac menu
[37:15-37:16] of my open cloth set up
[37:16-37:18] and I was like whoa
[37:18-37:19] they were like Claude you work on Claude
[37:19-37:21] that's awesome and so
[37:21-37:22] but in the timeframe that that happened
[37:22-37:24] that meant that our team was
[37:24-37:27] and every token that flows in and out of Claude
[37:27-37:29] in the world is running through the systems
[37:29-37:30] that our team has built
[37:30-37:32] and so there's a lot there
[37:32-37:34] from the perspective of scale
[37:34-37:36] and that's just one example
[37:36-37:37] of the many things that
[37:37-37:39] in January when we made our plan
[37:39-37:40] for all the things we were gonna go work on
[37:40-37:42] and the way that we were gonna place our bets
[37:42-37:43] we had to do some pivoting
[37:43-37:46] to think a little bit differently about our plans
[37:46-37:48] and I think that's just gonna be a constant
[37:48-37:49] in this era
[37:49-37:51] when things are evolving and changing so quickly.
[37:51-37:54] Given that you're literally agent experts
[37:54-37:57] are there any sort of things that you've set up
[37:57-37:59] in your personal productivity workflows
[37:59-38:02] that would be interesting for us to learn about?
[38:02-38:03] I think one thing that I would say
[38:03-38:05] that's been most interesting for me
[38:05-38:08] has been working on developer products for a long time
[38:08-38:11] has been it's really hard to make time
[38:11-38:13] to dog food your own products
[38:13-38:15] because you have to go write a bunch of code
[38:15-38:17] to integrate with your own API
[38:17-38:20] to build stuff to actually experience how they work
[38:20-38:22] and today that has become so much easier
[38:22-38:26] to be able to spend time dog fooding our own products
[38:26-38:29] and so it'll just be like little things here and there
[38:29-38:30] like I one time was kind of like
[38:30-38:32] we have a set of customers
[38:32-38:33] that are doing this really interesting thing
[38:33-38:34] with the platform
[38:34-38:36] and I wanna go see what they've built
[38:36-38:39] and normally I would open a browser
[38:39-38:41] and I would go make accounts on all these different
[38:41-38:44] services and go play around with the product and see
[38:44-38:46] and I was able to kind of just be like
[38:46-38:48] Claude managed agents like Claude
[38:48-38:50] can you please go build an agent
[38:50-38:53] that can go use all these different products
[38:53-38:55] and come back with screenshots or whatever it is
[38:55-38:58] so I can understand how customers are using the product
[38:58-38:59] so there's all these sorts of little things
[38:59-39:02] where it's like just so much easier now
[39:02-39:05] to have a sense for how customers are experiencing
[39:05-39:07] our products and how we need to evolve
[39:07-39:10] because it's so much faster and easier to use agents
[39:10-39:14] to test the agents which is kind of meta
[39:14-39:15] but I think we're living in a cool world
[39:15-39:17] from that perspective.
[39:17-39:19] Yeah for me I'm just all in on like remote agents
[39:19-39:21] I use remote agents to do like anything
[39:21-39:23] whenever they do something I always want them
[39:23-39:25] to remember it so I'll just kind of like
[39:25-39:27] I'll literally just tell Claude like remember
[39:27-39:30] and save to memory and that's all I do
[39:30-39:31] and I just keep talking to it
[39:31-39:32] and every time I'm gonna happy with it
[39:32-39:34] I'm like that was wrong, remember that was wrong
[39:34-39:36] didn't do it again, save it to memory
[39:36-39:37] and watch it save to memory
[39:37-39:38] and I just like go back and forth with it
[39:38-39:41] and it's actually been like the simplest thing ever
[39:41-39:43] and I like have found myself to be like massively
[39:43-39:45] more productive because I just tell you
[39:45-39:47] remember what I like did or didn't like
[39:47-39:48] and I love that I don't really have to like
[39:48-39:50] click anything or do anything
[39:50-39:51] except for it is like tell Claude
[39:51-39:52] so that's been super fun for me.
[39:52-39:55] One last question for me you are in the center
[39:55-39:57] like I consider the platform to be unsung heroes
[39:57-39:59] like everything you're doing is just incredible
[39:59-40:01] but I imagine you feel like a push and pull
[40:01-40:02] or a little bit of a tug of war between
[40:02-40:04] the compute and the data center guys
[40:04-40:06] versus the application team and like everyone around
[40:06-40:09] like how do you interact with all the teams
[40:09-40:11] and understand like what you need to do
[40:11-40:12] versus like influence everyone else
[40:12-40:13] and what they need to do.
[40:13-40:16] Yeah we really do sit in the middle
[40:16-40:17] it's very interesting.
[40:17-40:19] I think one of the maybe less known things
[40:19-40:22] about our platform is the exact same set of APIs
[40:22-40:25] the exact same platform that our external customers
[40:25-40:28] build on top of is what our first party products
[40:28-40:29] are all built on top of.
[40:29-40:32] And so it's interesting because our first party products
[40:32-40:34] are our customers for our team
[40:34-40:38] and then to your point yeah we also sit right above
[40:38-40:41] accelerators and inference and research and models
[40:41-40:42] and all these sorts of different things
[40:42-40:45] and so Anthropic is still small enough
[40:45-40:48] that we can still kind of just be best friends
[40:48-40:50] with all the different teams that are working on
[40:50-40:51] all these different problems
[40:51-40:54] and we're still scrappy enough to be able to say
[40:54-40:56] we've got a big thing that needs to happen right
[40:56-40:58] like maybe we've got a new class of models coming out
[40:58-41:00] and like end to end across all the things
[41:00-41:02] these things need to work really well
[41:02-41:03] we can still kind of put together
[41:03-41:05] like Tiger teams right or just groups of people
[41:05-41:07] who are just all in on a certain problem
[41:07-41:09] across a whole bunch of different functions
[41:09-41:10] and get those things done.
[41:10-41:12] And so I don't think there's any secret sauce
[41:12-41:14] other than just like strong relationships
[41:14-41:16] and finding the right ways to get scrappy
[41:16-41:17] and work together.
[41:17-41:19] Cool thank you both so much this is awesome
[41:19-41:20] really appreciate it.
[41:20-41:21] Thank you.
[41:21-41:22] Thank you.

