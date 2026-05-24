# 🌅 Automated Morning Briefer (n8n Workflow)

A zero-cost, fully automated n8n workflow that fetches the daily weather and the top news headline, combining them into a single consolidated morning briefing sent directly to your phone. 

Designed with fault tolerance and completely free, keyless APIs.

## ⚙️ Architecture & Data Flow

This workflow operates on a parallel execution model to prevent bottlenecks, merging separate data streams into a single clean payload.

1. **Schedule Trigger:** Initiates the workflow every day at 7:00 AM.
2. **Parallel Fetching:**
   - **HTTP Request:** Calls the Open-Meteo API for real-time local weather.
   - **RSS Read:** Fetches the latest breaking news feed.
3. **Data Isolation (Item Lists):** Filters the 40+ news articles down to just the single top headline to prevent notification spam.
4. **Merge Node (Combine by Position):** Stitches the isolated weather data and the single news article into one unified JSON object.
5. **Output (Telegram/Discord):** Formats the data into a readable message and sends the briefing.

## 🛠️ Prerequisites

To run this workflow, you need:
- An active [n8n](https://n8n.io/) instance (Desktop, Self-hosted, or Cloud).
- A destination for the message:
  - **Telegram:** A free bot token from [BotFather](https://core.telegram.org/bots#botfather).
  - **Discord:** A free [Webhook URL](https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks).

## 🚀 Installation

1. Download the `Demo_Workflow_in_Progress.json` file from this repository.
2. Open your n8n workspace and create a **New Workflow**.
3. Click the **Options menu** (the three dots `...` in the top right corner).
4. Select **Import from File** and upload the JSON file.
5. Open the final Output node (Telegram or Discord) and add your specific credentials.
6. Toggle the workflow to **Active** at the bottom of the screen.

## 🔧 Customization

You can easily adapt this workflow to your specific needs:

- **Change Location:** Open the `HTTP Request` node and update the `latitude` and `longitude` in the URL. (Currently set to `22.56` / `72.95`).
- **Change News Source:** Open the `RSS Read` node and swap the URL. Default is BBC World News, but any valid RSS feed will work.

## 🛡️ Fault Tolerance Note
The RSS Read node is configured with **"Continue On Fail"** enabled. If the news server times out or blocks the request, the workflow will not crash. It will gracefully pass an empty news value and still deliver your morning weather update.

## 📸 Workflow Preview

[n8n Workflow Screenshot](workflow.png)
