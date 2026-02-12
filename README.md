# Smart Image Analyzer (Azure Durable Functions)

## Project Overview
This project implements a **Hybrid Serverless Pattern** using Azure Durable Functions to analyze images uploaded to Blob Storage. It demonstrates the transition from sequential chaining to complex orchestration, specifically utilizing the **Fan-Out/Fan-In** pattern to perform multiple image analyses in parallel.



## Architectural Patterns
* **Blob Trigger (Entry Point)**: Automatically reacts to new image uploads in the `images/` container.
* **Fan-Out/Fan-In**: The orchestrator launches four analysis activities (Colors, Objects, Text, and Metadata) simultaneously.
* **Function Chaining**: Once all parallel tasks complete, the results are "chained" into a report generator and finally persisted to Table Storage.

## Technical Features
* **Parallel Processing**: Uses `context.task_all()` to run CPU-bound image processing tasks concurrently.
* **Image Processing**: Utilizes the `Pillow` library for dominant color extraction and EXIF metadata analysis.
* **Persistence**: Stores results in **Azure Table Storage** using a unique UUID for each analysis record.
* **Monitoring**: Integrated with **Application Insights** for real-time invocation tracking and error logging.

## How to Run Locally
1. Ensure **Azurite** is running for local storage emulation.
2. Rename `local.settings.example.json` to `local.settings.json` and provide your connection strings.
3. Run `func start` in your terminal.
4. Upload an image to your local `images` blob container using **Azure Storage Explorer**.
5. Access results at `http://localhost:7071/api/results`.

## Project Demo
You can view the full walkthrough of Lab 2 here:
[Watch the Lab 2 Demo on YouTube](https://youtu.be/wEm9y3p8qU4)
