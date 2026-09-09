# Google graph engineering / GraphRAG with ADK (Anatoli share)

- Source: https://x.com/AnatoliKopadze/status/2097380989538591155
- Author of tweet: Anatoli Kopadze (@AnatoliKopadze)
- Speakers (from transcript): **Annie** (Google Developer Relations engineer; main lab presenter from ~09:16); **Tilda** (named interlocutor in the opening conceptual segment). Opening segment also has an unnamed Google/ADK instructor. Anatoli promotes the video; he does not appear as a speaker.
- Posted: 2026-09-08
- Duration: 60:22
- Sibling: [summary](AI-2026-09-08-google-graph-engineering.summary.md)

## Tweet

This is the best 1 hour on graph engineering ever recorded, just released by Google how to go from a single agent to a full 24/7 system from scratch:

00:00 - what graphs actually are
09:16 - your first working agent
21:15 - graph engineering explained
41:03 - graph engineering in practice
52:21 - graphs that improve themselves

I've seen $500 courses that teach less than this video alone.

Watch it, then take it further with my step-by-step guide on graph engineering below.

### Chapters (from tweet)

| Time | Label |
| --- | --- |
| 00:00 | what graphs actually are |
| 09:16 | your first working agent |
| 21:15 | graph engineering explained |
| 41:03 | graph engineering in practice |
| 52:21 | graphs that improve themselves |

## Transcript

Whisper `small` / int8, English. ASR often hears GraphRAG as GraphRack, LLM as LIM, Gemini as gemnet / John Nipro, etc. Keep lines as-is.

