using Microsoft.AspNetCore.Mvc;
using TicketCounter.Models;

namespace TicketCounter.Controllers
{
    public class HomeController : Controller
    {
        [HttpGet]
        public IActionResult Index()
        {
            ViewBag.TicketTotal = 0;
            return View();
        }

        [HttpPost]
        public IActionResult Index(TicketSubmissionModel model)
        {
            if (ModelState.IsValid)
            {
                ViewBag.TicketTotal = model.CalculateTotal();
            }
            else
            {
                ViewBag.TicketTotal = 0;
            }
             return View(model);
        }
    }
}
