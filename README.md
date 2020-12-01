# Live Project

<h3>Introduction</h3>

During my time at the Tech Academy, I had the opportunity to work on a live project which not only alowed me to utilize the technical skills I had learned, but also allowed me to work in an Agile/Scrum environment.

The live project was built using ASP .Net MVC and Entity Framework. It was built for local theater company in Portland, Oregon as a content management service (CMS) so that those from the company would be able to easily manage their website without needing to manage the code directly. During the two week sprint, I was able to work both <a href id="#front-end>front end</a> and back end stories. While I dedicated much of my time perfecting front end stories, I also improved pages on back end stories to incorporate dynamic syntax using the conveniences C# has to offer with Razor pages. Working full-stack provided me with experience identifying bugs on a large scale and understanding a larger overview of how apps are created on both client and server side. 


<h3 id="#front-end">Front-End Stories</h3>
I spent a majority of my spring working on a particular front-end story where I had to customize the Award Details page to match the color-scheme for the theater while creating a container that allowed it to show at the center when the page loaded.

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

CSS code for the Award Details Container

```
@Styles.Render("~/Content/Site.css")
@*<h2>Details</h2>*@

<div class="award-details-container-main p-3"> 
    <div class="rounded award-details-container p-3">
        <h4 class="text-center">Award Details</h4>           
        
        <div class="row 1 pt-3">
          <div class="col-5 mr-n5 font-weight-bold"> @*Used a bootstrap column and used a negative marging to bring content closer to the property names*@ 
            Production Title: @*@Html.DisplayNameFor(model => model.Production.Title):*@ @*Need to change this to Production Title if necessary. Only shows up as "Title"*@
          </div>
          <div class="col">
            @Html.DisplayFor(model => model.Production.Title)
          </div>
        </div>
        <div class="row 2">
          <div class="col-5 mr-n5 font-weight-bold">
              @Html.DisplayNameFor(model => model.Year):
          </div>
          <div class="col">
             @Html.DisplayFor(model => model.Year)
          </div>
        </div>
      <div class="row 3">
          <div class="col-5 mr-n5 font-weight-bold">
            @Html.DisplayNameFor(model => model.Name):
          </div>
          <div class="col">
            @Html.DisplayFor(model => model.Name)
          </div>
        </div>
        <div class="row 3">
          <div class="col-5 mr-n5 font-weight-bold">
            @Html.DisplayNameFor(model => model.Type):
          </div>
          <div class="col">
            @Html.DisplayFor(model => model.Type)
          </div>
        </div>
        <div class="row 4">
          <div class="col-5 mr-n5 font-weight-bold">
            @Html.DisplayNameFor(model => model.Category):
          </div>
          <div class="col">
            @Html.DisplayFor(model => model.Category)
          </div>
        </div>
        <div class="row 5">
          <div class="col-5 mr-n5 font-weight-bold">
            @Html.DisplayNameFor(model => model.Recipient):
          </div>
          <div class="col">
            @Html.DisplayFor(model => model.Recipient)@if (Model.Recipient != null){<i class="fa fa-info-circle fa-fw"></i>}
          </div>
        </div>

        <p><div class="font-weight-bold">@Html.DisplayNameFor(model => model.OtherInfo):</div>
        @Html.DisplayFor(model => model.OtherInfo)
        </p>

    </div>

    <p class="p-1 ml-n2">
    @*Button to Edit Page*@
      <button class="iconBtn" onclick="window.location.href ='@Url.Action("Edit", "Awards", new { id = Model.AwardId })'">
        <i class="fa fa-edit fa-fw"></i>Edit
      </button>


      @*Button Back to Awards Index Page*@
      <button class="iconBtn" onclick="window.location.href ='@Url.Action("Index", "Awards")'">
        <i class="fa fa-hand-point-left fa-fw"></i>Back to List
      </button>
    </p>
</div>
```
I initially had created two columns and listed everything inside those two columns, but the Title and Content columns were not as close as the client desired. So I created a row for each Title and Content pair and created two columns within the row, which allowed more much easier customization. 

After completeing the first part of this story, I continued to work on the second story pertaining to the Award Details. It also dealt with customizing the layout but required me to write an onclick function in Javasript so that when the info icon was clicked, the Award Details container slid to the left and the Cast Member Details appeared next to it in a smooth transition. It also asked for a media query so that when the screen size was smaller, the Cast Member Details would appear underneath the Award Details container so as not to require users to scroll left and right. 

