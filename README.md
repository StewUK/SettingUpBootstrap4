# SettingUpBootstrap4
How to convert dotnet mvc app into using Bootstrap 4

http://www.mytecbits.com/microsoft/dot-net/bootstrap-asp-net-core-mvc
https://stackoverflow.com/questions/48481003/how-to-use-bootstrap-4-in-asp-net-core

-- Create package.json in root
```
{
  "version": "1.0.0",
  "name": "bstest",
  "private": true,
  "devDependencies": {
    "bootstrap": "4.0.0",
    "jquery": "3.3.1",
    "popper.js": "1.12.9"
  }
}
```
-- Run "npm install"

-- Run "dotnet add package BuildBundlerMinifier"

-- Amend bundleconfig.json
```
[
  {
    "outputFileName": "wwwroot/css/site.min.css",
    "inputFiles": [
      "wwwroot/css/site.css"
    ]
  },
  {
    "outputFileName": "wwwroot/js/site.min.js",
    "inputFiles": [
      "wwwroot/js/site.js"
    ],
    "minify": {
      "enabled": true,
      "renameLocals": true
    },
    "sourceMap": false
  },
  {
    "outputFileName": "wwwroot/vendor.min.css",
    "inputFiles": [
      "node_modules/bootstrap/dist/css/bootstrap.min.css"
    ],
    "minify": { "enabled": false }
  },
  {
    "outputFileName": "wwwroot/vendor.min.js",
    "inputFiles": [
      "node_modules/jquery/dist/jquery.min.js",
      "node_modules/popper.js/dist/umd/popper.min.js",
      "node_modules/bootstrap/dist/js/bootstrap.min.js"
    ],
    "minify": { "enabled": false }
  }
]
```
-- Amend _Layout.cshtml
```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"] - bstest</title>

    <environment include="Development">
        <link rel="stylesheet" href="~/vendor.min.css" />
        <link rel="stylesheet" href="~/css/site.css" />
    </environment>
    <environment exclude="Development">
        <link rel="stylesheet" href="~/vendor.min.css" />
        <link rel="stylesheet" href="~/css/site.min.css" asp-append-version="true" />
    </environment>
</head>
<body>
    <nav class="navbar navbar-expand-md navbar-dark bg-dark">
        <a asp-area="" asp-controller="Home" asp-action="Index" class="navbar-brand">TestingApp</a>
        <button class="navbar-toggler navbar-toggler-right" type="button" data-toggle="collapse"
        data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent"
        aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"/>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
                <li class="nav-item">
                    <a asp-area="" asp-controller="Home" asp-action="Index" class="nav-link">Home</a>
                </li>
                <li class="nav-item">
                    <a asp-area="" asp-controller="Home" asp-action="About" class="nav-link">About</a>
                </li>
                <li class="nav-item">
                    <a asp-area="" asp-controller="Home" asp-action="Contact" class="nav-link">Contact</a>
                </li>
                
            </ul>
            <span class="navbar-text">
                Hello, @User.Identity.Name!
            </span>
        </div>
    </nav>

    <div class="container body-content">
        @RenderBody()
        <hr />
        <footer>
            <p>&copy; 2018 - bstest</p>
        </footer>
    </div>

    <environment include="Development">
        <script src="~/vendor.min.js"></script>
        <script src="~/js/site.js" asp-append-version="true"></script>
    </environment>
    <environment exclude="Development">
        <script src="~/vendor.min.js"></script>
        <script src="~/js/site.min.js" asp-append-version="true"></script>
    </environment>

    @RenderSection("Scripts", required: false)
</body>
</html>
```

-- Amend Index.cshtml (Carousel fix)
```
<div id="myCarousel" class="carousel slide" data-ride="carousel" data-interval="6000">
    <ol class="carousel-indicators">
        <li data-target="#myCarousel" data-slide-to="0" class="active"></li>
        <li data-target="#myCarousel" data-slide-to="1"></li>
        <li data-target="#myCarousel" data-slide-to="2"></li>
        <li data-target="#myCarousel" data-slide-to="3"></li>
    </ol>
    <div class="carousel-inner" role="listbox">
        <div class="carousel-item active">
            <img src="~/images/banner1.svg" alt="ASP.NET" class="img-responsive" />
            <div class="carousel-caption" role="option">
                <p>
                    Learn how to build ASP.NET apps that can run anywhere.
                    <a class="btn btn-default" href="https://go.microsoft.com/fwlink/?LinkID=525028&clcid=0x409">
                        Learn More
                    </a>
                </p>
            </div>
        </div>
        <div class="carousel-item">
            <img src="~/images/banner2.svg" alt="Visual Studio" class="img-responsive" />
            <div class="carousel-caption" role="option">
                <p>
                    There are powerful new features in Visual Studio for building modern web apps.
                    <a class="btn btn-default" href="https://go.microsoft.com/fwlink/?LinkID=525030&clcid=0x409">
                        Learn More
                    </a>
                </p>
            </div>
        </div>
        <div class="carousel-item">
            <img src="~/images/banner3.svg" alt="Package Management" class="img-responsive" />
            <div class="carousel-caption" role="option">
                <p>
                    Bring in libraries from NuGet and npm, and automate tasks using Grunt or Gulp.
                    <a class="btn btn-default" href="https://go.microsoft.com/fwlink/?LinkID=525029&clcid=0x409">
                        Learn More
                    </a>
                </p>
            </div>
        </div>
        <div class="carousel-item">
            <img src="~/images/banner4.svg" alt="Microsoft Azure" class="img-responsive" />
            <div class="carousel-caption" role="option">
                <p>
                    Learn how Microsoft's Azure cloud platform allows you to build, deploy, and scale web apps.
                    <a class="btn btn-default" href="https://go.microsoft.com/fwlink/?LinkID=525027&clcid=0x409">
                        Learn More
                    </a>
                </p>
            </div>
        </div>
    </div>
    <a class="carousel-control-prev" href="#myCarousel" role="button" data-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="sr-only">Previous</span>
    </a>
    <a class="carousel-control-next" href="#myCarousel" role="button" data-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="sr-only">Next</span>
    </a>
</div>
```


