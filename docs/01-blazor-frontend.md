# Session 01: Developing a Blazor Frontend Web App

In this session, we're going to develop a ![Blazor Frontend Web App](https://learn.microsoft.com/en-us/aspnet/core/blazor?WT.mc_id=dotnet-121695-juyoo).

<!-- In this session, we'll take advantage of ![GitHub Copilot](https://docs.github.com/en/copilot/overview-of-github-copilot/about-github-copilot-business) capabilities to quickly develop a ![Blazor front-end web app](https://learn.microsoft.com/en-us/aspnet/core/blazor?WT.mc_id=dotnet-121695-juyoo). -->

> [GitHub Codespaces](https://docs.github.com/ko/codespaces/overview) Proceed based on working in the environment. In your local development environment's [Visual Studio Code](https://code.visualstudio.com/?WT.mc_id=dotnet-121695-juyoo)is mostly similar, but may be slightly different.

![Architecture](./images/01-architecture.png)

## 01-1: Create a Blazor project

1. Open a terminal and run the command below to create and navigate to the lab directory.

    ```bash
    cd $CODESPACE_VSCODE_FOLDER
    mkdir workshop
    cd workshop
    ```

1. Run the commands below to create a Blazor web app project.

    ```bash
    dotnet new sln -n AspireYouTubeSummariser
    dotnet new blazor -n AspireYouTubeSummariser.WebApp -int server -ai true
    dotnet sln add AspireYouTubeSummariser.WebApp
    ```

1. Run the commands below to build and run your Blazor web app project.

    ```bash
    dotnet restore && dotnet build
    dotnet run --project AspireYouTubeSummariser.WebApp
    ```

You can check out the project you have created so far in [save-points/session-00](../save-points/session-00/).

## 01-2: Create UI Component

To use a project imported from a save point, run the command below to restore the project.

   ```bash
   cd $CODESPACE_VSCODE_FOLDER
   mkdir -p workshop && cp -a save-points/session-00/. workshop/
   cd workshop
   dotnet restore && dotnet build
   ```

1. In Solution Explorer Under the directory `Components` Create a directory `UI`.
1. Under the `UI` directory, create a Razor Component file named `YouTubeSummariserComponent`. Inside the generated file, you'll already find something similar to the one below.

    ```razor
    <h3>YouTubeSummariserComponent</h3>

    @code {

    }
    ```

1. Clear all of the above and enter the code below.

    ```razor
    <div class="container">
        <div class="row">
            <h2>YouTube Summariser</h2>
        </div>

        <div class="row">
            <div class="col">
                <div class="mb-3">
                    <label for="youtube-link" class="form-label"><strong>YouTube Link</strong></label>
                    <input class="form-control" id="youtube-link" placeholder="Add YouTube link here" @bind="youTubeLinkUrl" />
                </div>
            </div>
            <div class="col">
                <div class="mb-3">
                    <label for="video-language-code" class="form-label"><strong>Video Language</strong></label>
                    <select class="form-select" id="video-language-code" aria-label="Video language code" @bind="videoLanguageCode">
                        <option value="en" selected>English</option>
                        <option value="ko">Korean</option>
                    </select>
                </div>
            </div>
            <div class="col">
                <div class="mb-3">
                    <label for="summary-language-code" class="form-label"><strong>Summary Language</strong></label>
                    <select class="form-select" id="summary-language-code" aria-label="Summary language code" @bind="summaryLanguageCode">
                        <option value="en" selected>English</option>
                        <option value="ko">Korean</option>
                    </select>
                </div>
            </div>
        </div>

        <div class="row">
            <div class="mb-3">
                <button type="button" class="btn btn-primary" @onclick="SummariseAsync">Summarise!</button>
                <button type="button" class="btn btn-secondary" @onclick="ClearAsync">Clear!</button>
            </div>
        </div>

        <div class="row">
            <div class="mb-3">
                <label for="summary" class="form-label"><strong>Summary</strong></label>
                <textarea class="form-control" id="summary" rows="10" placeholder="Result will show here" readonly>@summaryResult</textarea>
            </div>
        </div>
    </div>

    @code {
        private string youTubeLinkUrl = string.Empty;
        private string videoLanguageCode = "en";
        private string summaryLanguageCode = "en";
        private string summaryResult = string.Empty;

        private async Task SummariseAsync()
        {
            throw new NotImplementedException();
        }

        private async Task ClearAsync()
        {
            throw new NotImplementedException();
        }
    }
    ```

1. At the beginning of the `YouTubeSummariserComponent.razor` file, enter the following:

    ```razor
    @using AspireYouTubeSummariser.WebApp.Clients
    @inject IApiAppClient ApiApp
    ```

1. In the `YouTubeSummariserComponent.razor` file, enter the code below inside the `SummariseAsync` method.

    ```razor
    private async Task SummariseAsync()
    {
        try
        {
            var result = await ApiApp.SummariseAsync(youTubeLinkUrl, videoLanguageCode, summaryLanguageCode);
            summaryResult = result;
        }
        catch (Exception ex)
        {
            summaryResult = ex.Message;
        }
    }
    ```

1. Modify the `ClearAsync` method in the `YouTubeSummariserComponent.razor` file as shown below.

    ```razor
    private async Task ClearAsync()
    {
        youTubeLinkUrl = string.Empty;
        videoLanguageCode = "en";
        summaryLanguageCode = "en";
        summaryResult = string.Empty;

        await Task.CompletedTask;
    }
    ```

## 01-3: Create API Client

1. In Solution Explorer, create a `Clients` directory and create a C# class file named `ApiAppClient` in it. Inside the generated file, you'll already find something similar to the one below.

    ```csharp
    namespace AspireYouTubeSummariser.WebApp.Clients;

    public class ApiAppClient
    {

    }
    ```

1. Between `namespace` and `class`, add the `IApiAppClient` interface as shown below.

    ```csharp
    public interface IApiAppClient
    {
        Task<string> SummariseAsync(string youTubeLinkUrl, string videoLanguageCode, string summaryLanguageCode);
    }
    ```

1. Modify the `ApiAppClient` class as shown below.

    ```csharp
    public class ApiAppClient : IApiAppClient
    {
        public async Task<string> SummariseAsync(string youTubeLinkUrl, string videoLanguageCode, string summaryLanguageCode)
        {
            throw new NotImplementedException();
        }
    }
    ```

## 01-4: Injecting dependencies into the API Client

1. Open the `Program.cs` file in Solution Explorer and add `var app = builder.Build();` line, add a dependency injection for `ApiAppClient` as shown below.

    ```csharp
    builder.Services.AddHttpClient<IApiAppClient, ApiAppClient>(p => p.BaseAddress = new Uri("http://localhost:5050"));
    ```

   The port number `5050` is a random number and will need to be changed later.

1. This will result in an error stating that the namespace reference is not possible. Place the cursor where the error occurred and press the `CTRL`+`.` key or the `CMD`+`.` key to add the namespace.
1. Open the `ApiAppClient.cs` file again and modify it to inject an instance of `HttpClient` via the constructor, as shown below.

    ```csharp
    public class ApiAppClient(HttpClient http) : IApiAppClient
    {
        private readonly HttpClient _http = http ?? throw new ArgumentNullException(nameof(http));

        public async Task<string> SummariseAsync(string youTubeLinkUrl, string videoLanguageCode, string summaryLanguageCode)
    ```

1. Again, modify the `SummariseAsync` method as shown below.

    ```csharp
    public async Task<string> SummariseAsync(string youTubeLinkUrl, string videoLanguageCode, string summaryLanguageCode)
    {
        using var response = await _http.PostAsJsonAsync(
            "summarise",
            new { youTubeLinkUrl, videoLanguageCode, summaryLanguageCode }).ConfigureAwait(false);

        var summary = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
        return summary;
    }
    ```

## 01-5: Adding to a UI Component Page

1. In Solution Explorer, open the `Home.razor` file under the `Components/Pages` directory.

1. At the bottom of the page, add a `YouTubeSummariserComponent` as shown below.

    ```razor
    <YouTubeSummariserComponent />
    ```
This will result in an error stating that the namespace reference is not possible. Place the cursor where the error occurred and press the `CTRL`+`.` key or the `CMD`+`.` key to add the namespace.

## 01-6: Launch the Blazor Web App

1. In Solution Explorer, select the `AspireYouTubeSummariser.WebApp` project and right-click to run it in debugging mode.

1. On the first screen, enter your YouTube link as shown below and click the `Summarise!` button.

    ![YouTubeSummariserComponent #1](./images/01-blazor-frontend-01.png)

   It doesn't matter what the YouTube link is. In this case, we use the [https://youtu.be/z1M-7Bms1Jg](https://youtu.be/z1M-7Bms1Jg) link.

1. Then you can see the error message as below.

    ![YouTubeSummariserComponent #2](./images/01-blazor-frontend-02.png)

---

Congratulations! You're done developing your Blazor front-end web app. Now let's move on to [Session 02: Developing ASP.NET Core Backend API Apps](./02-aspnet-core-backend.md).
