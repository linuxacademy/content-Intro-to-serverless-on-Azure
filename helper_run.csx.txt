#r "Newtonsoft.Json"

using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using HtmlAgilityPack; //reference to NuGet package containing HTML parser library
using System.Xml; //HtmlAgilityPack is dependent on this reference

public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
//housekeeping log
    log.LogInformation("C# HTTP trigger function processed a request.");

//part of the original code. We keep it here just to continue demoing an input parameter
    string name = req.Query["name"];

//original code that responds to the HTTP call and pulls the name parameter from the request
    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    dynamic data = JsonConvert.DeserializeObject(requestBody);
    name = name ?? data?.name;

//code that expands the canned function with "real work" of parsing an HTML page
        var html = @"https://download.cms.gov/nppes/NPI_Files.html";
        HtmlWeb web = new HtmlWeb();
//dump the results of the web page call into an HTML (XML) document
        var htmlDoc = web.Load(html);
//parse the document to find the first instance of a bullet point with a link
        var monthlyLink = htmlDoc.DocumentNode
            .SelectSingleNode("//li/a")
            .Attributes["href"].Value;
//modified the original canned response with the value of the link parsed from the HTML
    string responseMessage = string.IsNullOrEmpty(name)
        ? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
                : $"Monthly link: " + monthlyLink;
//original code that returns the response message
            return new OkObjectResult(responseMessage);
}
