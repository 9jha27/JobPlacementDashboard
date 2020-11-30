# Live Project

<h3>Introduction</h3>

During my time at the Tech Academy, I had the opportunity to work on a live project which not only alowed me to utilize the technical skills I had learned, but also allowed me to work in an Agile/Scrum environment.

The live project was built using ASP .Net MVC and Entity Framework. It was built for local theater company in Portland, Oregon as a content management service (CMS) so that those from the company would be able to easily manage their website without needing to manage the code directly. During the two week sprint, I was able to work both <a href id="#front-end>front end</a> and back end stories. While I dedicated much of my time perfecting front end stories, I also improved pages on back end stories to incorporate dynamic syntax using the conveniences C# has to offer with Razor pages. Working full-stack provided me with experience identifying bugs on a large scale and understanding a larger overview of how apps are created on both client and server side. 


<h3 id="#front-end">Front-End Stories</h3>

```
.award-details-container-main {
    margin: auto;
    max-width: 500px; 
}

.award-details-container {
    border-radius: 15px;
    background-color: var(--main-secondary-color);
    margin: auto;
}

```

CSS for an Award Details Container




<h3 id=#back-end">Back-End Stories</h3>
                 
```
var newInfo = from l in db.DisplayInfo
select l;
var info = newInfo.ToList();
ViewBag.History = (info.Where(x => x.Title.Contains("History")));
ViewBag.Mission = (info.Where(x => x.Title.Contains("Mission")));
```
