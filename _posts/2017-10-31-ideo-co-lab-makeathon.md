---
layout: post
title:  "Prototyping at the IDEO CoLab"
date:   2017-10-31
author: Jared Johnson
---

This past weekend, I participated in the [IDEO CoLab Makeathon](http://www.ideocolab.com/makeathon/), where I was part of a team tasked with ideating, designing, and building a prototype in a single day.


## IDEO and the CoLab Makeathon

IDEO is a global design consultancy that is famous for pioneering the use of design thinking methodology in product and service design. The firm opened the CoLab offices in Cambridge, MA and San Francisco, CA in partnership with a number of different organizations across finance, technology and education and thinks of these locations as an R&D network. The focus of the CoLab is around designing prototypes exploring emerging technologies. Before arriving, I was told to brush up on [prototyping tools for blockchain and artificial intelligence](https://medium.com/ideo-colab/quick-prototyping-tools-for-emerging-technologies-3fb56f62360a).

The Makeathon is an event held annually at the CoLab. The CoLab team uses the Makeathon to evaluate candidates interested in their two-week January fellowship, an opportunity that attracts "makers" from the fields of business, engineering and design.

## My team

When we arrived at the Cambridge, MA CoLab office, the 60 or so of us were organized into 14 teams. My team members were a designer who also teaches human centered design in New York, an undergraduate Mechanical Engineering major at MIT, an MBA student at Columbia Business School, and an engineer working on computer vision. Clearly, I was in incredible company.

![team](/assets/images/IDEO_team.jpg)*Our team: Matt, Jennifer, Max, Wei and Me*

## Ideating

Each team was handed a brief that described their task for the day. My team's brief discussed exploring the balance between the utility of voice interfaces and privacy. It gave an example of a voice interface in an immigrations office, where natural language processing and artificial intelligence could certainly be useful but the privacy concerns around transmitting sensitive information are weighty.

After reading through the brief, we spent the morning brainstorming and iterating on our ideas utilizing some of IDEO's frameworks. We filled a poster board with sticky notes, which we rearranged multiple times as we worked to focus our ideas around one solution. Before breaking for lunch, we stumbled upon an idea to integrate a voice interface in a stuffed animal and grew excited. We knew that we wanted to build something for first responders or hospitals and had discussed different ways to make critical information collection easier for medical professionals. Our pivot came when considering how kids may be less likely to tell doctors (i.e. strangers) how they are feeling. Perhaps they would feel more comfortable talking to something that looks more like their furry friends at home.

![brainstorming](/assets/images/IDEO_brainstorming.jpg)*An idea is born*

## Making

In the afternoon, we started prototyping. The IDEO staff were helpful in pointing us toward some tools that might be helpful for what we wanted to build. I knew that I wanted to dig into the technical side and spent some time working to get Google's [Dialogflow](https://dialogflow.com/) up and running on my local machine while some of the other team members started to work on our presentation and business case. By mid afternoon, we had a breakthrough. We were able to write a speech script on my computer and get it to load on a borrowed Google Home.

![prototype2](/assets/images/IDEO_prototype.jpg)*IDEOg prototype*

## Demo Time

By the end of the day, we were able to demo a functional prototype that would respond to the user's voice. We borrowed an old IDEO prototype, a cardboard dog named Bernard, and paired it with our Google Home to create IDEOg. Our product was aimed at hospitals who could provide kids who enter the waiting room an IDEOg. The product would ask the child some questions about how they are feeling and let them know that the doctor would soon be out to see them. The voice interface can overhear crucial details and communicate with the doctor, who is able to see a dashboard of data collected by the IDEOg.

Collecting information, and information from a child no less, is certainly sensitive and our team had multiple discussions on how our product would handle this responsibility. To address this, we made two key decisions. First, we decided that the product should not retain any information from the patients. Once the child is released from the hospital, the product should delete all information that it has collected. Second, we decided that the doctor is the only person who is able to see the data on the back-end and is only able to see the assumptions that the AI has made, not the raw data itself. Anything that the doctor would like to preserve, he or she must record that in the medical files manually.  

![prototype1](/assets/images/IDEO_prototype_with_google_home.jpg)*IDEOg at our demo*

## Reflection

I was extremely proud of what my team was able to accomplish in one day and had a blast working with them. I was able to learn some of the frameworks used in human centered design, play around with new technologies, and tried my best to answer really difficult questions about the role that these technologies should play in future society. I would recommend future IDEO CoLab Makeathons to anyone interested in exploring emerging technologies and working on a team with incredibly talented people from a cross-section of fields.
