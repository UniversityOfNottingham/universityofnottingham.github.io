!!! success "`.NET Core` is now the approved target platform for .NET Applications."
    Please **do not** create any new **.NET Framework** projects without discussing this with the **Senior Developers**.

!!! info "Approved Technologies"
    The Senior Developers have discussed and chosen certain frameworks, libraries and technologies that we prefer to use as a solution for a given need or problem.

    Please consult this list when you are looking to solve a problem in your application, to see if we have a preferred way of doing things.

    This list can be debated and must evolve, but to see new technologies used or approved, the Senior Developers must be consulted and a case must be made.

## Technologies by use case

!!! tip "These use cases include"
    !!! success "approved technologies"
    !!! info "notes on optional supporting libraries"
    !!! warning "legacy technologies you might come across, but mustn't use on new apps."

??? summary "Active Directory User Authentication"
    !!! success "ASP.NET Identity Core"
    !!! info "UoN libraries for authentication and authorisation"

??? summary "Local User Accounts"
    !!! success "ASP.NET Identity Core"
    !!! info "Entity Framework Core"
    !!! info "UoN libraries for authentication and authorisation"

??? summary "Basic Authentication"
    !!! success "ZNetCS.AspNetCore.Authentication.Basic"
    !!! tip "Probably used in conjunction with another Auth backend (e.g. Local or AD)"

??? summary "Relational Database ORM"
    !!! success "Entity Framework Core"
        Use **Code First Migrations**

??? summary "Inversion of Control (IoC) / Dependency Injection (DI)"
    !!! success "Microsoft.Extensions.DependencyInjection"
    !!! success "Autofac"
        Only when doing more advanced DI that the above can't perform.

??? summary "Scheduled Tasks"
    !!! success "Hangfire"

??? summary "Queued Tasks"
    !!! success "Hangfire"

??? summary "Email sending"
    !!! success "Mailkit"
        Configures and performs spec compliant email tasks such as sending over SMTP.
    !!! success "SendGrid"
        Configures and performs email sending via the SendGrid API.
    !!! success "UoN.AspNetCore.RazorViewRenderer"
        Renders a string as a Razor View, allowing for rich email templating.

??? summary "Error Logging"
    !!! success "NLog"

??? summary "Unit Testing"
    !!! success "XUnit"
    !!! info "Moq"

??? summary "JSON"
    !!! success "Newtonsoft.JSON"

??? summary "Faceted Search"
    !!! success "Separate ElasticSearch instance"
        !!! fail "Don't do search itself within .NET - interact with ES instead."
    !!! success "Elastic Search.NET - low level client"
    !!! success "NEST - high level Elastic Search client"

??? summary "Object mapping"
    !!! success "AutoMapper"
        e.g. ViewModels -> DTOs -> Entities or vice versa

??? summary "Reading / writing CSV files"
    !!! success "CsvHelper"

??? summary "Parsing and rendering Markdown"
    !!! success "Westwind.AspNetCore.Markdown"
        - supports rendering in Razor Views via a TagHelper
        - supports parsing in C# and Razor using static methods

        [Documentation](https://weblog.west-wind.com/posts/2018/Mar/23/Creating-an-ASPNET-Core-Markdown-TagHelper-and-Parser)