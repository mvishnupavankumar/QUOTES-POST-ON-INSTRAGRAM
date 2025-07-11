# QUOTES-POST-ON-INSTRAGRAM

📸 Automated Instagram Quote Poster using n8n
📖 Description
This n8n workflow is designed for content creators and social media managers who want to automate their daily motivational quote posts on Instagram. It intelligently generates unique, visually appealing image prompts for AI image generation, creates the images, and then publishes them directly to your Instagram Business account via the Facebook Graph API.

For beginners: This workflow makes sure your Instagram page gets a new, inspiring picture every day, without you having to lift a finger!

For tech users: The workflow leverages the OpenRouter API to generate dynamic image prompts using a large language model (Gemini 2.5 Flash Lite), then sends these prompts to the Together AI API for image generation (using FLUX.1-schnell model). Finally, it uses the Facebook Graph API to upload the generated image and a predefined caption to an Instagram Business account. The entire process is scheduled to run daily.

⚙️ How It Works (step-by-step with emojis)
🔹 1. Schedule Trigger ⏰
Simple: This is the starting point! It automatically kicks off the entire workflow every day at 10 AM.

Tech: Uses the Schedule Trigger node configured to run daily at a specific hour.

🔹 2. SCRIPT 💬
Simple: This node talks to an AI to get a unique idea for our daily motivational image and its quote.

Tech: Makes an HTTP Request to the OpenRouter API, sending a detailed prompt to a Gemini 2.5 Flash Lite model to generate a new, unique image prompt based on a set of rules (e.g., varying animals, quotes, and styles).

🔹 3. IMAGE URL GENERATION 🎨
Simple: Takes the AI's idea and creates the actual image using another AI.

Tech: Performs an HTTP Request to the Together AI API, passing the prompt received from the previous "SCRIPT" node. It requests an image with specific dimensions (432x768) and a PNG format, using the black-forest-labs/FLUX.1-schnell model.

🔹 4. EXTRACT URL 🔗
Simple: Grabs the link to the newly created image and sets up the Instagram caption.

Tech: A Set node extracts the image_url from the Together AI response and sets a predefined caption for the Instagram post. It also configures the node parameter for the Facebook Graph API call.

🔹 5. Facebook Graph API1 ⬆️
Simple: This step prepares the image and caption to be posted on Instagram. It doesn't publish it yet, but gets it ready.

Tech: Uses the Facebook Graph API node to send a POST request to the /media edge. This stages the image and caption, returning a creation_id which is needed for the final publishing step.

🔹 6. Facebook Graph API ✅
Simple: This is the final step! It actually publishes the prepared image and caption to your Instagram account.

Tech: Another Facebook Graph API node is used to send a POST request to the /media_publish edge, using the creation_id obtained from the previous node to finalize the Instagram post.

🔁 Replace the following before running:
🔐 YOUR_OPENROUTER_BEARER_TOKEN
Replace this with your OpenRouter Bearer token in the Authorization header of the SCRIPT node.

🔑 YOUR_TOGETHER_AI_API_KEY
Replace this with your Together AI API Key in the Authorization header of the IMAGE URL GENERATION node.

🪪 REPLACE_ME (Facebook Graph Account ID)
You'll find this in the credentials section of both Facebook Graph API nodes. You need to configure your Facebook Graph API credentials in n8n first.

👤 YOUR_FACEBOOK_GRAPH_NODE
In the EXTRACT URL node, replace this placeholder with your actual Instagram Business Account ID. You can find this in your Facebook Developer settings.

🧪 Testing Instructions
✅ Open n8n at http://localhost:5678 (or wherever your n8n instance is running).
🔧 Click “Import Workflow” and paste the provided JSON.
🧪 To test each step individually, click on a node (e.g., "SCRIPT") and then click “Execute Node”.
🪵 Check the execution log at the bottom of the screen to troubleshoot any issues and verify the data flowing between nodes.
🚀 Once satisfied, activate the workflow by toggling the switch in the top right corner.

💡 Tips for Beginners
💡 Use the “Credentials” tab in n8n to set up your Facebook Graph API, OpenRouter, and Together AI API keys securely.
💡 Always check node outputs after each step in test mode to verify that the data is correct and flowing as expected.
💡 Adjust the schedule trigger in the "Schedule Trigger" node to fit your preferred daily posting time.
💡 If you encounter issues, the n8n documentation and community forums are great resources!
