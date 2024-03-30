# Session 00: Setting Up Your Development Environment

In this session, you will set up the development environment required to conduct the workshop.

## Subscribe to Azure OpenAI Proxy

1. Click the link below to sign up for an Azure OpenAI proxy subscription.

   👉 Subscription Link: [https://aka.ms/aspireinadaykr/request](https://aka.ms/aspireinadaykr/request)

1. Confirm that the 'DoNotReply@cloudextend.net' sender has received your Azure OpenAI proxy subscription code via the email you subscribed.

## Sign up for an Azure OpenAI proxy subscription and a GitHub Copilot subscription

1. Finalize your GitHub Copilot subscription via the link below.

   👉 GitHub Copilot subscription sign-up link: [https://github.com/redeem](https://github.com/redeem)

1. Check the link below to see if the Azure OpenAI proxy code is working properly.

   👉 Azure OpenAI Proxy Playground Link: [https://proxy.aoai.kr/playground](https://proxy.aoai.kr/playground)

## Get started with Gitoub Codespaces.

1. Fork this repository into your own GitHub account.
1. Create a GitHub Codespaces instance from your forked repository.
    ![Creating a Gitub Codespace Instance](./images/00-setup-01.png)
1. Run the command below in a terminal in your GitHub codespace to see the location of your current repository.
    ```bash
    git remote -v
    ```
   When you run this command, you should get something like this: If you see 'Azure-Samples' in 'origin', you'll need to recreate the codespace in your own repository.
    ```bash
    origin  https://github.com/<Your GitHub ID>/aspire-app-dev-in-a-day-ko (fetch)
    origin  https://github.com/<Your GitHub ID>/aspire-app-dev-in-a-day-ko (push)
    upstream        https://github.com/Azure-Samples/aspire-app-dev-in-a-day-ko.git (fetch)
    upstream        https://github.com/Azure-Samples/aspire-app-dev-in-a-day-ko.git (push)
    ```

---

Congratulations! You're done setting up your development environment. Now let's move on to Session 01: Developing a Blazor Front-End Web App(./01-blazor-frontend.md).