I used this Javascript code for the onclick function: 

```
@******************JS OnClick Function***************@
<script>
    var castDetails = document.getElementById("castDetails");
    var awardDetails = document.getElementById("awardDetails");

    function toggleCastDetails() {       
        if (awardDetails.className == "slideLeftAward") {
            //shrink the box if it's open
            castDetails.className = "slideRightCast";
            awardDetails.className = "slideRightAward";
        }

        else {
            //Expand the box
            awardDetails.className = "slideLeftAward";
            castDetails.className = "slideLeftCast";  
        }
    }
</script>
```

I then created CSS for each animation, using Webkit-Transform to slide each container in and out in a smooth manner. This was a very challenging part of my sprint, but I was able to review existing Bootstrap classes and how they conflict with CSS customizations.


<h3 id=#back-end">Back-End Stories</h3>
I was able to work on several smaller back-end stories. The one I am most proud of is refactoring a previously written seed method so that it was more useful when adding future content from the webpage. It was not originally written as a list, so I cleaned the code so that a future developer might be able to simply add new DisplayInfo objects to the list. For this story, I also seeded the company history and mission statements and created a ViewBag to display these contents dynamically from the database if they are ever updated.
                 
                 
```                 
protected void SeedDisplayInfo()
    {
    var info = new List<DisplayInfo>() //re-formatted the seed method so it will be easier to add information later if needed
            {
                new DisplayInfo
                {
                    Title = "Archive Page-title",
                    TextContent = "Theatre Vertigo Archive"
                },

                new DisplayInfo
                {
                    Title = "Archive Page-content",
                    TextContent = "In 1997, Theatre Vertigo was founded by Paul Floding, Nanette Pettit and Jeff Meyers.  " +
                    "Since then, Theatre Vertigo has performed in numerous spaces including The Russell Street Theater, " +
                    "The Electric Company, Theater!Theatre!, and their current home, The Shoebox Theater." +
                    "From 2003 to 2014, Theatre Vertigo produced Anonymous Theatre as a summer fundraiser in collaboration " +
                    "with The Anonymous Theatre Company. Other past collaborations include defunkt theatre, " +
                    "Stark Raving Theater, and Tears of Joy Theatre." +
                    "<br />" +
                    "<br />" +
                    "Theatre Vertigo has worked on world premieres including <i>Faust</i>. <i>Us</i> by Joseph Fisher, " +
                    "<i>99 Ways to Fuck a Swan</i> by Kim Rosenstock, and <i>The End of Sex</i> by Craig Jessen." +
                    "In 2016, Theatre Vertigo produced its first officially commissioned work from a playwright, <i>I Want " +
                    "To Destroy You</i>, by Rob Handel." 
                    //For the Archive content page - same as the content in "History" DisplayInfo, but decided to leave it in case
                    //the theater wants to change this content on the archive page.
                },

                new DisplayInfo
                {
                    Title = "History",
                    TextContent = "In 1997, Theatre Vertigo was founded by Paul Floding, Nanette Pettit and Jeff Meyers.  " +
                    "Since then, Theatre Vertigo has performed in numerous spaces including The Russell Street Theater, " +
                    "The Electric Company, Theater!Theatre!, and their current home, The Shoebox Theater." +
                    "From 2003 to 2014, Theatre Vertigo produced Anonymous Theatre as a summer fundraiser in collaboration " +
                    "with The Anonymous Theatre Company. Other past collaborations include defunkt theatre, " +
                    "Stark Raving Theater, and Tears of Joy Theatre." +
                    "<br />" +
                    "<br />" +
                    "Theatre Vertigo has worked on world premieres including <i>Faust</i>. <i>Us</i> by Joseph Fisher, " +
                    "<i>99 Ways to Fuck a Swan</i> by Kim Rosenstock, and <i>The End of Sex</i> by Craig Jessen." +
                    "In 2016, Theatre Vertigo produced its first officially commissioned work from a playwright, <i>I Want " +
                    "To Destroy You</i>, by Rob Handel."
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
    }
```

I then used ViewData to display the information on the page.


```
public ActionResult About()
{
    var newInfo = from l in db.DisplayInfo
    select l;
    var info = newInfo.ToList();
    ViewData["History"] = (info.Where(x => x.Title.Contains("History")).FirstOrDefault().TextContent);
    ViewData["Mission"] = (info.Where(x => x.Title.Contains("Mission")).FirstOrDefault().TextContent);
   
    return View();
}
```

