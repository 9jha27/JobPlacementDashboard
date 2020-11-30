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
protected void SeedDisplayInfo()
    {
    var info = new List<DisplayInfo>() 
    {
        new DisplayInfo
        {
            Title = "Archive Page-title",
            TextContent = "Theatre Vertigo Archive"
        },

        new DisplayInfo
        {
            Title = "History",
            TextContent = "In 1997, Theatre Vertigo was founded by Paul Floding, Nanette Pettit and Jeff Meyers.  " +
                    "Since then, Theatre Vertigo has performed in numerous spaces including The Russell Street Theater, " +
                    "The Electric Company, Theater!Theatre!, and their current home, The Shoebox Theater. " +
                    "From 2003 to 2014, Theatre Vertigo produced Anonymous Theatre as a summer fundraiser in collaboration with The Anonymous Theatre Company." +
                    "Other past collaborations include defunkt theatre, Stark Raving Theater, and Tears of Joy Theatre." +
                    "\nTheatre Vertigo has worked on world premieres including Faust Us by Joseph Fisher, 99 Ways to Fuck a " +
                    "Swan by Kim Rosenstock, and The End of Sex by Craig Jessen. In 2016, Theatre Vertigo produced its first " +
                    "officially commissioned work from a playwright, I Want To Destroy You, by Rob Handel."
        },

        new DisplayInfo
        {
            Title = "Mission",
            TextContent = "Theatre Vertigo’s mission is to engage audiences through compelling, " +
            "ensemble - driven theatre with a focus on producing and developing new and rarely seen works."
        }
    };
    info.ForEach(infos => context.DisplayInfo.AddOrUpdate(x => new { x.Title, x.TextContent }, infos));
    context.SaveChanges();
}
```
A seed method so that admin can update the history or mission statements and have it change dynamically without having to update any code. 


```
public ActionResult About()
{
    var newInfo = from l in db.DisplayInfo
    select l;
    var info = newInfo.ToList();
    ViewBag.History = (info.Where(x => x.Title.Contains("History")));
    ViewBag.Mission = (info.Where(x => x.Title.Contains("Mission")));
   
    return View();
}
```
Added a ViewBag for the seeded History and Mission details 
