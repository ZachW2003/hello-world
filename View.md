@model TicketSubmissionModel;

@{ ViewData["Title"] = "Ticket Counter"; }

<div class="container">
    <h1 class="mt-3 mb-4">@ViewBag.Title</h1>
   
    <form asp-action="Index" method="post">
        <div class="row">
            <label asp-for="VenueName" class="col-sm-3 form-label">
                Venue:
            </label>
            <div class="col-sm-3">
                <input asp-for="VenueName" class="form-control" />
            </div>
            <span asp-validation-for="VenueName"
                  class="col text-danger"></span>
        </div>
        
        <div class="row">
            <label asp-for="TicketsBought" class="col-sm-3 form-label">
                Tickets Bought: </label>
            <div class="col-sm-3">
                <input asp-for="TicketsBought" class="form-control" />
            </div>
            <span asp-validation-for="TicketsBought" 
                  class="col text-danger"></span>
        </div>
     

        <div class="row">
            <label asp-for="TicketID" class="col-sm-3 form-label">
                Ticket ID:
            </label>
            <div class="col-sm-3">
                <input asp-for="TicketID" class="form-control" />
            </div>
            <span asp-validation-for="TicketID"
                  class="col text-danger"></span>
        </div>
        
        <div class="row">
            <label class="col-sm-3 form-label">Total Tickets Punched:</label>
            <div class="col-sm-3">
                <input value="@ViewBag.TicketTotal.ToString()" readonly
                       class="form-control" />
            </div>
        </div>
        <div class="row">
            <div class="col offset-sm-3">
                <button type="submit" class="btn btn-primary">
                    Add tickets</button>
                <a asp-action="Index"
                   class="btn btn-secondary">Clear</a>
            </div>
        </div>

        
    </form>
</div>