[00:00-00:04] is you can think of your creating a graph workflow in the system.
[00:04-00:07] The graph can be something like you know organizational chart.
[00:07-00:10] And inside of this graph, each node can be agent node.
[00:10-00:14] It can be a function node, which can be a deterministic logic.
[00:14-00:19] It can be more. And then you're basically creating this graph in the system to solve the problem.
[00:19-00:22] So I'm still a little confused about all this terminology.
[00:22-00:25] Can you clarify like what is the harness?
[00:25-00:27] What is the loop and what is the graph?
[00:27-00:29] Yeah, that is a good question. It can be very confusing.
[00:29-00:32] So if you take a look at this picture, we have this harness part.
[00:32-00:38] So harness part is everything around the model, including its tools, memory, and god drills.
[00:38-00:43] And the loop can be the cycle that agent is running inside that harness.
[00:43-00:46] For example, the L, I'm doing the reasoning, trying to make a decision,
[00:46-00:51] picking a different tool, and selecting a different tool until it solves the problem.
[00:51-00:53] And until it's meeting the goal.
[00:53-00:57] And graph can be the organizational chart we were talking about earlier.
[00:57-01:00] It can contain agent node, containing function node, and more.
[01:00-01:03] Makes sense. So when you traverse the graph,
[01:03-01:06] you're passing memory or information down the graph to the next node.
[01:06-01:10] Yeah, exactly. So if you build with Google agent development kit ADK,
[01:10-01:15] if you build a multi-agent system, and we have this shared state among different agents.
[01:15-01:20] If you build a workflow, we have shared state among nodes in this workflow as well.
[01:20-01:22] What would a real-life example look like?
[01:22-01:25] Oh, so, Tilda, have you done PR review?
[01:25-01:27] Oh, unfortunately, yes, I hate code review.
[01:27-01:29] Tell me there's a way to make it easier.
[01:29-01:31] Imagine you want to automate the PR review.
[01:31-01:33] You're creating this workflow to automate the process.
[01:33-01:37] And because you already know exactly how to do the PR review,
[01:37-01:39] you know the workflow ahead of the time.
[01:39-01:41] So you're creating this workflow.
[01:41-01:44] And just like the picture you're seeing right now, we have three parts.
[01:44-01:46] So the first part of this workflow, including this fan out,
[01:46-01:49] and the second part is the joint, and the third part is the router.
[01:49-01:51] So let's start with the fan out part.
[01:51-01:55] The final part is we're starting this five parallel processing
[01:55-01:59] to pull the information for the PR, like a pull request.
[01:59-02:02] So you're probably familiar with the parallel processing, right?
[02:02-02:02] Yeah, absolutely.
[02:02-02:06] You might take one task and break it into like five different parts,
[02:06-02:08] and then you run them each at the same time,
[02:08-02:10] which is much faster than running them one after another
[02:10-02:11] and waiting for them all to finish.
[02:11-02:14] And the next is once you finish the parallel processing,
[02:14-02:15] we want to have a join node.
[02:15-02:18] Join node is basically to synthesize the results.
[02:18-02:20] So it's waiting for the slowest processing.
[02:21-02:22] And then it's inside the results that later on
[02:22-02:24] we can handle this information.
[02:24-02:26] And then we go to the last part, which is the router part.
[02:26-02:30] So we're using the router pattern to handle this information.
[02:30-02:32] You're probably familiar with router, right?
[02:32-02:36] I'm familiar with like a server router where you take a URL
[02:36-02:38] and then you match it with the kind of web page
[02:38-02:39] that you want to serve up.
[02:39-02:41] How does that relate to AI graph engineering?
[02:41-02:42] Oh, it's very similar.
[02:42-02:45] For the router pattern, basically you have this request input.
[02:45-02:50] And then we router to different sub-agent or specialist
[02:50-02:51] or different workflow.
[02:51-02:54] In our specific example, the condition is if the code fills,
[02:54-02:57] we will go to the specialized fixer agent.
[02:57-02:58] If the code pass,
[02:58-03:01] we will go to the human approval processing.
[03:01-03:03] So it sounds like we're taking basic principles
[03:03-03:07] of control flow and applying them to AI engineering.
[03:07-03:09] So this is a little embarrassing,
[03:09-03:12] but when I first heard about graph engineering,
[03:12-03:14] I thought that it was about knowledge graphs
[03:14-03:16] and the data model, but it sounds like that's not true.
[03:16-03:18] Yeah, it can be very confusing.
[03:18-03:20] A lot of terminology has graph.
[03:20-03:21] We have graph engineering.
[03:21-03:22] We have a graph rag.
[03:22-03:24] We have knowledge graph,
[03:24-03:26] but knowledge graph emphasizing on the data
[03:26-03:29] and graph engineering emphasizing on the behavior.
[03:29-03:30] Basically what goes in,
[03:30-03:33] that in what order and then what happens next.
[03:33-03:36] And just like the example we covered earlier.
[03:36-03:37] So how is graph engineering different
[03:37-03:38] than loop engineering?
[03:38-03:39] That's a good question.
[03:39-03:42] So loop engineering basically you have this one running loop
[03:42-03:44] and keep running until it's retrieving the goal.
[03:44-03:46] And the graph engineering is you're creating
[03:46-03:47] this graph workflow.
[03:48-03:49] And then inside of the graph,
[03:49-03:51] you have different node and different edge
[03:51-03:53] to solve the problem.
[03:53-03:55] Do you know when to use what?
[03:55-03:57] It sounds like loop engineering is better
[03:57-04:01] for simple workflows like I want a one paragraph summary.
[04:02-04:03] And graph engineering would be better
[04:03-04:05] for a much more complex workflow.
[04:05-04:09] Like I need a 50 page PDF with a bunch of graphics
[04:09-04:10] and different shiny things.
[04:10-04:13] I know there's another terminology called agents one.
[04:13-04:15] What is the difference between graph engineering
[04:15-04:16] and agents one?
[04:16-04:18] They're both agent orchestration patterns,
[04:18-04:20] but under the hood they're pretty different.
[04:20-04:23] So in graph engineering, you as the engineer,
[04:23-04:25] you define each node,
[04:25-04:27] what happens at each step of the workflow,
[04:27-04:29] how the data looks and everything.
[04:29-04:32] And also agent that it says at a certain node,
[04:32-04:33] it doesn't need to know what happened before.
[04:34-04:37] And this whole thing gives you really good
[04:37-04:39] predictability, debugability,
[04:39-04:42] and control for problems that can be really strictly defined
[04:42-04:44] like the PR workflow you mentioned earlier.
[04:44-04:46] What about agent swarm?
[04:46-04:49] Well, not all problems are easily defined like that.
[04:49-04:50] In an agent swarm,
[04:50-04:53] you have each agent just gets its own personality
[04:53-04:54] and that's it.
[04:54-04:56] And you just throw the problem to them.
[04:56-04:59] So it sounds like if you want to solve an ambiguous problem
[04:59-05:00] and we want to use agent swarm,
[05:02-05:03] because it's more flexible,
[05:03-05:05] we can handle more ambiguous use case.
[05:05-05:08] But if you already know the workflow ahead of time,
[05:08-05:09] like the PR review example,
[05:09-05:11] we can use graph workflow.
[05:11-05:12] Exactly, you got it.
[05:12-05:15] So that's graph engineering in a nutshell.
[05:15-05:16] In today's episode,
[05:16-05:20] we will level up by learning the three workflow agents
[05:20-05:22] that oxyree tasks,
[05:22-05:24] also three communication mechanism
[05:24-05:27] that let agent communicate with each other.
[05:27-05:28] By the end of today's episode,
[05:28-05:31] you will learn how to structure flows
[05:31-05:33] and get your agent talk to each other.
[05:33-05:34] And let's get started.
[05:35-05:38] The first part of today's episode is workflow agent.
[05:38-05:41] So we already know agent can form hierarchy,
[05:41-05:44] the organizational chart from last episode.
[05:44-05:47] But how do we control the flow of work?
[05:48-05:50] That is where workflow agents come in.
[05:50-05:52] We have three workflow agents
[05:52-05:55] and the first type is sequential agent.
[05:55-05:57] They're like an assembling line.
[05:57-06:01] So each sub agent run in a fixed order.
[06:01-06:03] They pass in results along.
[06:03-06:06] It is perfect for case like you fetch data
[06:06-06:10] and do the cleaning and analyze and then summarize.
[06:10-06:13] The second type of workflow agent are parallel agent.
[06:14-06:15] They're like a manager,
[06:15-06:19] assigning tasks to three employees all at once.
[06:19-06:22] It is really great for use case like independent tasks.
[06:22-06:27] For example, you're fetching data from multiple APIs simultaneously.
[06:27-06:30] And the third type of workflow agent are loop agent.
[06:30-06:35] They're like your debug again and again until it works.
[06:35-06:38] So loop agent run tasks again and again
[06:38-06:40] until a condition is met
[06:40-06:43] or meeting the maximum iteration number.
[06:43-06:46] The second part of today's episode is
[06:46-06:49] how do agent communicate with each other?
[06:49-06:52] You know from last episode we know hierarchy
[06:52-06:54] and just now we talk about workflow agent.
[06:54-06:58] But how do agent actually talk to each other?
[06:58-07:02] So ADK gives us three communication mechanism.
[07:02-07:06] And the first of them are shared session state.
[07:06-07:09] You can think of it as a shared wide board.
[07:09-07:13] So one agent write its result and pass it to next agent
[07:13-07:15] and the next agent read it from this wide board.
[07:15-07:20] For example, an LIM agent can save its output to the state.
[07:20-07:24] And another agent can pick it up and read the state output.
[07:24-07:27] The second type of communication mechanism
[07:27-07:29] are LIM driven delegation.
[07:29-07:31] That is where it gets smart.
[07:32-07:35] A coordinated agent as like a CEO.
[07:35-07:37] He will look at the request and decide,
[07:37-07:40] okay, which sub agent should I delegate to?
[07:41-07:46] For example, if the request is generate an invoice
[07:46-07:49] and the CEO will browse it to billing agent.
[07:49-07:52] The third type of communication mechanism
[07:52-07:55] are explicit invocation agent as a tool.
[07:55-07:59] Here, one agent can call another agent like a function
[07:59-08:02] instead of using it as a sub agent.
[08:02-08:05] So you wrap the target agent as a tool.
[08:05-08:09] The parent decide, okay, when should I invoke this tool?
[08:09-08:12] For example, a parent agent doing analyze
[08:12-08:15] might call a calculator agent as a tool
[08:15-08:17] whenever math is required.
[08:17-08:20] So you may wonder what is the real difference
[08:20-08:23] between agent as a tool to sub agent?
[08:23-08:25] In this diagram on the screen,
[08:25-08:27] you can see the difference between them.
[08:27-08:32] To summarize, a sub agent is part of an organizational chart
[08:32-08:35] and is always managed by its parent agent.
[08:35-08:39] An agent as a tool is like bringing a consultant.
[08:39-08:40] You call them where you need it,
[08:40-08:44] but they're not part of your core hierarchy.
[08:44-08:46] All right, let's quickly wrap up
[08:46-08:48] on what we talk about in today's episode.
[08:48-08:51] We talk about workflow agent gives the orchestration pattern.
[08:51-08:54] We have sequential pattern, parallel pattern,
[08:54-08:56] and also loop pattern.
[08:56-08:59] We also talk about three communication mechanism
[08:59-09:01] through agents.
[09:01-09:03] We have shared session state,
[09:03-09:07] LLM delegation, and explicit invocation.
[09:07-09:10] Together, this makes your multi-agent system
[09:10-09:13] not just structure, but collaborative and flexible.
[09:14-09:15] And that's it.
[09:15-09:16] Hi there.
[09:16-09:17] By the end of this video,
[09:17-09:19] you will learn how to build
[09:19-09:22] GraphRack AI agent with Google agent development kit
[09:22-09:24] capable of semantic search,
[09:24-09:26] hypersearch, and answering complex questions
[09:26-09:27] in knowledge graph.
[09:28-09:29] Hi friends.
[09:29-09:30] If you're new here,
[09:30-09:32] I'm Annie and developed relations engineer,
[09:32-09:35] previously worked as sub-engineer for seven years
[09:35-09:37] on that building production system.
[09:37-09:41] Currently, I'm helping developer building AI agent.
[09:41-09:44] So this is something I personally really curious about
[09:44-09:48] that how does GraphRack help AI understanding
[09:48-09:50] complex relationship in data?
[09:50-09:52] So if you're curious about how to build
[09:52-09:55] AI agent step-by-step in practice,
[09:55-09:56] don't forget to subscribe.
[09:56-09:59] All right, let's dive in and start building.
[10:03-10:05] So today, let's go through this lab.
[10:06-10:09] So if you go to the top right of the screen,
[10:09-10:11] you will see the lab link.
[10:12-10:17] And this lab is about AI agent with graph rack,
[10:17-10:19] with ADK and memory bank.
[10:19-10:20] And for this video,
[10:20-10:23] we will focus on how to build a GraphRack
[10:23-10:25] AI agent with ADK.
[10:26-10:29] And this is what's the final result.
[10:29-10:31] And you can see that they have the 3D rendering
[10:32-10:36] of the final relationship for all the data
[10:36-10:38] we're going to play around today.
[10:38-10:40] And if you open the camera,
[10:40-10:43] you can use your hand to control this graph.
[10:43-10:44] It's pretty cool.
[10:44-10:47] And at the very bottom, if you ask questions,
[10:47-10:49] you can do a search.
[10:49-10:52] And here we're going to cover hybrid search,
[10:52-10:53] semantic search, and keyword search.
[10:54-10:55] Pretty cool.
[10:55-10:57] All right, so let's get started.
[10:57-10:59] Before I start,
[10:59-11:01] you will see that we have some environment set up
[11:01-11:03] and this is skip if you're in the workshop
[11:03-11:05] and this is not.
[11:05-11:08] So this lab is actually designed for Google workshop.
[11:08-11:11] But if you're watching this video right now,
[11:11-11:12] you don't have to worry too much about it.
[11:12-11:15] You just directly start with the step two.
[11:15-11:17] If you're curious about workshop information,
[11:17-11:19] you can go to the last page.
[11:19-11:22] And here you can see this is a workshop series.
[11:22-11:26] You can go from level zero to all the way to level five.
[11:26-11:29] So it's all the lab related to multi-modal agent.
[11:29-11:30] If you're curious about it.
[11:30-11:33] But for this step, you can actually run it independently.
[11:33-11:34] So you don't have to worry too much.
[11:35-11:37] So let's get started.
[11:39-11:43] At the very first, you need to enable billing account.
[11:43-11:47] So here we're going to give you $5 free credits
[11:47-11:50] so that you can have GCP account set up.
[11:50-11:52] And for this whole process,
[11:52-11:55] you do not need to put any payment information on credit card.
[11:55-11:57] If you ask you to input your credit card,
[11:57-12:00] you can just skip that and just claim the $5
[12:00-12:05] so that you have this credit to do this graph rack lab.
[12:05-12:05] All right.
[12:05-12:09] So this is a testing account I have at C.
[12:10-12:13] If you open it, you can see we have this way back home data.
[12:13-12:16] And just click here to claim your credit.
[12:16-12:17] All right.
[12:17-12:20] So here just click accept and continue.
[12:20-12:23] Then you will see our credit successfully applied.
[12:23-12:25] So now you have a free credit
[12:25-12:28] that allow you to do the rest of the lab.
[12:30-12:31] All right.
[12:31-12:34] So the second step is to open environment.
[12:34-12:37] And here we are opening a Cloud Shell editor environment.
[12:38-12:42] This is like VS Code environment, but on cloud.
[12:42-12:47] The reason we are doing Cloud Shell is we have this control environment
[12:47-12:49] so that everyone can reproduce the same thing.
[12:49-12:52] Imagine that if you want to set up on VS Code
[12:52-12:56] or different IDE locally and everybody have a different setup
[12:56-12:58] or different operating system,
[12:58-13:00] it might be really hard for you to reproduce the same thing
[13:00-13:02] because at the end of the day,
[13:02-13:05] you want to reproduce the same cool app with a graph rack.
[13:05-13:07] So if you want to reproduce this,
[13:07-13:10] it's easier to do it in this control environment.
[13:10-13:15] And this is, as you can see, very similar to VS Code.
[13:15-13:16] I'm going to zoom in a little bit
[13:16-13:17] so that you can see it more clear.
[13:19-13:19] Cool.
[13:19-13:21] So now I successfully opened it.
[13:22-13:26] And those are the steps that just to open the terminal
[13:26-13:27] and editor.
[13:27-13:31] And you can see I already have this editor and terminal open.
[13:31-13:32] So I'm good to go.
[13:32-13:36] And the next step is to making sure we have the,
[13:36-13:38] set the project ID and everything.
[13:38-13:42] So I just copy this code and paste to the terminal.
[13:42-13:43] All right.
[13:43-13:45] As you can see, I'm trying,
[13:45-13:47] it's saying that I'm currently using this account.
[13:48-13:50] Just making sure that the account you're using
[13:50-13:54] is actually the account that you're claiming the credit just now.
[13:54-13:55] Oh, by the way,
[13:55-13:57] if you are claiming the credits,
[13:57-13:59] making sure you're using a Gmail account,
[14:00-14:02] it doesn't work for your educational account
[14:02-14:04] or an additional account.
[14:04-14:06] And also if you run into any error,
[14:06-14:09] you can try to claim it in a incognito window.
[14:09-14:11] That usually resolve most issues.
[14:12-14:15] So let's go ahead and clone our report.
[14:15-14:18] So next step, I want to open this folder
[14:18-14:20] because it's a file and open folder.
[14:20-14:22] So here, let's see.
[14:23-14:24] So when you open the folder,
[14:24-14:27] you might see that you lose the terminal.
[14:27-14:31] So you can click the top right there to open the terminal.
[14:31-14:32] Or you can click this button
[14:32-14:37] similar to how you're opening the terminal in VS Code.
[14:37-14:39] As you can see that we have this different level,
[14:39-14:42] this actually corresponding to our workshop.
[14:42-14:43] So this, as I mentioned before,
[14:43-14:46] this lab is also designed for Google AI workshop.
[14:46-14:48] But if you're watching this video,
[14:48-14:50] you can just continue this lab as independent content.
[14:50-14:51] You do not have to worry about it.
[14:51-14:53] But if you're curious about the lab,
[14:54-14:58] this level, each level, level zero to level five,
[14:58-15:00] actually corresponding to those folder over here.
[15:00-15:03] So you can navigate the code for different level
[15:03-15:05] if you're curious about other content.
[15:05-15:07] But for this video, we will focus on level two.
[15:07-15:11] So I'll just open the level two for today's video.
[15:11-15:12] Cool.
[15:13-15:15] And I just finished the second step.
[15:15-15:17] Let's go to the third step.
[15:17-15:18] Environment is set up.
[15:18-15:19] And here at the very beginning,
[15:19-15:21] it's still the similar step.
[15:21-15:23] You just open the terminal.
[15:23-15:26] And what's next is I want to run the script
[15:26-15:30] to initiate its script to set up the repo.
[15:30-15:33] So what I do is I copy this, click this,
[15:33-15:36] and go to the Cloud Shell and paste to the terminal.
[15:37-15:41] So what it does is it's trying to create a project ID for me
[15:41-15:44] and attach to the project, to the billing account
[15:44-15:45] we claimed earlier.
[15:45-15:48] And here you can see you can either
[15:48-15:50] press enter to create a new project.
[15:50-15:51] I already created the ID for you
[15:51-15:54] or you type an existing project ID for you.
[15:54-15:59] So it's recommended that we create a new project for this lab.
[15:59-16:02] But if you want to reuse some existing project,
[16:02-16:05] you can type an existing project ID to use.
[16:05-16:07] That's also feasible.
[16:07-16:09] So what I do is I just press enter.
[16:09-16:11] I'm not entering a one or two.
[16:11-16:12] I just press enter.
[16:12-16:15] And it will default using this new project.
[16:15-16:16] So what we're just behind the scene
[16:16-16:19] is creating this new project for me.
[16:19-16:22] And it will automatically link the billing account
[16:22-16:25] I just claimed to this new project.
[16:25-16:28] And also it's installing some dependency
[16:28-16:30] to set up the environment.
[16:30-16:32] And now you can see this yellow thing over here.
[16:32-16:35] That means I successfully point to the new project
[16:35-16:37] I'm creating and the whole environment
[16:37-16:38] explicitly set up.
[16:39-16:39] Great.
[16:40-16:43] So next step is making sure we can fix
[16:43-16:44] set the project ID.
[16:44-16:47] Actually in the step I already set the project ID.
[16:47-16:50] I'm just do the step to double check.
[16:51-16:54] And then what's next is we need to enable the required API.
[16:54-16:57] Just copy paste to enable the required API.
[16:58-17:01] And over here you can see that we want to enable
[17:01-17:05] some API platform and cloud build.
[17:05-17:07] Because later on we might want to deploy
[17:07-17:09] the whole thing to Cloud Run.
[17:09-17:11] Because we might want to build the Docker.
[17:11-17:14] So we want to have enabled the artifact registry.
[17:14-17:16] And here we're using a graph database.
[17:16-17:18] So here we're using Spanner.
[17:18-17:19] So you want to enable Spanner.
[17:20-17:23] And later on we want to enable the multimodal inputs
[17:23-17:25] so you want to have the storage API.
[17:25-17:29] So those are just the easy way for you to enable some API.
[17:29-17:32] Of course you can also enable them in the Google Cloud Console.
[17:32-17:35] But this is just some command line for you
[17:35-17:37] to easily enable them.
[17:37-17:39] And next let's run the set up script.
[17:40-17:41] Oh I'm still waiting for it.
[17:41-17:44] So while I'm waiting for this enabling
[17:44-17:49] I can talk a little bit
[17:49-17:51] we're going to build by the end of the lab.
[17:51-17:53] And this is actually part of the workshop.
[17:53-17:57] So if you follow the level 0 to level 5
[17:57-17:58] you will actually see yourself.
[17:58-18:00] You will create an icon of yourself.
[18:00-18:02] And you see yourself on the planet.
[18:02-18:06] So the thing for this workshop is you're in the universe.
[18:06-18:07] You're on the planet.
[18:07-18:09] And you want to find your way back home.
[18:10-18:13] And on this planet because you want to find
[18:13-18:18] your way back to earth you're trying to survive on this planet.
[18:18-18:19] So there is a relationship between the people
[18:20-18:23] who are among people on this planet.
[18:23-18:26] Some people have the skills maybe they have medical skills.
[18:26-18:28] Some other people maybe they got injured.
[18:29-18:32] So therefore some people they have the medical skill
[18:32-18:35] can treat the people who got injured.
[18:35-18:37] Right so there is a potential relationship between
[18:37-18:41] so my name is Annie and this is what I'm good at.
[18:41-18:44] But this is the resource I have but I also need something.
[18:44-18:48] And maybe if I know how to maybe if I have some medical skills
[18:48-18:50] and some announced need some treatment
[18:50-18:52] so maybe I can help them right.
[18:52-18:54] So there's a relationship on it.
[18:54-18:58] That's exactly how what is the graph knowledge base
[18:58-19:00] we are trying to build later on.
[19:00-19:02] So that's a context for this lab.
[19:02-19:07] All right so I'm going back to this ID
[19:07-19:11] and you can see that I successfully enable all this API.
[19:11-19:14] So what's next is I want to run the set up script.
[19:15-19:18] Just copy this and paste to the terminal.
[19:18-19:20] And here what it does behind the scene is
[19:20-19:23] it's trying to grab in all those environment variable
[19:23-19:26] and create a dot in refile for me
[19:26-19:29] and put all the value to the dot in refile.
[19:29-19:32] And here you can see there's a dot in refile on to level two.
[19:32-19:34] So I'm clicking dot in refile.
[19:34-19:37] I can see all those value is grabbing for me.
[19:37-19:42] And I have all my environments set up automatically for me.
[19:42-19:42] Cool.
[19:42-19:46] And what's next is we want to load the sample data
[19:46-19:49] by first install the dependency.
[19:49-19:52] We copy this and we paste over here.
[19:53-19:57] So here we're using UV to do all the environments control.
[19:57-19:59] So in the backend folder over here
[19:59-20:04] if we go to the P by project tome file
[20:04-20:06] you can see those are the dependency we have.
[20:06-20:10] So by doing UV sync we can install all this dependency.
[20:10-20:14] And what's next is I want to load all the initial survival data.
[20:15-20:18] So I'm copy this and paste over here.
[20:18-20:21] So the data we are trying to load over here
[20:21-20:25] is exactly the relationship we were talking about earlier.
[20:25-20:29] So we have some people are good at medical skills.
[20:29-20:30] Some people need injured.
[20:30-20:33] So they may have the one people's skill
[20:33-20:35] may be helpful to another people's needs.
[20:35-20:37] So there's a match between them.
[20:37-20:37] Right.
[20:37-20:39] So therefore we have a graph relations.
[20:40-20:45] We can have a graph database to hold most host data over here.
[20:45-20:47] And go back to the thing.
[20:48-20:50] As I mentioned before this is a workshop thing
[20:50-20:53] and we have a survival network challenge.
[20:53-20:56] To summarize the challenge we have is on social data.
[20:56-21:01] Like maybe people are uploading photo text message or videos.
[21:01-21:02] And we have complex relationship here
[21:02-21:05] because we need to know who has the skills,
[21:05-21:07] who need help and where are they.
[21:07-21:09] And then we need to make time critical decision
[21:09-21:12] that we want to match the helpers in real time.
[21:13-21:15] And traditionally to handle multimodal data
[21:15-21:18] we might have separate pipeline
[21:18-21:21] and to search who can help whom
[21:21-21:22] we might do the keyword search.
[21:22-21:25] But the problem is if you search like magic
[21:25-21:29] if the keyword does not exactly match medical training
[21:29-21:32] you might not able to find the person who has a medical skill.
[21:32-21:34] So that could be a problem.
[21:34-21:38] And relationship wise if you're not using graph database
[21:38-21:41] if you're using relational database like using table
[21:41-21:43] you might have to join the query.
[21:43-21:45] So it can be complex and slow.
[21:45-21:47] And lastly we talk about personalization.
[21:48-21:51] Yeah so this is for the whole lab but for this video
[21:51-21:54] we're only going to talk about the symmetric search and relationship.
[21:55-21:58] But for the next video we're going to talk about multimodal handling
[21:58-21:59] and personalization.
[21:59-22:00] So stay tuned.
[22:01-22:02] All right.
[22:02-22:05] And so the solution for the challenge is
[22:05-22:07] to capture the multimodal processing
[22:07-22:12] we were building multimodal multi-agent system to capture
[22:12-22:14] and to help quickly find the search
[22:14-22:17] like for the helper we're using graph rack.
[22:17-22:21] So we're going to cover what is graph rack and why graph rack.
[22:21-22:24] We're also going to cover different type of search in this lab.
[22:25-22:28] And then we're using Google agent development kit.
[22:28-22:29] To orchestrate the whole thing
[22:29-22:34] orchestrate the multi agent for multimodal processing
[22:34-22:37] and orchestrate the agent with the graph rack agent
[22:37-22:40] and also multimodal processing agent.
[22:40-22:44] And lastly we have the memory band for the member part.
[22:44-22:46] Again we're going to cover this in the next video.
[22:46-22:49] So here we're using Google standard DB
[22:49-22:52] to contain this graph knowledge.
[22:53-22:56] Traditionally you might be using post-graphs and Neo4j
[22:56-22:59] but with Spanner we only have one unified database
[22:59-23:01] so that you have single source of truth
[23:01-23:03] and you don't have to deal with the data
[23:03-23:06] sink delay a lot of benefit of using Spanner.
[23:07-23:10] And let's get to see what does Spanner look like.
[23:10-23:14] So once you successfully run this command
[23:14-23:17] that is setup data.py zone
[23:17-23:20] you will see that all database setup complete.
[23:20-23:20] Right.
[23:20-23:21] So just over here.
[23:21-23:24] So here you can access the database at this link.
[23:24-23:25] So just copy this link.
[23:25-23:26] Click into this link
[23:26-23:32] and you can see we are into Google Cloud Console Spanner
[23:32-23:36] over here and we already load all the data for you
[23:37-23:39] and congratulations you just finished the step.
[23:41-23:42] And let's go to step four.
[23:45-23:49] How to visualize graph data in Spanner Studio.
[23:49-23:52] And to follow the step we go to the Spanner DB
[23:53-23:56] like Spanner DB Google Cloud Console
[23:56-23:58] and at this step Spanner Studio
[23:58-24:00] you click in this you can see we have also table
[24:01-24:02] it's available for you.
[24:03-24:06] And then over here we have the query input
[24:06-24:09] so we can type anything over here
[24:09-24:12] and just do a real life a real time change
[24:12-24:13] real time check.
[24:13-24:15] So here firstly we want to understand
[24:15-24:18] who are there in this knowledge database.
[24:18-24:20] We talk about we have different survival on the planet
[24:20-24:23] but who are there and who is there.
[24:23-24:25] Which part of the planet there are.
[24:25-24:30] So here I'm copy this query just to get a sense of
[24:30-24:31] what is the relationship over here.
[24:31-24:34] So I'm copy this around the query
[24:34-24:36] and I can immediately see the result over here.
[24:36-24:39] And here is a graph that showcases the relationship.
[24:40-24:42] If you hover on the blue note
[24:42-24:44] then here you can see the survival
[24:44-24:48] and the red note is you can see where are they.
[24:49-24:52] So here by running this query over here
[24:52-24:54] you can just directly see all the relationship.
[24:55-24:56] It's pretty cool right.
[24:57-25:00] And what's next is now you understand
[25:00-25:03] that we have full survival over here.
[25:03-25:05] And what's next is we want to understand
[25:05-25:07] what are the skills they have
[25:07-25:09] so that later on you can search the skill
[25:09-25:11] and you'll find a match for the helper right.
[25:12-25:13] So I'm copy this command
[25:13-25:16] and then paste it over here and run it again.
[25:16-25:19] Now I can see the relationship is the survival
[25:19-25:21] and their skills.
[25:21-25:24] So here I have the survival and the skills.
[25:24-25:25] Cool.
[25:25-25:28] So also we have some explanation in this lab.
[25:28-25:30] Again on the screen top right
[25:30-25:33] you have this link about this lab
[25:33-25:35] so that if you open the link
[25:35-25:38] you can read through the explanation
[25:38-25:41] and go through the lab together with this video.
[25:41-25:42] Cool.
[25:42-25:44] So now we understand we have full survival
[25:44-25:46] and they're on a different part of the planet
[25:46-25:48] and they have different skills.
[25:48-25:50] So here we need to understand
[25:50-25:52] what do they need.
[25:52-25:53] And I copy this query.
[25:53-25:57] Again I go to the cloud council at Spanner studio.
[25:57-26:00] Again I'm going to paste this query over here
[26:01-26:04] and I run them to see what are the need.
[26:04-26:07] Again the blue note is a survival.
[26:07-26:10] Click to the survival and the red note is a need.
[26:10-26:14] Apparently this survival they need medical treatment.
[26:14-26:17] And lastly we can see who can help whom.
[26:18-26:21] I copy this paste over here
[26:21-26:23] and I can see wow I have
[26:23-26:24] some existing match.
[26:25-26:29] So this person whose name is Alina Frost
[26:29-26:31] and he has a medical skill
[26:31-26:32] and he has a science skill.
[26:33-26:35] And with this medical skill
[26:35-26:38] you can see it's matching those person.
[26:38-26:42] This survival captain Yuki need medical treatment.
[26:42-26:45] So therefore Alina's medical skill
[26:45-26:49] can potentially help Yuki's medical need.
[26:49-26:53] So we already have some match over here.
[26:54-26:58] So here we can already traverse this graph
[26:58-27:02] to understand some relationship and potential match.
[27:02-27:04] But as you can see
[27:04-27:09] there possibly could have more match in this graph
[27:09-27:11] that later on we're going to explain
[27:11-27:14] how to search them effectively.
[27:14-27:15] Cool.
[27:15-27:18] So now you successfully finish step four
[27:18-27:21] and what we did so far is
[27:21-27:24] we are successfully loading this data in SpinalDB
[27:24-27:28] and we play around this relationship in the studio
[27:28-27:31] so that we can visualize the graph here
[27:31-27:34] so that we better understanding what's going on over here.
[27:34-27:36] We're understanding the relationship
[27:36-27:39] of what survival have, where they are,
[27:39-27:42] what skill they have, and what the results they have,
[27:42-27:47] what they need and potential and existing match over here.
[27:47-27:49] And we can visualize them like this.
[27:49-27:50] Pretty cool.
[27:50-27:53] We can visualize them as a notch and edge over here
[27:53-27:55] in this Spinal Studio.
[27:57-28:00] So what's next is let's start with the AI
[28:00-28:03] empowered embedding in SpinalDB.
[28:04-28:07] So let's take a look at this diagram on the screen.
[28:08-28:11] So a lot of things going on on the screen.
[28:11-28:15] So let's take a look from bottom and over the way up.
[28:16-28:19] At the very bottom, most importantly,
[28:19-28:21] we're creating this text embedding model
[28:21-28:23] and jump-net-prone model in Spanner.
[28:24-28:26] And then we have the service layer.
[28:27-28:31] Basically, we are using the model we're creating over here
[28:31-28:35] and implement the logic in the service
[28:35-28:38] so that we can do rack search, keyword search,
[28:38-28:40] hybrid search, and analyze query.
[28:40-28:43] And once we have the service layer,
[28:43-28:45] like service logic implemented,
[28:45-28:49] we can directly use them in the tool layer
[28:49-28:52] to building the tools for our agent.
[28:52-28:55] So here we can build in the semantic search tool,
[28:55-28:57] keyword search tool, and hybrid search tool.
[28:58-29:00] Later we're going to explain what exactly is hybrid search.
[29:02-29:05] And lastly, we're going to use those tools in the agent,
[29:05-29:07] like our root agent over here.
[29:07-29:10] Here we're using ADK, Google agent development kit
[29:10-29:12] to build agent over here.
[29:12-29:14] Just a quick recap, what is agent?
[29:14-29:19] So agents usually have the model as a brain to choose tools
[29:19-29:21] and then use tools to make decisions
[29:21-29:24] and resolve some problems for the user.
[29:24-29:27] And here we're building the tools like semantic search tool,
[29:27-29:29] keyword search tool, and hybrid search tool
[29:29-29:30] for this root agent.
[29:30-29:33] And here are all the logic over here,
[29:33-29:36] all the way down here to building this agent.
[29:38-29:41] And you may wonder why we are creating
[29:41-29:45] the model in Spanner, not directly using the model
[29:45-29:48] in the Python code in service layer.
[29:48-29:49] Because we could potentially just directly using
[29:49-29:52] what has a model in service layer.
[29:52-29:55] Why we are creating this model in Spanner?
[29:56-30:01] So the answer is it's quick and cleaner this way
[30:01-30:05] because here we are directly creating the embedding
[30:06-30:08] for those data in the database.
[30:08-30:12] So we are using the job model to directly analyze the data.
[30:12-30:17] So it will be quicker and cost less
[30:17-30:19] if you're directly using the model in Spanner
[30:19-30:23] versus you're using the model in the service code.
[30:23-30:25] Because in the service code, if you're using the model,
[30:25-30:28] you have to talk to the database and grab the data
[30:28-30:31] and then talk to using the one who has an AI model
[30:31-30:33] with the prompt and get a response back.
[30:33-30:35] So it's additional loop over there.
[30:36-30:42] And the question now becomes how we are going to use
[30:42-30:45] creating the model in the Spanner studio directly.
[30:45-30:49] And here we are using something called ML predict.
[30:49-30:52] So Spanner's ML predict let you to generate the embedding
[30:52-30:54] directly in SQL.
[30:54-30:57] And it can store vector alongside graph data
[30:57-30:59] and also perform semantic search.
[31:00-31:04] But it's not creating a real model in Spanner.
[31:04-31:06] It's creating the virtual model.
[31:06-31:08] So it's just a reference.
[31:08-31:10] We don't have to store model weights.
[31:10-31:12] And here's a diagram that you can reference.
[31:13-31:17] So we can use ML predict directly in the Spanner.
[31:17-31:21] So here we are using, we have this input first add
[31:21-31:23] to what has an embedding model
[31:23-31:27] and get this embedding back to the Spanner.
[31:27-31:28] And then we can calculate it.
[31:29-31:32] So for those of you who don't know what is embedding
[31:32-31:35] and what is RAC to quickly go through them
[31:35-31:38] is retrieval augmented generation.
[31:38-31:44] And retrieval is you, so the problem RAC trying to solve is
[31:44-31:48] if you directly use it may not have the personalized
[31:48-31:50] knowledge base for your question.
[31:50-31:53] So here you may want to use additional database,
[31:53-31:57] a personalized database, so that if you link your system
[31:57-32:00] to that personalized database, you can do retrieval
[32:00-32:01] from the database.
[32:01-32:04] And then you retrieve the answer from the database
[32:04-32:08] and then you augment to your existing answer for the final
[32:08-32:10] and then based on that you can generate the final response
[32:10-32:11] back to the user.
[32:11-32:14] So basically you're adding additional knowledge base
[32:14-32:20] to your AI system to make it understand more specialized data
[32:20-32:25] to have more accurate answer and to eliminate hallucination.
[32:26-32:28] So that is usually what we talk about.
[32:29-32:33] Retrieval augmented generation and the very important part
[32:33-32:37] for retrieval augmented generation is usually we want
[32:37-32:39] to generate embedding to do the retrieval.
[32:40-32:43] What does that mean is we want to have the embedding
[32:43-32:47] like a numeric representation of the item we want to search for.
[32:48-32:52] And then for the database we want to have an embedding space
[32:52-32:54] so that everything in that database we want to have
[32:54-32:57] embedding representation for all of them.
[32:58-33:01] So embedding by numeric representation of them.
[33:01-33:05] So we do the search, you're trying to see this like this
[33:05-33:07] mathematic representation is embedding.
[33:07-33:10] How close does this item I'm trying to search
[33:11-33:13] to this embedding space?
[33:13-33:16] So if they're very close, that means they're very similar.
[33:16-33:20] If they're not very close, that means they're not very similar.
[33:20-33:26] So that is the quick overview of what is embedding
[33:26-33:31] and what is embedding and why we-want to create an embedding here.
[33:31-33:33] And just go back to today's lab.
[33:33-33:36] We're using embedding, we're creating the embedding model
[33:36-33:40] directly in SpannerDB with ML predicts.
[33:40-33:44] And ML predict can create a virtual model in Spanner.
[33:44-33:46] It's very quick and very clean.
[33:46-33:50] So here a lot of talking and let's get on continue the lab.
[33:51-33:54] So what we want to do is we want to create a text embedding
[33:54-33:55] for the things we are trying to search.
[33:56-34:00] So we want to have the embedding model first.
[34:01-34:05] And then we can use this embedding model to convert things to the embedding
[34:05-34:07] and then we are doing the semantic search.
[34:07-34:10] And now I'm copy this and to the embedding.
[34:10-34:13] So here we are pasted over here.
[34:14-34:17] And here's a very important thing is you need to replace the project ID
[34:17-34:19] to the real project ID.
[34:19-34:24] So what I do over here is I'm going to .env file
[34:24-34:30] and then copy this project ID and then I'm going to paste it over here.
[34:30-34:32] So this is how you do it.
[34:32-34:36] And if you forget to paste it and you just happened to click run,
[34:37-34:40] you may have to, if you forget to replace it,
[34:40-34:43] you may have to do drop model, texting embedding,
[34:43-34:45] and then you redo it.
[34:45-34:46] Because if you don't drop it,
[34:46-34:49] you may not be able to create the model again.
[34:50-34:53] So let's go back to the studio and click the run.
[34:54-34:57] So here we want to create a model called texting embedding.
[34:57-34:58] Great.
[34:58-35:00] It says successfully created.
[35:00-35:04] If you click it again, it says it failed because it's duplicated.
[35:04-35:06] So that means it's already created before.
[35:07-35:08] Cool.
[35:08-35:12] So if you click twice, if you see the fail, that's expected
[35:12-35:14] because you already created it already.
[35:14-35:16] And what's next is we want to add an embedding column.
[35:16-35:20] So we are copy this and we're going to paste it over here.
[35:20-35:22] And click run.
[35:22-35:25] And here we successfully create a skills table.
[35:25-35:30] So what we want to do is we want to search skills
[35:30-35:32] and we want to create embedding space.
[35:32-35:35] So basically we want to convert everything in the skill table
[35:35-35:37] to skill embedding.
[35:37-35:38] And this is how we're going to do it
[35:38-35:40] because we already have the model.
[35:40-35:42] And we can just creating,
[35:42-35:44] we can create a text embedding for all the skill
[35:44-35:46] in the skills table.
[35:46-35:48] So here we have 10 rule updated.
[35:48-35:51] So basically we update them to be embedding
[35:51-35:55] so that we can use semantic search over here.
[35:55-35:56] Again, if you see the permission error,
[35:56-35:59] you might have to redo the previous step
[35:59-36:02] to drop the model and then re-creating the model text
[36:02-36:04] embedding with the correct project ID.
[36:04-36:06] And now let's verify embedding.
[36:06-36:10] Like copy this and then go back to the vendor studio
[36:10-36:11] and we're going to paste it.
[36:12-36:13] Cool.
[36:13-36:17] So you can see that we can see all the skills available
[36:17-36:19] over here with the embedding.
[36:19-36:24] We have the embedding dimension over here is 768.
[36:24-36:27] That means we're using 768 dimension
[36:27-36:30] to describe the skill over here.
[36:31-36:34] So that means we are successfully
[36:34-36:38] convert all the skills to embedding in this embedding space.
[36:38-36:38] Great.
[36:38-36:42] So last thing is we want to test the semantic search.
[36:42-36:45] So just copy here and paste and just run.
[36:46-36:50] And you can see we successfully do the semantic search.
[36:50-36:53] What we're trying to search is we're trying to search magic.
[36:54-36:57] As you can see when we search magic, it's not medical.
[36:58-37:00] It's if you use a keyword search,
[37:00-37:02] you may not able to find a result
[37:02-37:05] for those things that are similar to the meaning of magic.
[37:06-37:09] Then because you're converting them to embedding
[37:09-37:13] and here you actually get the meaning of magic.
[37:13-37:16] And then you're searching in the skill table,
[37:16-37:17] you're just like a skill.
[37:17-37:21] You're searching this embedding representation of skills.
[37:21-37:24] So here you're searching the embedding space
[37:24-37:28] and you're trying to find how close they are with the call sign.
[37:28-37:31] We're using the call sign to calculate the distance.
[37:31-37:34] So basically the smaller the distance they are,
[37:35-37:37] that means the similar there.
[37:37-37:40] And here you can see the medical training
[37:40-37:42] is actually the most similar to magic.
[37:42-37:47] And leadership probably not as similar to magic as a medical training.
[37:47-37:49] So here we are ranking them by the distance.
[37:49-37:53] And this is exactly where we're called semantic search earlier.
[37:53-37:55] And this is for when we do the retrieval.
[37:55-37:58] This is how we want to retrieve things.
[37:58-37:58] Cool.
[37:58-38:02] That means we have successfully do the semantic search over here.
[38:02-38:06] What's next is we want to create a gemnet model to analyzing.
[38:06-38:08] And the gemnet model we are going to use
[38:08-38:12] in gemnet model directly in Spanner Studio, a Spanner as well.
[38:12-38:14] We are just like what we said earlier,
[38:14-38:16] we want to use in gemnet pro model over here.
[38:17-38:19] So similarly we're using ML create a predict
[38:19-38:22] to directly using the gemnet model.
[38:22-38:23] And this is what we want to do.
[38:23-38:26] We want to copy this and paste it.
[38:26-38:31] So here I did the wrong because I didn't replace the project ID.
[38:31-38:36] So what I want to do here is I want to draw this model first
[38:36-38:37] and then run it to drop this
[38:37-38:41] and now I want to recreate this with the correct project ID.
[38:41-38:44] So here I need to go to the editor
[38:44-38:46] and here I have this project ID.
[38:46-38:51] Just copy this and then paste over here so that you can run them.
[38:52-38:57] And here I successfully create a correct gemnet pro model.
[38:57-38:59] And what's next is I want to use this gemnet
[38:59-39:02] to analyze and generate these.
[39:03-39:07] So I'm copy this and paste over here.
[39:07-39:09] Let's take a look at what this query does.
[39:10-39:13] So here I'm actually sending this prompt
[39:13-39:15] to the gemnet pro over there.
[39:17-39:21] So this prompt is I want to access those two survival
[39:21-39:23] and this is a survival name.
[39:23-39:26] And I want to generate a score from one to 10
[39:26-39:28] and one sentence reason.
[39:28-39:31] So I directly sending this prompt
[39:31-39:33] to what has AI model over there
[39:33-39:35] like this gemnet pro model over there.
[39:36-39:38] And with this question and generate this answer says
[39:38-39:44] oh I'm generating this score nine over 10 and with this reason.
[39:44-39:47] So that means you're successfully using the gemnet pro model.
[39:47-39:50] Again you can see if you have the syntax error message
[39:50-39:53] you can ignore them because the result here is correct.
[39:54-39:58] Cool. So at this step that means you have successfully
[39:58-40:00] creating the model creating the embedding.
[40:01-40:05] Just to recap what we did before we create this text embedding model.
[40:06-40:09] We also create this gemnet pro model in Spanner.
[40:09-40:13] And you also did is you're using this text embedding model
[40:13-40:17] and try the semantic search in Spanner
[40:17-40:21] because you're converting the skill to embedding space.
[40:21-40:26] And then we try to search magic in the skill embedding space
[40:26-40:30] and we can rank the result by the distance for the embedding
[40:30-40:34] and then we can rank how similar they are to the things we're trying to create.
[40:34-40:37] So that's what we just did for that step.
[40:37-40:40] And congratulations for those who have finishing that step.
[40:41-40:46] And the next step is now we are having this model in Spanner
[40:46-40:50] and we also get a taste of the semantic search in SpannerDB
[40:50-40:54] and what's next is we want to directly use them
[40:54-40:58] in the service layer so that we can implement the service layer logic
[40:58-41:03] and later on we can connect the agent to the service logic.
[41:03-41:06] So here I'm going to step six graph rack.
[41:09-41:12] So in this step what we're trying to do is we are trying to
[41:13-41:18] implementing the semantic search logic all the way
[41:18-41:22] from service layer to the tooling layer to the agent layer.
[41:22-41:26] And here we are using ADK agent development kit for the agent.
[41:27-41:32] So if you don't know what is ADK, I will do ADK doc Google search.
[41:32-41:36] And on the first result, here is the ADK doc page.
[41:36-41:40] And here I can learn everything about ADK doc.
[41:40-41:43] You can get started with ADK and build your agent.
[41:43-41:46] So I will go to the agent tab and try to understanding
[41:46-41:51] those are different types of agent and just get familiar with this framework.
[41:52-41:59] So let's go back and try to implement our semantic search in the graph rack agent.
[41:59-42:03] Excited? So now you're actually building a graph rack agent over here.
[42:04-42:09] Cool. Let's copy this to the terminal and paste it over here.
[42:09-42:14] So this step is basically opening this file for me in the editor.
[42:14-42:16] And here I'm opening this service folder.
[42:16-42:20] So I'm opening I'm trying to do the implementation in the service layer.
[42:20-42:25] And what I want to do is I just need to copy paste the important logic.
[42:25-42:29] So I'm searching this to do replace the code.
[42:29-42:31] And I'm going to paste the whole thing.
[42:31-42:36] And I need to replace the whole line by a triple tap this.
[42:37-42:42] So it's selecting the whole line and I paste it so that the indentation is correct.
[42:43-42:47] And let's take a look at what they're pasting over here.
[42:48-42:54] So here we actually is very similar to the query we just run in the Spanner Studio, right?
[42:54-42:59] Because we're using the text embedding model we created in the Spanner.
[42:59-43:04] And we're trying to find the cosine distance for the skill embedding space.
[43:05-43:09] But you can see that we actually have more things over here.
[43:09-43:12] We actually have the drawing table over here.
[43:12-43:13] And what does that mean?
[43:13-43:18] So here is what we call graph rag kicking.
[43:18-43:20] And let's take a look at this diagram.
[43:20-43:26] So this is the overview of what we're trying to do, like the graph rag process.
[43:26-43:31] So in our example, we're trying to find magic for burning victim.
[43:31-43:34] So we're searching magic for burning victim.
[43:34-43:37] And then I'm trying to see who can help magic, right?
[43:38-43:42] So here we have this embedding model created in Spanner Studio.
[43:42-43:48] So what we did first is we're creating this embedding of this magic so that we have this
[43:48-43:52] new magic representation of magic, right?
[43:52-43:57] So next is we're trying to search in that embedding space and find the things that
[43:58-44:00] physically close to magic.
[44:01-44:08] And the important of graph rag, the difference between graph rag versus traditional
[44:08-44:15] rag is we actually do this LM context in the graph context so that you can traverse
[44:15-44:18] this graph to understand more information.
[44:18-44:23] So you're not only understanding what is the skill that's similar to magic.
[44:23-44:27] Previously, we get medical training that's similar to magic.
[44:27-44:33] You also get the corresponding relationship of we can traverse this graph to understand
[44:33-44:36] what are the relationship connecting to the skill.
[44:36-44:42] Who has this doctor's thought has the skill of medical training so that it's able to understand
[44:42-44:49] we traverse the graph and get more content for this curious so that you can give more
[44:50-44:52] related funds to your question.
[44:52-44:54] And this is really powerful.
[44:54-44:58] And our code is we are trying to join this table.
[44:58-45:05] It's basically how we want to traverse the graph node to get more related information over here.
[45:05-45:10] And if you're curious, you can read more explanation over here in this lab.
[45:10-45:16] Again, the lab is on the top right of our window.
[45:16-45:18] Now let's continue to building the tool.
[45:18-45:21] So what we did before is we're creating the service layer.
[45:21-45:25] Now we want to connecting the tool layer to the service layer.
[45:25-45:29] And again, we're just only working on the semantic search.
[45:29-45:31] So I'm copying this paste.
[45:31-45:33] So I'm opening the tool file.
[45:33-45:36] And over here, I'm locating the comment.
[45:36-45:37] I'm going to paste it over here.
[45:38-45:42] And I'm going to triple tap and select in the whole line.
[45:42-45:49] And I'm copy this and I'm pasting this so that I'm creating this tool cosmetic search.
[45:50-45:57] And over here, I'm using the logic that I implemented in the service layer.
[45:57-46:01] Again, if you're curious about the source code and you want to understand
[46:01-46:09] any more about the logic, I recommend you to go to the top right link and open this lab.
[46:09-46:17] And you will see the source code over here to understand more about the detailed logic behind the scene.
[46:17-46:18] Let's continue.
[46:18-46:24] So now we have the tool and we want to connect in the tool to the ADK agent.
[46:24-46:29] So here the, I think a basic agent code.
[46:29-46:36] So here is a basic agent code over here is with ADK, you just need to using the agent library and
[46:36-46:41] define what model you're using, what is the description and then adding the tools over here.
[46:41-46:45] You're supporting Python, TypeScript, Go, and Java.
[46:45-46:50] And I'm copying this to do and replacing, oh, I skipped a step.
[46:50-46:53] I need to go to the agent file first.
[46:53-46:57] So I have the agent file and I'm searching this.
[46:57-47:01] So here I am copying this to the prompt.
[47:01-47:08] So what I'm trying to do is I'm adding this semantic search logic in the agent instruction
[47:08-47:13] so that in the agent instruction it knows when to do the semantic search.
[47:13-47:14] Cool.
[47:14-47:16] And lastly, we need to add the tools.
[47:16-47:19] We're just creating, we're connecting that to the agent.
[47:19-47:25] So the agent, the brain, model as a brain to select the tools we're providing to the agent.
[47:25-47:33] So what we want to do is again, we want to search this in the pasted and just paste.
[47:33-47:34] And here we go.
[47:34-47:38] We're connecting, we're adding these tools to the agent.
[47:38-47:39] And now congratulations.
[47:39-47:43] You're just successfully building a graph rack agent.
[47:43-47:47] And now you may say that, oh, here is some reading for you,
[47:47-47:49] understanding how the hyper-research work.
[47:50-47:55] So what we did before is we are implementing semantic search for rack agent.
[47:55-48:00] So semantic search is we're getting the embedding and we're trying to find things that are actually
[48:01-48:04] similar to the meaning of the things we're trying to search.
[48:04-48:08] So the keyword search is we're searching the exact text matching word.
[48:08-48:12] And semantic search is we're trying to find things that are similar.
[48:12-48:15] But what if we want to search medical skills in mountain?
[48:15-48:18] We want to find things, we want to search for things that are similar
[48:18-48:20] to medical skills.
[48:20-48:23] But also we want to have the exact keyword search for mountain.
[48:24-48:26] So here, what if I care both?
[48:27-48:28] How do you do the search?
[48:28-48:33] And here we are introducing this hyper-search with the RF algorithm
[48:34-48:38] so that we can combine, do the fusion for both type of search.
[48:39-48:41] And this is the algorithm behind the scene.
[48:41-48:44] As a keyword search, we have this ranking.
[48:44-48:47] And with the semantic search, we have another ranking.
[48:47-48:51] And then we're using this RF scrolling algorithm to calculate a new score.
[48:51-48:53] And then we get this new ranking.
[48:53-49:00] And then we find the result that's a good combination for the two type of the search.
[49:01-49:06] And if you're curious about exact logic, you can go to this file.
[49:06-49:09] And then the hyper-search, when the hyper-search is caught,
[49:09-49:13] we are implementing this logic over there to calculate the ranking.
[49:14-49:18] And those are the some readings for you that if you're
[49:18-49:21] curious about when to use what kind of search, cool.
[49:21-49:25] So just to summarize what we've done so far.
[49:25-49:30] So to summarize what we've done so far is we're creating the embedding model
[49:30-49:33] and John Nipro model in Spanner.
[49:33-49:37] And we're implementing the related logic in the service layer.
[49:37-49:40] And then we're connecting the service layer, the semantic search logic
[49:40-49:43] to the semantic search tool.
[49:43-49:47] And then we are using this tool all the way in the ADK agent.
[49:47-49:52] So here we are creating the graph-rack agent with semantic search.
[49:52-49:57] We're also understanding what is the difference between the graph-rack search
[49:57-50:00] versus the traditional pure-rack search.
[50:00-50:06] We're also understanding hyper-search with a new algorithm like RF algorithm
[50:06-50:10] so that we can combine the result for the keyword search and also semantic search.
[50:10-50:14] And what's next is we want to test our agent with ADKBAP.
[50:17-50:22] And to do the test, we just first copy this and then gonna paste it to the terminal.
[50:22-50:25] So if you take a look at this command we're typing,
[50:25-50:27] what we actually care is ADKBAP.
[50:27-50:32] So ADKBAP is a command to open the ADKBAP UI
[50:32-50:36] that we can directly interact and troubleshooting
[50:36-50:39] and have the possibility for the agent we're creating.
[50:40-50:44] If you want to learn more about the ADKBAP,
[50:44-50:50] you can find more with the ADKBAP doc in this link over here.
[50:50-50:55] You can see how to use the ADKBAP in a different way to start ADKBAP
[50:55-50:58] with different language over here and more.
[50:58-51:02] So now if you're doing ADKBAP, we're just clicking on this link
[51:02-51:05] so that we're open up this ADKBAP.
[51:05-51:09] And on the top left, you can select the agent we're creating
[51:09-51:12] and you can ask him some questions.
[51:12-51:15] For example, who can help with injuries?
[51:15-51:19] And according to this, we're expecting it to using Semantic Search
[51:19-51:24] to find the person who has the medical skills to help with injury.
[51:24-51:26] So here you can see I can help with the...
[51:27-51:29] We can try to use Semantic Search if you have on it.
[51:30-51:34] You can see those are other tools that connect into the agent.
[51:35-51:38] And this is the result for using these tools.
[51:39-51:43] And this is finally LLM Generators.
[51:43-51:47] Say, oh, so we have David Chen has this first ad
[51:47-51:50] and we have Dr. Elena has the medical training and more.
[51:51-51:52] Pretty cool.
[51:52-51:57] So you can see the tracing over here by when it is executing the tool.
[51:57-52:00] So you can see it's not the time we're executing the tool.
[52:01-52:06] And how long the latency, how long the duration for me to calling LLM.
[52:07-52:11] So this is a really cool way for us to do the troubleshooting.
[52:11-52:14] Once we finish all the testing, we're going to do the control C
[52:14-52:18] to end the process so that we can continue more testing.
[52:21-52:24] So the next step is we want to run the full application.
[52:24-52:28] Remember the cool UI we had earlier, like this cool UI.
[52:28-52:33] So to do that, we want to actually run the full application.
[52:33-52:38] So what we did earlier is we're creating the root agent
[52:38-52:39] and then we're connecting it to the tools.
[52:40-52:44] So now we want to connect the backend to the frontend.
[52:44-52:48] And in this case, we have the frontend, the browser and the react component.
[52:48-52:51] So the backend, we have the ADK agent.
[52:51-52:58] And then we're using fast API for the API layer in the file called chat.pyzone
[52:58-53:02] at the router in today's in this lab setup.
[53:02-53:06] So here's our important concept over here for us to understand
[53:06-53:09] how exactly we're connecting frontend and backend.
[53:10-53:15] And here's the concept of runner and session service and memory service.
[53:16-53:20] So runner basically a power up agent.
[53:21-53:26] So for agent, we have model as a brain to choose the tools we want.
[53:27-53:32] And each time when we model is making a decision to choose a certain tool,
[53:32-53:35] or we're using this model, they're all different events.
[53:35-53:42] And for those events to continue, we need an agent to power up them to have this event loop.
[53:43-53:47] So that is where a runner play the role.
[53:47-53:51] So we have this runner to power things up to grab this event.
[53:51-53:55] So that in this API service, in this API layer,
[53:55-53:59] we're going to pass the input from the frontend UI.
[53:59-54:02] And then we're going to through this runner power the event.
[54:02-54:04] We're going to send it to the agent.
[54:04-54:06] And then finally, we get the final response.
[54:06-54:11] We're going to power, we're going to pass the response from the final response for the agent
[54:11-54:13] and send it back to the frontend UI.
[54:14-54:17] We also have session service and memory service.
[54:18-54:23] So those basically contain the conversation history we have with agent.
[54:23-54:27] So whatever you're talking to the agent, you talk to agent say,
[54:27-54:30] do this search or who has this medical skill.
[54:30-54:33] You ask information about this relationship,
[54:33-54:36] about to understand more about this knowledge database,
[54:36-54:41] all the conversation you have with agent is stored in the session service and memory service.
[54:43-54:45] So now we are at try.pysonfile.
[54:46-54:52] And then what we do is we copy this to you and we're going to paste it over here.
[54:52-54:56] As you can see, this step is we're creating the session series,
[54:56-54:59] the memory series, so that it can store the conversation.
[54:59-55:01] We have this agent.
[55:02-55:07] And so for ADK, we have three different types of session service.
[55:07-55:09] And here we're using in-memory session service.
[55:09-55:14] So for in-memory session service, if you refresh the page or turn down the machine,
[55:14-55:17] it stores all the conversation stored in the run.
[55:18-55:20] And then when you reopen the machine,
[55:20-55:22] you will lose the conversation data we have.
[55:23-55:28] And in the ADK doc, you can take a look at session service school.
[55:29-55:36] So here we have in-memory session service that stores all the data directly in the application memory.
[55:36-55:39] We also have what has AR session service that can store things,
[55:39-55:41] like using what has AR infra,
[55:41-55:46] we have API code for session management so that it can scale on cloud.
[55:46-55:52] We also have database session service that can connect to relational database
[55:52-55:55] or different type of database for a persistent data.
[55:56-56:00] So if you store your information in the database solution,
[56:00-56:05] or in the what has AR solution, it can potentially scale and store long-term information.
[56:06-56:10] But right now in the lab, we're using in-memory session service.
[56:10-56:13] Cool. So now we have the session service.
[56:13-56:16] We need to replace the runner.
[56:16-56:19] We go here and search the runner,
[56:20-56:23] and we are copied this to the runner over here.
[56:23-56:29] And you can see if it attached the session service and memory service we're creating in the runner over here.
[56:29-56:32] And if you want to learn more about runner,
[56:32-56:38] you can also search runner in the stock to see the runner role,
[56:38-56:41] the auxrator, and understand more about runner.
[56:42-56:47] Cool. So now we're just implementing this important piece,
[56:47-56:51] runner session service and memory service in the API layer,
[56:51-56:56] so that we can connect the front-end react component to the ADK agent we're creating over here.
[56:57-57:01] And let's give a try to see the final response.
[57:01-57:03] So we just copy this and then we paste it here.
[57:03-57:04] It paste over here.
[57:05-57:12] So what we did over here is I'm actually using a script startapp.srgrip
[57:12-57:15] to help you quickly start application.
[57:15-57:20] But essentially what it does behind the scene is it first start the backend
[57:20-57:22] and checking the port with the ASO
[57:22-57:25] port to spin up the server.
[57:26-57:33] And then it's using so you can see that we have the service running on ASO's port.
[57:34-57:37] And then what's next is we want to use MPM,
[57:37-57:41] restore MPM round dev to start a react frontend.
[57:42-57:46] If you don't run the script, you can run the backend and frontend separately.
[57:46-57:51] But here we are running them so that it's easier for you to start that.
[57:51-57:54] So here we can see we have the local host, we're just clicking them.
[57:55-57:58] And now we expect to have the application working.
[57:58-58:01] Cool. So you can see that it's actually having application.
[58:01-58:06] I'm going to say allow it and you can see I can controlling this app.
[58:06-58:07] It's pretty cool, right?
[58:08-58:15] And what's amazing is those relationship or those 3D graph you're seeing over here
[58:15-58:19] is actually the 3D rendering of the Spanner Studio,
[58:19-58:22] the data you saw in the Spanner Studio.
[58:22-58:27] So this is a 3D version of all the relationship we have so far.
[58:27-58:31] If you, for example, if you click into the notes, for example, over here,
[58:31-58:36] you can have the survivor detected and this is the information over here.
[58:36-58:41] And now let's go to the lab and try to ask the question.
[58:41-58:43] For example, find skills similar to Healy.
[58:44-58:46] Just copy this, paste it.
[58:46-58:54] So what happens behind the scene is in the chat.py file, the fast API layer that we have,
[58:54-58:59] we are asking this question and we put this question to the ADK agent.
[58:59-59:02] And ADK agent going to return the response back to the user.
[59:02-59:06] Now if you see the song's back to response service
[59:06-59:09] account information using the email field, if you see the response,
[59:09-59:13] that's very likely to happen to you because now we're using the cloud
[59:13-59:18] shell environment and it will time out every other 30 minutes.
[59:18-59:22] So your token will expire for the security purpose.
[59:22-59:27] So all you need to do is just like me refresh this whole page to refresh the,
[59:27-59:32] so that we can refresh our token and we should solve this problem.
[59:33-59:35] So I'm going to click this open terminal.
[59:36-59:39] I already opened it, so I will refresh the page to see
[59:39-59:40] does that resolve the problem.
[59:41-59:45] And let's copy this and paste over here.
[59:45-59:48] As you can see now we find the response.
[59:48-59:55] You will find the skill similar to the Healy and it is using semantic similarity like Racksearch.
[59:55-59:58] What we did is we successfully create the graph rack agent.
[59:58-1:00:02] It's ADK and Spanner and then we're building,
[1:00:02-1:00:05] we connect the front end and back end, it's fast API.
[1:00:05-1:00:12] And now when you ask anything in the chat, you can directly find the result in the Spanner,
[1:00:12-1:00:14] from the Spanner knowledge base.
[1:00:15-1:00:16] Very cool.
[1:00:16-1:00:22] So you can also test different search and get the result.
