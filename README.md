# NextCloud Cookbook To Cooklang
A utility to convert NextCloud Cookbook JSON files to Cooklang format.

# Why?
Mostly a personal project for my own use case. I have hundreds of recipes collected over the years in[ NextCloud Cookbook](https://github.com/nextcloud/cookbook) format (JSON document with custom schema) but I prefer the Markdown like format of [CookLang](https://cooklang.org/). Cooklang syntax is very easy to visually read and share for non-technical users (compared to JSON) and it is easier to edit plain text files from any device.

# Project Status
The project is (finally) fully functional and it successfully converted my entire recipe collection! But I implemented it in an unexpected way; read the next section for how it works.

# How does it work?
The scripts in the directory will recursively loop over all of the recipe files in a directory and process conversions in groups of ten for parallelization.

It utilizes Perplexity's AI API endpoint to assist with the conversion. Given that most people only have a few hundred recipe files at most; it is cost effective to convert using an LLM. One hundred recipe conversions should cost well under one dollar.

The script includes a reference file specifying the Cooklang file format for the LLMs to reference for understanding. This is necessary because none of the existing LLM models can accurately author Cooklang files alone without bugs (I tested all of them available as of 12/2024). You must give it the full file format specification before usage to prevent hallucination.

So to recap the conversion script's tasks:
- The first step is to teach Perplexity the Cooklang syntax.
- Then to send it the file that needs to be converted to store in conversation context.
- Then it sends a clear instructional prompt for what to do (along with a few more reminders to not deviate from the file format specification to reduce the quantity of LLM hallucination bugs).

# Additional notes
I also included some personal preferences at the end of the file format reference file such as using imperial system units instead of metric system (I live in the USA). Adjust according to your preferences accordingly. 
