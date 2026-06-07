Context
You are an AI Assistant ,create a html UI with css

GO STEP BY STEP FOLLOWING THE INSTRUCTIONS PROVIDED UPON MY APPROVAL PROCEED WITH NEXT STEP.

STEPS
Instructions:
[SRTICTLY] DO NOT USE THE LANGFLOW EMBED CHAT
[MANDATORY] Generate the HTML page with custom inline chat UI that calls the Langflow API directly
[CRITICAL] Ensure that the chat interface is fully functional and properly integrated into the HTML page
[MANDATORY] Postion or place the chat inteface on the top right side of the page
[MANDATORY] Have the option to toggle the chat interface on and off with a button
[MANDATORY] Ensure that the toggle button is easily accessibile and  indicates the current state of the chat interface (on or off)
[MANDATORY] Add option to copy the chat output
[MANDATORY] Use CSS to style the chat interface and the toggle button to make them visually appealing and user-friendly
[MANDATORY] This chat interface is designed for Testcase generator
[MANDATORY] Ensure that the chat interface is easy to use and navigate for users who are looking to generate test cases
[MANDATORY] Implement clear option to clear chat messages
[MANDATORY] Include clear instructions or labels within the chat interface to guide users on how to use it effectively for generating test cases
[MANDATORY] Include a section of sample user story for a fund transfer with copy paste option to be pasted in chat interface

API Details:
curl --request POST \
     --url 'http://localhost:7860/api/v1/run/fc2ff262-f703-4f56-844d-2a5b62e909ca?stream=false' \
     --header 'Content-Type: application/json' \
     --data '{
		           "output_type": "chat",
		           "input_type": "chat",
		           "input_value": "Generate Fund Transfer testcases",
                   "session_id": "sk-d5SFgV3-bWpdJtXuR1_sg__-t_9xX2Td5i0U0k22lDI"
		         }'




















